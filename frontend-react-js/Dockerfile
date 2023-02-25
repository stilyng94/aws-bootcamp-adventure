FROM node:16.18

# Install curl to use for health check and dumb-init as process manager
RUN apt-get install --no-install-recommends -y curl && apt-get install --no-install-recommends -y dumb-init \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/*

ENV PORT=3000

COPY . /frontend-react-js

WORKDIR /frontend-react-js

RUN npm install

RUN chown -R node /frontend-react-js

EXPOSE ${PORT}
# Never run application as root user
USER node

ENTRYPOINT ["/usr/bin/dumb-init", "--"]

CMD ["/bin/bash", "-c", "npm","start"]