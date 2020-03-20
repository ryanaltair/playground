FROM node:12-alpine AS deps
RUN apk add jq
COPY package.json /tmp
RUN jq '{ dependencies, devDependencies }' < /tmp/package.json > /tmp/deps.json

FROM node:12-slim
WORKDIR /home/app/
COPY --from=deps /tmp/deps.json ./package.json
COPY package-lock.json .npmrc ./
RUN npm install --only=production
COPY index.js ./
CMD [ "bash" ]