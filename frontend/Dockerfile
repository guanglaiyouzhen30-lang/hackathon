FROM node:20-slim

WORKDIR /app

# npmパッケージのインストール
# package.jsonとpackage-lock.json(あれば)を先にコピーしてキャッシュを活かす
COPY package.json package-lock.json* ./
RUN npm install

# ソースコードのコピー
COPY . .