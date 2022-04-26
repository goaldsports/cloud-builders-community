FROM node:16.14.2-alpine3.15

COPY . .

# Download and install required tools.
RUN apk --no-cache add curl
RUN curl -L https://get.pulumi.com/ | sh
RUN npm install -g npm@8.5.2

ENV PATH=$PATH:/root/.pulumi/bin

ENTRYPOINT [ "pulumi", "version" ]
