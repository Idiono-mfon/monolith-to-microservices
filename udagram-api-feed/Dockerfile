# STAGE 1

FROM node:12-alpine AS build
# Create app directory
WORKDIR /usr/src/app
# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied where available (npm@5+)
COPY package*.json ./
RUN npm ci 
# Bundle app source
COPY . .

# Build Service
RUN npm run build-server

# STAGE 2

FROM node:12-alpine

# Set work directory for Stage 2 build
WORKDIR /usr/src/app

# A wildcard is used to ensure both package.json AND package-lock.json are copied where available (npm@5+)

COPY package*.json ./

RUN npm ci 

COPY --from=build /usr/src/app/www ./www

# Container Port
EXPOSE 8080

CMD [ "npm", "run", "prod" ]
