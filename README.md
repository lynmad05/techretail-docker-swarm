# TechRetail - Despliegue con Docker Swarm

## Integrantes

* Ailyn Medina Mallqui
* Yamile Ochoa Marín

---

## 1. Descripción del proyecto

Este proyecto implementa una arquitectura de microservicios utilizando **Docker Swarm** para la empresa ficticia **TechRetail**, una plataforma de comercio electrónico que requiere alta disponibilidad, escalabilidad horizontal y balanceo de carga.

El sistema simula un entorno productivo distribuido mediante múltiples nodos virtuales que ejecutan contenedores de forma orquestada.

---

## 2. Caso de estudio

TechRetail presentaba problemas de rendimiento durante campañas de alta demanda (como “Cyber Days”), generando:

* Caídas del sistema en horas pico
* Tiempos de respuesta elevados
* Pérdidas económicas por inactividad
* Falta de escalabilidad

Para solucionar estos problemas, se implementa **Docker Swarm** como herramienta de orquestación.

---

## 3. Arquitectura del sistema

La infraestructura fue implementada mediante **máquinas virtuales en VMware Workstation**, cada una con **Ubuntu Server 22.04 LTS**.

### 🔹 Nodos del clúster

* **1 nodo Manager (swarm-manager)**

  * Orquesta el clúster
  * Gestiona el estado del sistema
  * Distribuye tareas

* **2 nodos Worker (swarm-worker-1, swarm-worker-2)**

  * Ejecutan los contenedores asignados

### 🔹 Red

* Red overlay: `techretail_net`
* Permite comunicación entre servicios sin importar el nodo físico

---

## 4. Microservicios desplegados

| Servicio   | Tecnología        | Descripción               |
| ---------- | ----------------- | ------------------------- |
| Frontend   | Nginx             | Interfaz web              |
| Backend    | Node.js           | API REST                  |
| Database   | MySQL             | Persistencia de datos     |
| Cache      | Redis             | Optimización de consultas |
| Visualizer | Docker Visualizer | Monitoreo del clúster     |

---

## 5. Configuración del sistema

### Seguridad

* Uso de **Docker Secrets** para la contraseña de base de datos
* Protección de credenciales en `/run/secrets/`

### Configuración

* Uso de **Docker Config** para variables:

  * API_PORT
  * APP_NAME
  * ENV

---

## 6. Funcionalidades implementadas

### 🔹 Orquestación

Gestión de contenedores en múltiples nodos mediante Docker Swarm.

### 🔹 Escalabilidad

* Frontend: 3 réplicas (escalable)
* Backend: 2 réplicas
* Escalado dinámico con comandos Docker

### 🔹 Alta disponibilidad

* Reinicio automático de servicios ante fallos (`restart_policy`)

### 🔹 Distribución de carga

* Balanceo automático entre contenedores

---

## 7. Tecnologías utilizadas

* Docker
* Docker Swarm
* VMware Workstation
* Ubuntu Server 22.04
* Nginx
* Node.js
* MySQL
* Redis

---

## 8. Evidencias

Las evidencias del proyecto se encuentran organizadas de la siguiente manera:

- Carpeta `/informe`: contiene el informe técnico completo en PDF  
  - Capturas del despliegue  
  - Explicación detallada del proceso  
  - Enlace al video demostrativo  

> Nota: No se incluyen capturas ni videos directamente en el repositorio por organización y buenas prácticas.
> Se recomienda revisar el informe para una comprensión completa del despliegue.
---

## 10. Cómo ejecutar el proyecto

### 🔹 Requisitos

* Docker instalado
* Docker Swarm inicializado
* 3 nodos (1 manager y 2 workers)

### 🔹 Pasos

1. Clonar el repositorio:

```bash
git clone https://github.com/tu-repo/techretail.git
cd techretail
```

2. Crear el secret:

```bash
echo "password" | docker secret create db_password -
```

3. Crear el config:

```bash
docker config create app_config configs/app_config.env
```

4. Desplegar el stack:

```bash
docker stack deploy -c docker-compose.yml techretail
```

5. Verificar servicios:

```bash
docker stack services techretail
```

---

## 11. Resultados

El sistema demuestra:

* Alta disponibilidad de servicios
* Escalabilidad horizontal
* Balanceo de carga automático
* Gestión centralizada de contenedores

---

## 12. Conclusión

Docker Swarm permite implementar soluciones distribuidas de forma eficiente, facilitando la administración, escalabilidad y disponibilidad de aplicaciones modernas.

---