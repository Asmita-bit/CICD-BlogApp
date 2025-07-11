FROM node:20-alpine AS builder

WORKDIR /app

COPY package.json yarn.lock ./
RUN yarn install --frozen-lockfile

COPY . .

RUN yarn build


# Runtime Stage
FROM node:20-alpine AS runner

WORKDIR /app

RUN yarn global add serve


COPY --from=builder /app/dist /app/dist

EXPOSE 5173

CMD ["serve", "-s", "dist", "-l", "5173"]

