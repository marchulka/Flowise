# Stage 1: Build stage
FROM node:20-alpine AS build

USER root

ENV PUPPETEER_SKIP_DOWNLOAD=true

RUN npm install -g flowise

# Stage 2: Runtime stage
FROM node:20-alpine

RUN apk add --no-cache chromium git python3 py3-pip make g++ build-base cairo-dev pango-dev curl

ENV PUPPETEER_EXECUTABLE_PATH=/usr/bin/chromium-browser

COPY --from=build /usr/local/lib/node_modules /usr/local/lib/node_modules
COPY --from=build /usr/local/bin /usr/local/bin

# --- Вот тут важные изменения: ---
# 1. Экспортируем порт для ясности (не критично для Render, но хорошо для читаемости)
EXPOSE 3000

# 2. Переменные окружения всегда явно задаём
ENV HOST=0.0.0.0
ENV FLOWISE_HOST=0.0.0.0

# 3. Самое главное: подставляем порт из окружения Render (он задается в $PORT)
ENTRYPOINT ["sh", "-c", "flowise start --port ${PORT:-3000} --host 0.0.0.0"]
