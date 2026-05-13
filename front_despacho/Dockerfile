# Etapa 1: Build de la aplicación
FROM node:20-alpine AS build-stage
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Etapa 2: Servidor de producción (Nginx)
FROM nginx:stable-alpine
# Copiamos los archivos compilados al directorio de Nginx
COPY --from=build-stage /app/dist /usr/share/nginx/html
# Copiamos una configuración personalizada si fuera necesario
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]