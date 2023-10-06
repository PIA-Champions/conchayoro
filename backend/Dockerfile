FROM node:16-alpine As development
WORKDIR /src/app
COPY --chown=node:node package*.json ./
RUN npm ci
RUN ls -la
COPY --chown=node:node . .
USER node
FROM node:16-alpine As build
WORKDIR /src/app
COPY --chown=node:node package*.json ./
COPY --chown=node:node --from=development /src/app/node_modules ./node_modules
COPY --chown=node:node . .
CMD [ "npm", "start" ]
