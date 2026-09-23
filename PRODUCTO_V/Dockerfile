# ==============================================================================
# ETAPA 1: Construcción y Dependencias (Builder)
# ==============================================================================
FROM node:18-alpine AS builder

# Establecer el directorio de trabajo dentro del contenedor
WORKDIR /app

# Copiar archivos de definición de paquetes primero (aprovechamiento de caché de capas)
COPY package*.json ./

# Instalar todas las dependencias (incluidas devDependencies para compilación y pruebas)
RUN npm ci

# Copiar el resto del código fuente del proyecto
COPY . .

# ==============================================================================
# ETAPA 2: Entorno Ligero de Producción (Runner)
# ==============================================================================
FROM node:18-alpine AS runner

# Establecer la variable de entorno a producción
ENV NODE_ENV=production

WORKDIR /app

# Crear un grupo y usuario no raíz por razones de seguridad (Principio de Menor Privilegio)
RUN addgroup -g 1001 -S nodejs && adduser -S nodejs -u 1001

# Copiar archivos de paquetes e instalar únicamente dependencias de producción
COPY package*.json ./
RUN npm ci --only=production && npm cache clean --force

# Copiar artefactos procesados desde la etapa builder asignando permisos al usuario nodejs
COPY --from=builder --chown=nodejs:nodejs /app/server.js ./
COPY --from=builder --chown=nodejs:nodejs /app/src ./src
# Cambiar al usuario no privilegiado
USER nodejs

# Exponer el puerto de la aplicación
EXPOSE 8080

# Comando de arranque de la aplicación
CMD ["node", "server.js"]