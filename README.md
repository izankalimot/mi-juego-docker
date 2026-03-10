````markdown
# 🎮 Juego Web - Docker Compose

Este proyecto permite ejecutar la aplicación **Juego Web** utilizando **Docker Compose**, desplegando automáticamente:

¿En qué consiste?
Es un juego tipo clicker, haz click todo lo rápido que puedas durante 5 segundos para conseguir ser el mejor.

- Una **base de datos MySQL**
- Una **aplicación web**

---

# 📋 Requisitos

Antes de comenzar debes tener instalado:

- [Docker](https://www.docker.com/)
- Docker Compose (incluido en Docker moderno)

Comprobar instalación:

```bash
docker --version
docker compose version
````

---

# 📁 Estructura del proyecto

```
juego-docker/
│
└── docker-compose.yml
```

---

# ⚙️ Configuración del docker-compose

El sistema contiene **dos servicios principales**:

| Servicio | Descripción              |
| -------- | ------------------------ |
| `db`     | Base de datos MySQL      |
| `app`    | Aplicación web del juego |

## 🗄 Base de datos

* Imagen: `izankalimot/juego-db:latest`
* Base de datos: `juego_db`
* Usuario: `jugador`
* Contraseña: `player_password`
* Contraseña root: `root_password`
* Persistencia mediante volumen `db_data`

## 🌐 Aplicación Web

* Imagen: `izankalimot/juego-web:latest`
* Puerto expuesto: **8080**
* Depende del servicio de base de datos

---

# 🚀 Instalación y ejecución

1️⃣ Clonar o crear el proyecto.

2️⃣ Colocar el archivo `docker-compose.yml`.

3️⃣ Ejecutar:

```bash
docker compose up -d
```

Docker realizará automáticamente:

* Descarga de imágenes
* Creación de contenedores
* Inicio de servicios

---

# 🔍 Comprobar contenedores

```bash
docker ps
```

Deberías ver:

```
juego_db
juego_app
```

---

# 🌍 Acceder a la aplicación

Abrir en el navegador:

```
http://localhost:8080
```

---

# 💾 Persistencia de datos

Los datos de la base de datos se almacenan en el volumen:

```
db_data
```

Esto permite que **los datos se mantengan aunque los contenedores se eliminen**.

Ver volúmenes:

```bash
docker volume ls
```

---

# 🧾 Ver logs

Logs de todos los servicios:

```bash
docker compose logs
```

Logs en tiempo real:

```bash
docker compose logs -f
```

Logs de un servicio específico:

```bash
docker compose logs app
```

---

# 🔧 Acceder a MySQL manualmente

Entrar al contenedor:

```bash
docker exec -it juego_db mysql -u jugador -p
```

Contraseña:

```
player_password
```

---

# ⏹ Detener la aplicación

```bash
docker compose down
```

Esto detiene y elimina los contenedores pero **mantiene los datos**.

---

# 🔄 Reiniciar servicios

```bash
docker compose restart
```

---

# 🗑 Eliminar todo el entorno

Para eliminar contenedores **y datos**:

```bash
docker compose down -v
```

⚠️ **Advertencia:** esto eliminará la base de datos permanentemente.

---

# 📌 Comandos rápidos

| Acción           | Comando                  |
| ---------------- | ------------------------ |
| Iniciar          | `docker compose up -d`   |
| Ver contenedores | `docker ps`              |
| Ver logs         | `docker compose logs -f` |
| Parar            | `docker compose down`    |
| Reiniciar        | `docker compose restart` |
| Eliminar todo    | `docker compose down -v` |
