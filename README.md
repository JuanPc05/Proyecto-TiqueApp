# Proyecto-TiqueApp

Sistema de gestión contable para pequeños negocios: registro de productos, movimientos de ingresos/egresos y reportes diarios con apoyo de análisis de datos.

Proyecto integrador — Desarrollo de Software, semestre final.

## Stack

| Capa | Tecnología |
|---|---|
| Frontend | React + Vite |
| Backend | Spring Boot |
| Base de datos | MariaDB |
| Servicio de datos/reportes | Python (FastAPI) |
| Administración de BD | phpMyAdmin |
| Orquestación | Docker Compose |

## Estructura del repositorio

```
.
├── docker-compose.yml
├── .env.example
├── frontend/          # React + Vite
├── backend/           # Spring Boot (API principal, lógica de negocio)
├── data-service/      # Python FastAPI (reportes y análisis)
└── docs/              # Documentación del proyecto (arquitectura, MoSCoW, actas)
```

Cada carpeta de servicio tiene su propio `Dockerfile`. No se requiere instalar Java, Node, Python ni MariaDB de forma nativa en tu máquina — todo corre en contenedores.

## Requisitos previos

Solo necesitas **Docker** funcionando en tu sistema. No importa si es Ubuntu nativo o Windows con WSL2 — el comportamiento de los contenedores es idéntico en ambos casos.

- **Ubuntu:** [Docker Engine](https://docs.docker.com/engine/install/ubuntu/) + [Docker Compose plugin](https://docs.docker.com/compose/install/linux/).
- **Windows:** [Docker Desktop](https://www.docker.com/products/docker-desktop/) con backend WSL2 habilitado.
  - Importante: clona este repositorio **dentro del filesystem de tu distro WSL** (ej. `/home/tu-usuario/...`), no en `/mnt/c/Users/...`. Clonar desde el lado Windows del filesystem hace que Docker sea notablemente más lento porque cada acceso a archivo cruza la frontera Windows↔Linux.
  - Trabaja desde la terminal de WSL o desde VS Code con la extensión "Remote - WSL".

## Cómo levantar el proyecto

1. Clona el repositorio:
   ```bash
   git clone <url-del-repo>
   cd <nombre-carpeta>
   ```

2. Copia el archivo de variables de entorno de ejemplo y complétalo:
   ```bash
   cp .env.example .env
   ```
   Edita `.env` con tus propios valores locales (usuario/contraseña de la base de datos, etc.). **Este archivo nunca se sube al repositorio.**

3. Levanta todos los servicios:
   ```bash
   docker compose up --build
   ```
   La primera vez tarda más porque construye las imágenes. Las siguientes veces es más rápido (`docker compose up` sin `--build`, salvo que hayas cambiado dependencias).

4. Servicios disponibles una vez levantado:

   | Servicio | URL |
   |---|---|
   | Frontend | http://localhost:5173 |
   | Backend (API) | http://localhost:8080 |
   | Data service (docs OpenAPI) | http://localhost:8000/docs |
   | phpMyAdmin | http://localhost:8081 |

5. Para apagar todo:
   ```bash
   docker compose down
   ```
   Agrega `-v` (`docker compose down -v`) solo si además quieres borrar los datos de la base de datos (volumen persistente) — úsalo con cuidado.

## Flujo de trabajo en equipo

- **Ramas:** trabaja siempre en una rama a partir de `main` (ej. `feature/registro-movimientos`), nunca commits directos a `main`.
- **Antes de un Pull Request:** verifica que `docker compose up --build` funcione desde cero en tu máquina.
- **Variables de entorno:** si agregas una nueva variable en `.env`, agrégala también (sin el valor real) a `.env.example`, para que el resto del equipo sepa que existe.
- **Line endings:** el repo fuerza `LF` en todos los archivos vía `.gitattributes` — no necesitas configurar nada manualmente en Windows, pero si `git status` te muestra cambios masivos de línea sin haber tocado código, revisa tu configuración de `core.autocrlf`.

## Documentación adicional

- [`docs/arquitectura.md`](docs/arquitectura.md) — decisiones de arquitectura y justificación del stack.
- [`docs/moscow.md`](docs/moscow.md) — alcance del proyecto (Must/Should/Could/Won't).

## Equipo

- Juan Pablo Castillo Rueda — Scrum Master / [rol técnico]
- Andres Esteban Flórez Palacio — [rol técnico]
- Johan Sebastian Sepulveda Rojas — [rol técnico]