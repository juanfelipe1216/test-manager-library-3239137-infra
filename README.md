# test-manager-library-3239137-infra

> **Prueba técnica · Ficha ADSO 3239137**
> Horario: **viernes 23 de octubre de 2026, de 7:00 a. m. a 11:00 a. m.** (hora Colombia). Entrega a las **11:00 a. m.**

Este repositorio es la **infraestructura** de *Manager Library*: contenedores, red, volúmenes y el motor de base de datos vacío. **Empieza vacío a propósito**: se construye en el fork de cada aprendiz.

## Instrucciones

Cada aprendiz debe **crear el fork** de los seis repositorios del proyecto y **resolver el proyecto
con el spec planteado**.

1. Hacer fork, a su cuenta de GitHub, de cada repositorio de la tabla del final.
2. Leer el spec en [`test-manager-library-3239137-docs`](https://github.com/code-sena/test-manager-library-3239137-docs).
   Se entrega en dos versiones: `spec-python/` y `spec-.net/`.
3. Desarrollar en los forks.

## El reto se desarrolla con React y PHP (Laravel)

El spec está escrito para Python y para .NET, pero el reto **no** se hace en esos lenguajes:

| Capa | Tecnología del reto |
|---|---|
| Frontend | React |
| Backend | PHP con Laravel |

Lo que el spec define sobre el negocio —historias, criterios de aceptación, reglas, contrato de la
API, modelo de datos— se respeta. Lo que define sobre la tecnología se traduce a React y Laravel.

## La prueba no consiste en escribir el código

El propósito principal es ver la **capacidad de desempeño con SDD** (*Spec-Driven Development*,
desarrollo guiado por especificación): cómo se lee, se interpreta y se aplica una especificación
para llevarla a un stack distinto. El código es el medio, no el fin.

## Entrega

Cuenta lo que quede **subido a los forks antes de las 11:00 a. m.** Lo que llegue después no se revisa.
No hay prórroga: suban avances parciales con commits pequeños durante la prueba.

## Los seis repositorios

| Repositorio | Qué va ahí |
|---|---|
| [`test-manager-library-3239137-docs`](https://github.com/code-sena/test-manager-library-3239137-docs) | El spec: `spec-python/` y `spec-.net/` |
| [`test-manager-library-3239137-api`](https://github.com/code-sena/test-manager-library-3239137-api) | Backend en PHP (Laravel) |
| [`test-manager-library-3239137-app`](https://github.com/code-sena/test-manager-library-3239137-app) | Frontend en React |
| [`test-manager-library-3239137-page`](https://github.com/code-sena/test-manager-library-3239137-page) | Sitio público estático de presentación |
| [`test-manager-library-3239137-infra`](https://github.com/code-sena/test-manager-library-3239137-infra) | Contenedores, red, volúmenes y motor de base de datos vacío |
| [`test-manager-library-3239137-tool`](https://github.com/code-sena/test-manager-library-3239137-tool) | Utilidades: sembrador de datos de demostración |

## Entorno local implementado

Se utilizan PHP 8.4, Laravel 12 y PostgreSQL 16.

Los repositorios deben estar en carpetas hermanas.
El Dockerfile está en el repositorio api, dentro de backend.

### Preparación

- Docker Desktop debe estar funcionando.
- Copiar .env.example a .env en este repositorio y configurar la contraseña.
- El backend debe tener su archivo .env local y APP_KEY generada.
- El puerto 8000 debe estar disponible.

### Arranque

Desde este repositorio:

```bash
docker compose up -d --build
docker compose ps
```

### Verificación

```bash
curl -i http://localhost:8000/api/v1/health
```

Resultado comprobado: HTTP 200 y {"status":"ok"}.

### Estado actual

API y PostgreSQL funcionan mediante Compose.
Las dos migraciones del negocio están ejecutadas y verificadas.
Frontend integrado y sembrador ejecutado: 40 libros, 10 socios, 15 préstamos y tres vencidos.

Las tablas, restricciones y categorías se crearán desde las
migraciones del backend; infra no contiene scripts CREATE TABLE.
## Entrega integrada
Ver ARRANQUE.md para preparación, cuatro servicios, pruebas y semilla.
El arranque actual ejecuta migraciones y provisión desde la aplicación.
