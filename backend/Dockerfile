FROM node:18-alpine AS deps

WORKDIR /app

COPY package*.json ./

RUN npm install --legacy-peer-deps

FROM node:18-alpine AS runner
WORKDIR /app

RUN addgroup --system appgroup && adduser --system --ingroup appgroup appuser

COPY --from=deps /app/node_modules ./node_modules
COPY . .

RUN mkdir -p ./uploads

RUN chown -R appuser:appgroup /app

USER appuser
EXPOSE 8000
CMD ["node", "index.js"]