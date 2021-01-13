# Containerizing the VUE Hello World Node Application

This small set of instructions will help you containerize the vue-cli and hello-world Node.js application.

### Pre-requisites:
* Ensure that you have git-scm installed on your local system.
* Ensure that you have Node.js installed on your local system.
* Ensure that you have a operational docker installation.

### High Level Steps for building the container on MacOS:
```
1. Install Docker Desktop
2. Install Homebrew
3. Install Node.js
4. Install the vue cli
5. Create the vue hello-world application
6. Create the Dockerfile at the root of the app directory
7. Run the docker build command to build the application
8. Use docker run to bind port 8080 to the localhost and run the container.
```

### Steps for building the vue hello-world docker container:

**Install Homebrew:**
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

**Update Homebrew:**
- brew update

**Run Brew doctor:**
- brew doctor

**Install node JS with Home-brew:**
- brew install node

**Install the VUE CLI using NPM:**
- npm install -g @vue/cli

**Create the  VUE  hello-world application:**
- vue create hello-world

**CD into the “hello-world” directory and create a file called Dockerfile:**
- cd hello-world
- touch Dockerfile

**Add the following text to the DockerFile:**
```
FROM node:lts-alpine

RUN npm install -g http-server

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

RUN npm run build

EXPOSE 8080

CMD [ "http-server", "dist" ]
```
**Create the Docker image:**
- docker build -t vue-hello-world .

**Run the containerized Node application:**
- docker run -it -p 8080:8080 —rm —name vue-hello-world
