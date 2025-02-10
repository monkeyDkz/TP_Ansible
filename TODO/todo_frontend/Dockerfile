# Utiliser une image de base officielle de Node.js
FROM node:14

# Définir le répertoire de travail dans le conteneur
WORKDIR /usr/src/app

# Copier les fichiers package.json et package-lock.json
COPY package*.json ./

# Installer les dépendances
RUN npm install

# Copier le reste des fichiers de l'application
COPY . .

# Construire l'application React
RUN npm run build

# Installer Nginx pour servir l'application
FROM nginx:alpine
COPY --from=0 /usr/src/app/build /usr/share/nginx/html

# Copier le fichier de configuration Nginx
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Exposer le port sur lequel l'application va tourner
EXPOSE 80

# Définir la commande pour démarrer Nginx
CMD ["nginx", "-g", "daemon off;"]