# Rock R server image with dsSurvival for DataSHIELD/Opal.
# For the pilot on the existing stack, match the base image tag that is already running.
# For a multi-site rollout, pin ONE fixed tag at every site (never `latest`).
FROM datashield/rock-base:6.3-R4.4

# If apt-get fails on permissions, the base image runs as non-root:
# add `USER root` here and restore the original user afterwards.
# Check with: docker run --rm datashield/rock-base:6.3-R4.4 whoami
RUN apt-get update \
 && apt-get install -y --no-install-recommends libcurl4-openssl-dev libssl-dev libxml2-dev \
 && rm -rf /var/lib/apt/lists/*

RUN Rscript -e "install.packages(c('remotes','survival'), repos='https://cloud.r-project.org')" \
 && Rscript -e "remotes::install_github('neelsoumya/dsSurvival', ref='v2.1.3', upgrade='never')"

# Single quotes and no $ so Docker does not substitute anything in the R code.
RUN Rscript -e 'library(dsSurvival); d <- packageDescription("dsSurvival"); stopifnot(!is.null(d[["AggregateMethods"]])); cat("dsSurvival", as.character(packageVersion("dsSurvival")), "OK\n")'
