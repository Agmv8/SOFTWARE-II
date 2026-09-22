# Producto V: Gestión de Configuración, Versionamiento y DevOps - Unidad 5

## Contenido de la Carpeta

* **Documento:** [Resolucion_Unidad_5_ISII.pdf](./Resolucion_Unidad_5_ISII.pdf)

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