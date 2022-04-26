FROM node:16.14.2-alpine3.15

COPY . .

# Download and install required tools.
RUN curl -L https://get.pulumi.com/ | bash
RUN npm install -g npm@8.5.2

ENV PATH=$PATH:/root/.pulumi/bin

ENTRYPOINT [ "pulumi", "version" ]
