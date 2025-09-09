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

# Comando para criar um arquivo de 8GB com dados aleatórios (não compressíveis)
# ATENÇÃO: Este comando é EXTREMAMENTE LENTO e pode levar muitos minutos para ser concluído.
# Ele lê de /dev/urandom (dados aleatórios) para garantir que a camada da imagem não seja comprimida.
RUN dd if=/dev/urandom of=large_file.img bs=1M count=400

EXPOSE 8080
CMD ["npm", "start"]