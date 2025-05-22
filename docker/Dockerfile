FROM node:20-alpine

RUN apk add --no-cache chromium

ENV PUPPETEER_SKIP_DOWNLOAD=true
ENV PUPPETEER_EXECUTABLE_PATH=/usr/bin/chromium-browser
ENV HOST=0.0.0.0
ENV FLOWISE_HOST=0.0.0.0

RUN npm install -g flowise

EXPOSE 3000

ENTRYPOINT ["sh", "-c", "flowise start --port ${PORT:-3000} --host 0.0.0.0"]
