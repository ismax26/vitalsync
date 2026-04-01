# Multi-stage build : permet de séparer l'étape de build/test de l'image finale.
# Avantages : l'image de production est plus légère (pas de devDependencies)
# et plus sécurisée (moins de surface d'attaque, pas d'outils de build).

# Stage 1 : Installation des dépendances et exécution des tests
FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm test

# Stage 2 : Image de production légère
FROM node:20-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install --only=production
COPY --from=builder /app/server.js .
EXPOSE 3000
USER node
CMD ["node", "server.js"]