FROM node:20.18.0-bullseye

# Log versions
RUN set -x \
    && node -v \
    && npm -v

RUN npm i -g npm@8.19.3

WORKDIR /bitcore

# Add source
# NOTE(danny): this is really suboptimal, but we will fix as we move to `turbo`
COPY package*.json ./
COPY packages/ ./packages/

# Install dependencies and build
RUN npm install --ignore-scripts

# not sure why this isn't being found, so just manually install for now
RUN npm install xrpl-secret-numbers
RUN npm install @dabh/diagnostics
RUN npm install fn.name
RUN npm install require_optional

# Build the typescript files
RUN npm run compile

# build this package
WORKDIR /bitcore/packages/bitcore-wallet-service
RUN npm run tsc

# Start the server
CMD ["./start.sh"]