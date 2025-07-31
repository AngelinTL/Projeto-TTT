# Etapa de build
FROM node:18-alpine as build

WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY . .

# Executa build com configuração de produção
RUN npm run build -- --configuration production

# Etapa final com nginx
FROM nginx:alpine

# Limpa o HTML padrão do nginx
RUN rm -rf /usr/share/nginx/html/*

# Copia build Angular (ajustado para o caminho real do build)
COPY --from=build /app/dist/login-page/browser /usr/share/nginx/html

# Copia configuração personalizada do nginx
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

