# Use explicit image reference
FROM node:lts-bullseye-slim@sha256:d93fb5c25db163dc795d40eabf66251a2daf6a2c6a2d21cc29930e754aef4c2c

# dumb-init as process manager to forward signals
RUN apt-get update -y && apt-get install --no-install-recommends -y curl &&  apt-get install --no-install-recommends -y dumb-init \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/*

ENV PORT=3000

COPY . /frontend-react-js

WORKDIR /frontend-react-js

RUN npm install && npm clean cache --force

RUN chown -R node /frontend-react-js

EXPOSE ${PORT}
# Never run application as root user
USER node

ENTRYPOINT ["/usr/bin/dumb-init", "--"]

CMD ["/bin/bash", "-c", "npm start"]