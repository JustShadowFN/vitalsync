# =============================================================================
# Multi-stage build – pourquoi ce choix ?
#
# Stage 1 (builder) : installe TOUTES les dépendances (y compris devDependencies)
#   et exécute les tests. Jest, supertest et ESLint ne quittent jamais ce stage.
#   Avantage sécurité : les outils de dev/test n'existent pas dans l'image finale,
#   réduisant la surface d'attaque.
#
# Stage 2 (production) : copie uniquement le code compilé et les dépendances de
#   production. On utilise node:20-alpine (~5 MB) au lieu de node:20 (~900 MB)
#   pour minimiser la taille de l'image et les vulnérabilités potentielles.
# =============================================================================

# ── Stage 1 : build + tests ───────────────────────────────────────────────────
FROM node:20-alpine AS builder

WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY . .

RUN npm test

# ── Stage 2 : image de production ────────────────────────────────────────────
FROM node:20-alpine AS production

WORKDIR /app

COPY package*.json ./
RUN npm ci --only=production

COPY --from=builder /app/server.js ./

ENV NODE_ENV=production

EXPOSE 3000

CMD ["node", "server.js"]
