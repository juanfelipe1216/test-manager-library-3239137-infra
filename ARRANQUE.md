# Entorno local — Manager Library

## Preparación inicial
Requiere Docker Desktop. Los seis forks deben ser carpetas hermanas
con sus nombres originales.

1. En infra copiar .env.example a .env y completar DB_PASSWORD.
2. En api/backend copiar .env.example a .env.
3. Completar ADMIN_USERNAME, ADMIN_PASSWORD y JWT_SECRET en el .env
   del backend. JWT_SECRET: al menos 32 caracteres aleatorios.
4. Desde infra ejecutar:

~~~bash
docker compose build api
docker compose run --rm --no-deps api composer install --no-interaction --no-scripts
docker compose run --rm --no-deps api php artisan key:generate
docker compose up -d --build
~~~

Los .env reales están ignorados. No guardar credenciales en documentos.

## Servicios
- React: http://localhost:5173
- API: http://localhost:8000/api/v1/health
- Presentación: http://localhost:8080
- PostgreSQL: red interna, nombre db.

El motor arranca vacío. El comando de la aplicación ejecuta después las
migraciones de api y provisiona al administrador desde entorno.
Infra no contiene DDL. API usa cuatro workers para probar concurrencia.
Esperar a que los logs muestren Server running.

~~~bash
docker compose ps
docker compose logs --tail=20 api
curl -i http://localhost:8000/api/v1/health
docker compose exec api php artisan test --compact
docker compose exec api php tests/smoke.php
~~~

## Detener sin borrar datos
docker compose down

Los datos permanecen en library_data. No usar down -v para una revisión
normal: elimina el volumen de datos.

## Semilla
Desde tool copiar .env.example a .env y completar las credenciales del
administrador. Ejecutar npm run seed. Ver README de tool para el reloj
controlado y sus límites.
