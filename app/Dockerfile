# Estágio 1: Builder da aplicação
FROM node:18-alpine as builder
WORKDIR /usr/src/app
COPY package*.json ./
RUN npm install
COPY . .

# Estágio 2: Imagem final com o arquivo grande
FROM node:18-alpine
WORKDIR /root/
COPY --from=builder /usr/src/app .

# Comando para criar um arquivo de 8GB
# O fallocate cria um arquivo de um determinado tamanho rapidamente, sem de fato escrever zeros,
# o que torna o build da imagem mais rápido. A imagem final terá o tamanho desejado.
RUN apk add --no-cache util-linux && \
    fallocate -l 8G large_file.img

EXPOSE 8080
CMD ["npm", "start"]