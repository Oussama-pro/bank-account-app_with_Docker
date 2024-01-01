# Stage 1: Compile and Build angular codebase  /-> comme en dans backend en genere les service.jar

# Use official node image as the base image
FROM node:latest as build

# Set the working directory /->   dossier de travail et ou se enregistrer les fichier de mon app front-end
WORKDIR /usr/Local/app

# Add the source code to app   /->   ./ : copier tous les fichier de app dans Workdir qui est dans ce chemin: /usr/Local/app/
COPY ./ /usr/Local/app/

# Instalt all the dependencies   /-> dans mon directoey "WORKDIR" va executer cette commande pour installer les dependence psq en ne copy pas le dossier node module, danc en va deplacer le fichier "package.json" et en a installer les depd necessaire
RUN npm install


# Generate the build of the application  /->npm run build: executer le script build  qui se trouve dans fichier package.json  scripts": { "build": "ng build", },
RUN npm run build   #equivalent de "ng build" dans backend "mvn clean package -DskipTests"

# Stage 2: Serve app with nginx server

# Use official nginx image as the base image   /-> je creer un image qui se base sur l'image de serveur web nginx
FROM nginx:latest

# Copy the build output to replace the default nginx contents.  /-> en peut faire ca manuellement
COPY --from=build /usr/Local/app/dist/angular-front-end/browser /usr/share/nginx/html

# Expose port 80
EXPOSE 80
