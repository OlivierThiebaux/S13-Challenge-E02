# Stage 1: Dépendances
FROM node:latest AS dependances
WORKDIR /app
COPY package*.json ./
RUN npm install

# Stage 2: Builder
FROM node:latest AS builder
WORKDIR /app
#COPY --from=dependances /app/node_modules ./node_modules
COPY ./ ./
RUN npm run build

# Stage 3: Production
FROM node:latest AS production
WORKDIR /app

COPY --from=builder /app/dist ./dist
#COPY --from=builder /app/node_modules ./node_modules
COPY package*.json ./

# Variables d'environnement communes
ENV NODE_ENV production
ENV PORT 3000

# Utilisateur non privilégié pour la sécurité
USER node

# Exposition du port
EXPOSE $PORT

# Démarrage de l'application
CMD ["node", "dist/main"]
