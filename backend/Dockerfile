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
RUN npm install
RUN ls -la 
ENV NODE_ENV production
RUN npm ci --only=production && npm cache clean --force
USER node
FROM node:16-alpine As production
COPY --chown=node:node --from=build /src/app/node_modules ./node_modules
COPY --chown=node:node --from=build /src/app/dist ./dist
CMD [ "node", "dist/main.js" ]
