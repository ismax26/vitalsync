
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
```

Crée aussi `backend/.dockerignore` :
```
node_modules
npm-debug.log
.git
.gitignore
test
coverage
.env