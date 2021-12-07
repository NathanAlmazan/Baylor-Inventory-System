FROM node:alpine AS deps

RUN apk add --no-cache libc6-compat
WORKDIR /app
COPY package*.json ./
RUN npm ci

FROM node:alpine AS builder
WORKDIR /app
COPY . .
COPY --from=deps /app/node_modules ./node_modules
RUN npm install --production 

ENV NODE_ENV production
ENV API_BASE_URL="https://baylor-company.herokuapp.com"
ENV SECRET_KEY="wyIJ2wMLRTNw9CPSTjblem39iFa2fxScnw3L4Zzy"
ENV BACKEND_KEY="eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOjAsInVzZXJuYW1lIjoiRnJvbnQgU2VydmVyIiwicG9zaXRpb24iOiJTZXJ2ZXIiLCJpYXQiOjE2MzU3NDQyMzl9.R4Y5_DPgMIZ8tNVUuQ4ZZnLWa6XPne_S1RQpTUgorUE"
ENV NEXTAUTH_URL="http://localhost:3000"
ENV SECRET="INp8IvdIyeMcoGAgFGo8IvdIyeMcoGAgFGo8IvdIyeMcoGAgFGogFGo8IvdIyeMco"
ENV NODE_OPTIONS=--openssl-legacy-provider

RUN npm run build

FROM node:alpine AS runner
WORKDIR /app

RUN addgroup -g 1001 -S nodejs
RUN adduser -S nextjs -u 1001

COPY --from=builder /app/public ./public
COPY --from=builder --chown=nextjs:nodejs /app/.next ./.next
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/package.json ./package.json

ENV API_BASE_URL="http://172.19.0.3:4000"
ENV SECRET_KEY="wyIJ2wMLRTNw9CPSTjblem39iFa2fxScnw3L4Zzy"
ENV BACKEND_KEY="eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOjAsInVzZXJuYW1lIjoiRnJvbnQgU2VydmVyIiwicG9zaXRpb24iOiJTZXJ2ZXIiLCJpYXQiOjE2MzU3NDQyMzl9.R4Y5_DPgMIZ8tNVUuQ4ZZnLWa6XPne_S1RQpTUgorUE"
ENV NEXTAUTH_URL="http://localhost:3000"
ENV SECRET="INp8IvdIyeMcoGAgFGo8IvdIyeMcoGAgFGo8IvdIyeMcoGAgFGogFGo8IvdIyeMco"

USER nextjs

EXPOSE 3000

ENV PORT 3000

CMD ["node_modules/.bin/next", "start"]