FROM node:18.15.0-alpine3.17

COPY . .

# Download and install required tools.
RUN apk --no-cache add curl
RUN apk --no-cache add bash
RUN curl -L https://get.pulumi.com/ | sh
RUN npm install -g npm@10.8.1

ENV PATH=$PATH:/root/.pulumi/bin

ENTRYPOINT [ "pulumi", "version" ]
