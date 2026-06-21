FROM node:18.20.4-alpine3.20

COPY . .

# Download and install required tools.
# Pin the Pulumi CLI version. Previously this used `curl get.pulumi.com | sh`
# with no --version, so the image baked whatever CLI was latest at build time
# (it drifted to 3.119.0). The deploy then ran that stale CLI against newer
# @pulumi/pulumi SDKs from the app node_modules, and the CLI<->SDK protocol
# mismatch failed gRPC (de)serialisation ("b.oa/b.Va is not a function") on
# every resource call. Keep this in lockstep with the @pulumi/pulumi version
# the apps depend on.
ARG PULUMI_VERSION=3.120.0
RUN apk --no-cache add curl
RUN apk --no-cache add bash
RUN curl -L https://get.pulumi.com/ | sh -s -- --version ${PULUMI_VERSION}
RUN npm install -g npm@10.8.1

ENV PATH=$PATH:/root/.pulumi/bin

ENTRYPOINT [ "pulumi", "version" ]
