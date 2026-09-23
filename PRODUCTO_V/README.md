# Producto V: Gestión de Configuración, Versionamiento y DevOps - Unidad 5

## Contenido de la Carpeta

* **Documento:** [Unidad_5_ISII.pdf](./Unidad_5_ISII.pdf)

## Enlace de la Defensa en Video

* **Enlace Único del Video:** https://drive.google.com/file/d/1sKCEcGewdxj8uEX2GUQjqSk_nxvyifM-/view?usp=sharing

## Ejercicio 2: Construcción y Prueba del Contenedor Docker

### 1. Construir la imagen
```bash
docker build -t app-facturacion:1.0 .
```

### 2. Ejecutar el contenedor
```bash
docker run -d --name test-facturacion -p 8080:8080 app-facturacion:1.0
```

### 3. Verificar logs
```bash
docker logs test-facturacion
```

### 4. Verificar conexión
```bash
Invoke-WebRequest -Uri http://localhost:8080  # PowerShell
# o
curl http://localhost:8080  # Git Bash o WSL
```

### 5. Detener y limpiar
```bash
docker stop test-facturacion
docker rm test-facturacion
```