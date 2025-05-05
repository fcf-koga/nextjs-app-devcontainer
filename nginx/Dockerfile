# Nginx 1.24（軽量な Alpine ベース）を使用
FROM nginx:1.24-alpine

# 環境切り替え（dev または prod）で設定ファイルを分岐
ARG NGINX_ENV=prod

# 環境に応じた nginx.conf をコピー
COPY nginx.${NGINX_ENV}.conf /etc/nginx/nginx.conf

# 必要に応じて静的ファイルやその他設定をここで追加可能
# COPY ./static /usr/share/nginx/html
