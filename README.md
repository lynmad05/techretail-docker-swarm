# TechRetail - Despliegue con Docker Swarm

## Integrantes

* Ailyn Medina Mallqui
* Yamile Ochoa Marín

---

## 1. Descripción del proyecto

Este proyecto implementa una arquitectura de microservicios utilizando **Docker Swarm** para la empresa ficticia **TechRetail**, una plataforma de comercio electrónico que requiere alta disponibilidad, escalabilidad horizontal y balanceo de carga.

El sistema permite simular un entorno productivo distribuido, compuesto por múltiples nodos que ejecutan contenedores de forma orquestada.

---

## 2. Caso de estudio

TechRetail presentaba problemas de rendimiento debido al crecimiento de usuarios en campañas de alta demanda como “Cyber Days”, generando:

* Caídas del sistema en horas pico
* Tiempos de respuesta elevados
* Pérdidas económicas por inactividad
* Falta de escalabilidad

Para resolver esto, se implementa Docker Swarm como solución de orquestación de contenedores.

---

## 3. Arquitectura del sistema

El clúster está compuesto por:

* 1 nodo **Manager**
* 2 nodos **Worker**
* Red **overlay (techretail_net)** para comunicación interna

### Microservicios desplegados:

* **Frontend**: Nginx (interfaz web)
* **Backend**: Node.js (API REST)
* **Database**: MySQL (persistencia de datos)
* **Cache**: Redis (optimización de consultas)
* **Visualizer**: monitoreo del clúster Swarm

---

## 4. Tecnologías utilizadas

* Docker
* Docker Swarm
* Nginx
* Node.js
* MySQL
* Redis

---

## 5. Servicios del sistema

| Servicio   | Imagen         | Réplicas |
| ---------- | -------------- | -------- |
| Frontend   | nginx:alpine   | 3        |
| Backend    | node:18-alpine | 2        |
| Database   | mysql:8        | 1        |
| Cache      | redis:7-alpine | 1        |
| Visualizer | dockersamples  | 1        |

---

## 6. Funcionalidades implementadas

### 6.1 Orquestación con Docker Swarm

Se utiliza Swarm para administrar múltiples nodos y distribuir contenedores automáticamente.

### 6.2 Escalabilidad

* Frontend escalado a mínimo 3 réplicas
* Backend con 2 réplicas
* Escalado dinámico con `docker service scale`

### 6.3 Alta disponibilidad

Los servicios se reinician automáticamente en caso de fallos mediante `restart_policy`.

### 6.4 Seguridad

Se implementa:

* Docker Secrets para credenciales de base de datos

---

## 7. Comandos principales

### Inicializar Swarm

```bash
docker swarm init --advertise-addr <IP_MANAGER>
```

### Crear secret

```bash
echo "MiPasswordSegura123" | docker secret create db_password -
```

### Desplegar stack

```bash
docker stack deploy -c docker-compose.yml techretail
```

### Ver servicios

```bash
docker stack services techretail
```

### Ver nodos

```bash
docker node ls
```

### Escalar frontend

```bash
docker service scale techretail_frontend=5
```

---

## 8. Evidencias

Las evidencias del despliegue se encuentran organizadas en el repositorio:

* `/screenshots`: capturas del clúster, servicios y escalado
* `/docs`: informe técnico en PDF

---

## 9. Resultado esperado

El sistema demuestra:

* Alta disponibilidad de servicios
* Escalabilidad horizontal
* Balanceo de carga automático
* Gestión centralizada de contenedores

---

## 10. Conclusión

Docker Swarm permite la orquestación eficiente de contenedores en entornos distribuidos, mejorando la escalabilidad, disponibilidad y administración de servicios en aplicaciones modernas.

---

