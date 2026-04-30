# TechRetail - Docker Swarm

## Integrantes

- Ailyn
- Yamile

---

## Descripción

Este proyecto implementa un clúster Docker Swarm para la empresa TechRetail, desplegando una arquitectura de microservicios con frontend, backend, base de datos y cache.

---

## Servicios

| Servicio      | Tecnología              |
| ------------- | ----------------------- |
| Frontend      | Nginx                   |
| Backend       | Node.js                 |
| Base de datos | MySQL                   |
| Cache         | Redis                   |
| Visualizador  | Docker Swarm Visualizer |

---

## Tecnologías usadas

![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)
![Docker Swarm](https://img.shields.io/badge/Docker%20Swarm-2496ED?style=flat&logo=docker&logoColor=white)

- **Docker**
- **Docker Swarm**

---

## Instrucciones de uso

### 1. Inicializar Swarm

```bash
docker swarm init
```

### 2. Crear secret

```bash
echo "MiPasswordSegura123" | docker secret create db_password -
```

### 3. Desplegar el stack

```bash
docker stack deploy -c docker-compose.yml techretail
```

### 4. Ver servicios activos

```bash
docker stack services techretail
```

### 5. Escalar un servicio

```bash
docker service scale techretail_frontend=5
```

---

## Evidencias

Las capturas y video se encuentran en el repositorio.

---

## Conclusión

Docker Swarm permite escalar aplicaciones fácilmente y mejorar la disponibilidad de los servicios.
