FROM node:20-alpine AS deps
WORKDIR /app
COPY package.json yarn.lock ./
# RUN yarn install --frozen-lockfile
RUN yarn install 
FROM node:20-alpine AS builder
WORKDIR /app
COPY --from=deps /app/node_modules ./node_modules
COPY . .
ARG VITE_CLERK_PUBLISHABLE_KEY
ENV VITE_CLERK_PUBLISHABLE_KEY=$VITE_CLERK_PUBLISHABLE_KEY
RUN yarn build
FROM node:20-alpine AS runner
WORKDIR /app
RUN yarn global add serve
COPY --from=builder /app/dist ./dist
EXPOSE 5173
CMD ["serve", "-s", "dist", "-l", "5173"]



