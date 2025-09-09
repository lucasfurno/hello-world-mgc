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

# Comando para criar um arquivo de 8GB escrevendo dados reais
# ATENÇÃO: Este comando é lento e irá demorar vários minutos para ser concluído.
# Ele lê do /dev/zero (bytes nulos) e escreve um arquivo de 8GB (8192 blocos de 1MB).
RUN dd if=/dev/zero of=large_file.img bs=1M count=8192

EXPOSE 8080
CMD ["npm", "start"]