FROM node:18 AS base
CMD [ "bash" ]

# Build
FROM base AS test-and-build
COPY . /workspace
WORKDIR /workspace
ARG REACT_APP_API_SERVER
# 環境変数を引数で設定
RUN npm ci && npm run test && npm run build

# Hosting in nginx
FROM nginx:latest AS production
COPY --from=test-and-build /workspace/build /var/www
# nginxの設定ファイル
COPY nginx.conf /etc/nginx/conf.d/default.conf
