# CRUD Application con Docker 🐳

Aplicación CRUD completa con Node.js, Express y PostgreSQL usando Docker y Docker Compose.

## 📋 Características

- ✅ CRUD completo de productos (Create, Read, Update, Delete)
- 🎨 Interfaz web moderna y responsive
- 🐘 Base de datos PostgreSQL
- 🐳 Completamente dockerizada
- 📦 Listo para subir a DockerHub

## 🚀 Inicio Rápido

### Opción 1: Usar Docker Compose (Recomendado)

```bash
# Clonar o navegar al directorio
cd C:\Users\pinnc\docker-crud-app

# Levantar la aplicación
docker-compose up -d

# Ver logs
docker-compose logs -f

# Detener la aplicación
docker-compose down
```

### Opción 2: Construir y ejecutar manualmente

```bash
# Construir la imagen
docker build -t crud-app .

# Ejecutar PostgreSQL
docker run -d \
  --name crud_postgres \
  -e POSTGRES_PASSWORD=postgres123 \
  -e POSTGRES_DB=cruddb \
  -p 5432:5432 \
  postgres:15-alpine

# Ejecutar la aplicación
docker run -d \
  --name crud_app \
  -p 3000:3000 \
  -e DB_HOST=host.docker.internal \
  crud-app
```

## 🌐 Acceso

Una vez levantada la aplicación, accede a:

**http://localhost:3000**

## 📤 Subir a DockerHub

### 1. Login en DockerHub

```bash
docker login
```

### 2. Etiquetar la imagen

```bash
# Reemplaza 'tu-usuario' con tu nombre de usuario de DockerHub
docker tag crud-app tu-usuario/crud-app:latest
docker tag crud-app tu-usuario/crud-app:1.0.0
```

### 3. Subir la imagen

```bash
docker push tu-usuario/crud-app:latest
docker push tu-usuario/crud-app:1.0.0
```

### 4. Usar la imagen desde DockerHub

```bash
docker pull tu-usuario/crud-app:latest
docker run -d -p 3000:3000 tu-usuario/crud-app:latest
```

## 🛠️ Tecnologías Utilizadas

- **Backend**: Node.js + Express
- **Base de datos**: PostgreSQL
- **Frontend**: HTML5 + CSS3 + JavaScript vanilla
- **Containerización**: Docker + Docker Compose

## 📊 Estructura del Proyecto

```
docker-crud-app/
├── public/
│   └── index.html          # Interfaz web
├── server.js               # Servidor Express
├── package.json            # Dependencias
├── Dockerfile              # Construcción de la imagen
├── docker-compose.yml      # Orquestación de contenedores
├── .dockerignore          # Archivos a ignorar
└── README.md              # Este archivo
```

## 🔧 Variables de Entorno

| Variable | Valor por defecto | Descripción |
|----------|-------------------|-------------|
| `PORT` | `3000` | Puerto del servidor |
| `DB_HOST` | `db` | Host de PostgreSQL |
| `DB_PORT` | `5432` | Puerto de PostgreSQL |
| `DB_USER` | `postgres` | Usuario de BD |
| `DB_PASSWORD` | `postgres123` | Contraseña de BD |
| `DB_NAME` | `cruddb` | Nombre de la BD |

## 📝 API Endpoints

- `GET /api/productos` - Obtener todos los productos
- `GET /api/productos/:id` - Obtener un producto por ID
- `POST /api/productos` - Crear un nuevo producto
- `PUT /api/productos/:id` - Actualizar un producto
- `DELETE /api/productos/:id` - Eliminar un producto
- `GET /health` - Health check del servidor

## 🎯 Comandos Útiles

```bash
# Ver contenedores en ejecución
docker ps

# Ver logs de la aplicación
docker logs crud_app -f

# Ver logs de la base de datos
docker logs crud_postgres -f

# Entrar al contenedor de la app
docker exec -it crud_app sh

# Entrar a PostgreSQL
docker exec -it crud_postgres psql -U postgres -d cruddb

# Limpiar todo (contenedores, imágenes, volúmenes)
docker-compose down -v
docker system prune -a
```

## 🐛 Troubleshooting

### La aplicación no se conecta a la BD

1. Verificar que el contenedor de PostgreSQL esté corriendo:
   ```bash
   docker ps | grep postgres
   ```

2. Ver logs de la BD:
   ```bash
   docker logs crud_postgres
   ```

### Puerto 3000 ya está en uso

Cambiar el puerto en `docker-compose.yml`:
```yaml
ports:
  - "8080:3000"  # Usar puerto 8080 en lugar de 3000
```

## 📄 Licencia

MIT

## 👨‍💻 Autor

Taller Docker - CRUD Application
