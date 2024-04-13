# ### Build


# FROM  --platform=linux/x86_64 beevelop/ionic AS ionic
# ## Create app directory
# WORKDIR /usr/src/app
# ## Install app dependencies
# ## A wildcard is used to ensure both package.json AND package-lock.json are copied
# COPY package*.json ./
# RUN npm ci --force
# ## Bundle app source
# COPY . .
# RUN ionic build
# ### Run 
# FROM nginx:alpine
# #COPY www /usr/share/nginx/html
# COPY --from=ionic  /usr/src/app/www /usr/share/nginx/html

### Build Stage ###
FROM node:16 AS build

# Install Ionic CLI globally
RUN npm install -g @ionic/cli

# Set working directory
WORKDIR /usr/src/app

# Copy package.json and package-lock.json files
COPY package*.json ./

# Install app dependencies
RUN npm ci --legacy-peer-deps

# Copy the rest of the application
COPY . .

# Build the application
RUN npx ionic build

### Production Stage ###
FROM nginx:alpine

# Copy built files from the previous stage
COPY --from=build /usr/src/app/www /usr/share/nginx/html