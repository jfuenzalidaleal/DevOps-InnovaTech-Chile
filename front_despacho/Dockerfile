# ETAPA 1: Construcción del Front (Vite)
FROM node:20-alpine AS build
WORKDIR /app

# Copiar archivos de dependencias
COPY package*.json ./
RUN npm install

# Copiar el resto del código y generar la versión de producción
COPY . .
RUN npm run build

# ETAPA 2: Servidor Web Nginx
FROM nginx:stable-alpine

# CAMBIO AQUÍ: Vite genera la carpeta "dist", no "build"
COPY --from=build /app/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]