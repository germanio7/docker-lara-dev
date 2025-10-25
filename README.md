# Laravel Multi-Project Docker Dev Environment 🐳

Este entorno permite desarrollar múltiples proyectos **Laravel** con diferentes versiones de **PHP** y **Node.js**, utilizando servicios compartidos como **Nginx**, **MySQL**, **phpMyAdmin** y **Mailpit**.

---

## 📁 Estructura del Proyecto
```bash
laravel-docker-dev/
├── docker-compose.yml
├── nginx/
│ └── default.conf
├── php/
│ ├── php74/
│ │ └── Dockerfile
│ └── php82/
│ └── Dockerfile
├── node/
│ ├── node16/
│ │ └── Dockerfile
│ └── node18/
│ └── Dockerfile
└── projects/
├── proyecto1/ (PHP 7.4 + Node 16)
└── proyecto2/ (PHP 8.2 + Node 18)
```

---

## ⚙️ Servicios

| Servicio     | Puerto  | Descripción                          |
|--------------|---------|--------------------------------------|
| Nginx        | 80      | Servidor HTTP para los proyectos     |
| MySQL        | 3306    | Base de datos                        |
| phpMyAdmin   | 8080    | Cliente web para MySQL               |
| Mailpit      | 8025    | Captura de correos SMTP              |
| Laravel App  | http://proyecto1.local, http://proyecto2.local |
| Node.js      | 2 contenedores con diferentes versiones       |

---

## 🧩 Requisitos Previos

- Docker y Docker Compose instalados
- Acceso sudo para editar `/etc/hosts`

---

## 🧑‍💻 Instrucciones

### 1. Clona este repositorio

```bash
git clone <REPO_URL> laravel-docker-dev
cd laravel-docker-dev
```

### 2. Agrega tus proyectos Laravel

Coloca tus proyectos en las siguientes carpetas:

```bash
projects/proyecto1/
projects/proyecto2/
```
El código debe tener el archivo `public/index.php` como punto de entrada.


### 3. Configura tu archivo hosts

Edita `/etc/hosts` y agrega:

```lua
127.0.0.1 proyecto1.local
127.0.0.1 proyecto2.local
```

### 4. Configura `.env` en Laravel para Mailpit

Edita `/etc/hosts` y agrega:

```env
MAIL_MAILER=smtp
MAIL_HOST=mailpit
MAIL_PORT=1025
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS=test@example.com
MAIL_FROM_NAME="${APP_NAME}"
```

### 5. Levanta los contenedores

Coloca tus proyectos en las siguientes carpetas:

```bash
docker-compose up -d --build
```

### 6. Accede a los servicios

* Proyecto 1 (PHP 7.4): http://proyecto1.local
* Proyecto 2 (PHP 8.2): http://proyecto2.local
* phpMyAdmin: http://localhost:8080
* Mailpit: http://localhost:8025


## 📦 Node.js por proyecto

Para usar Node dentro de los contenedores:

```bash
# Proyecto 1 (Node 16)
docker exec -it node_proyecto1 bash
cd proyecto1
npm install
npm run dev

# Proyecto 2 (Node 18)
docker exec -it node_proyecto2 bash
cd proyecto2
npm install
npm run dev
```

## 🛠 Tips Adicionales
* Puedes modificar los Dockerfiles para agregar más extensiones, herramientas o comandos útiles.
* Usa `docker-compose logs -f` para ver los logs en tiempo real.
* Crea múltiples proyectos fácilmente duplicando servicios en el `docker-compose.yml`.