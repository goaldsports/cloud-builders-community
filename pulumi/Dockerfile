FROM node:24-alpine

COPY . .

# Download and install required tools.
# Pin the Pulumi CLI version. Previously this used `curl get.pulumi.com | sh`
# with no --version, so the image baked whatever CLI was latest at build time.
# NOTE: lockstep with the apps' @pulumi/pulumi SDK (3.120.0) is NOT the fix
# for the "b.Va/b.oa is not a function" gRPC failures — the June 2026 image
# pinned 3.120.0 CLI in lockstep and every deploy-functions-app-* build still
# failed. Pulumi's compatibility model is newer-CLI-supports-older-SDK, and
# CLI 3.247.0 on a current node is verified clean against the notifications
# deployment program (register, read, and refresh paths) with SDK 3.120.0.
ARG PULUMI_VERSION=3.247.0
RUN apk --no-cache add curl
RUN apk --no-cache add bash
RUN curl -fsSL https://get.pulumi.com/ | sh -s -- --version ${PULUMI_VERSION}

ENV PATH=$PATH:/root/.pulumi/bin

ENTRYPOINT [ "pulumi", "version" ]
