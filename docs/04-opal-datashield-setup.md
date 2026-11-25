# 4. Opal / DataSHIELD setup

## Local test stack

The test instance runs with Docker on Windows (WSL) and has four containers:

| Container | Image / role |
|-----------|-------------|
| `opal1-opal` | Opal server |
| `opal1-rock` | R server (`datashield/rock-base`) |
| `opal1-nginx` | Reverse proxy |
| `opal1-mongo` | Opal database |

Opal reaches Rock by container name over the internal Docker network. Rock has no host port mapping.

## Adding dsSurvival

Opal's UI blocks R package installation, so dsSurvival has to be **baked into the Rock image**. See [`docker/rock-survival/Dockerfile`](../docker/rock-survival/Dockerfile).

- Server package: **`neelsoumya/dsSurvival`** (not `datashield/...`), pinned to **v2.1.3**. This version includes fixes for stratified and ggplot survival curves.
- Client package: `neelsoumya/dsSurvivalClient`, same tag.

### Pilot approach (single server)

Rebuild the existing Rock service and stay on the `default` profile:

```yaml
  rock:
    build: ./rock-survival
    image: aphrc/rock-survival:1.0
    container_name: opal1-rock
    # everything else unchanged
```

```bash
docker compose build --no-cache rock
docker compose up -d --force-recreate rock
docker exec opal1-rock Rscript -e 'cat(intersect(rownames(installed.packages()), c("dsBase","dsSurvival")), sep="\n")'
```

```r
library(opalr)
o <- opal.login(username = "administrator", password = "<password>", url = "<opal-url>")
dsadmin.publish_package(o, "dsSurvival", profile = "default")
dsadmin.get_methods(o, type = "aggregate", profile = "default")
```

### Before a multi-site rollout

- [ ] **Pin a fixed `rock-base` tag at every site.** If sites use `latest`, they can end up on different dsBase versions, and SLMA will still pool coefficients from them without warning.
- [ ] **Check dsBase compatibility between client and server.** The dsSurvival README pairs its client with `dsBaseClient@6.1.1`, but `rock-base:6.3-*` ships dsBase 6.3.x.
- [ ] Check the tag exists: `git ls-remote --tags https://github.com/neelsoumya/dsSurvival`
- [ ] Optionally move dsSurvival to a dedicated `survival` profile or cluster.

TODO: record the final deployed image tag and the dsBase versions in use.
