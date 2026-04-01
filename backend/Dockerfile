# Multi-stage build : le stage "builder" installe TOUTES les dépendances
# (y compris devDependencies) et exécute les tests dans un environnement isolé.
# Le stage "production" repart de zéro avec une image alpine minimale :
# - les devDependencies (jest, supertest…) ne sont jamais copiées dans l'image finale
# - la surface d'attaque est réduite (moins de binaires, pas d'outils de build)
# - l'image finale est ~3x plus légère qu'avec node:20 standard
# Résultat : image de prod sécurisée, sans artefacts de test ni dépendances inutiles.

# Stage 1 : build & test
FROM node:20-alpine AS builder

WORKDIR /app

COPY package.json ./
RUN npm install

COPY . .
RUN npm test

# Stage 2 : production
FROM node:20-alpine AS production

WORKDIR /app

COPY package.json ./
RUN npm install --omit=dev

COPY --from=builder /app/server.js ./

EXPOSE 3000

CMD ["node", "server.js"]
