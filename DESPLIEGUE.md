# DESPLIEGUE — Evidencias y respuestas

Este documento recopila todas las evidencias y respuestas de la practica.

---

## Parte 1 — Evidencias minimas

### Fase 1: Instalacion y configuracion

1) Servicio Nginx activo
- Que demuestra:![Evidencias Docker](evidencias/evidencias-docker.png)
- Comando: docker-compose ps 
- Evidencia: captura de `docker compose ps` (desde fuera) o `service nginx status` (desde dentro del contenedor) mostrando el servicio activo. Nota: `systemctl` no suele funcionar dentro de Docker.

2) Configuracion cargada
- Que demuestra: ![Evidencias configuracion](evidencias/evidencias-configuracion_nginx.png)
- Comando:
  - docker exec 2526-u2-4-2serweb-agsergio04-nginx-1 ls -l /etc/nginx/conf.d/
  - docker exec 2526-u2-4-2serweb-agsergio04-nginx-1 cat /etc/nginx/conf.d/default.conf
- Evidencia: captura listando el directorio de configuracion dentro del contenedor (ej: `ls -l /etc/nginx/conf.d/` o `sites-enabled` segun la imagen usada) donde se vea tu archivo `.conf`.


3) Resolucion de nombres
- Que demuestra:![Evidencias Resolucion Nombres](evidencias/evidencias-web-con-nombre.png)
- Evidencia: captura del navegador con la barra de direcciones mostrando `http://nombre_web` (no la IP) y la pagina cargada.


4) Contenido Web
- Que demuestra:
![Evidencias Resolucion Nombres](evidencias/evidencias-web-con-nombre.png)
![Evidencias Reloj](evidencias/evidencias-web-con-nombre-reloj.png)
- Evidencia: la misma captura anterior, pero debe verse claramente el diseno de la web importada de Cloud Academy.


### Fase 2: Transferencia SFTP (Filezilla)

5) Conexion SFTP exitosa
- Que demuestra:![Conexion FilleZilla](evidencias/evidencia-conexion-exitosa-FilleZilla.png)
- Evidencia: captura de Filezilla mostrando en el panel de registro "Status: Connected to..." y en el panel derecho el listado de carpetas remoto. Nota: en Docker la ruta suele ser `/home/usuario/upload`, no `/var/www`.


6) Permisos de escritura
- Que demuestra:![](evidencias/evidencia-permiso-de-escritura.png)
- Evidencia: captura de Filezilla mostrando la transferencia completada o los archivos ya presentes en el servidor remoto.


### Fase 3: Infraestructura Docker

7) Contenedores activos
- Que demuestra:
- Comando:
- Evidencia: captura de `docker compose ps` donde se vean los dos servicios con estado Up y los puertos `0.0.0.0:8080->80/tcp` y `0.0.0.0:2222->22/tcp`.


8) Persistencia (Volumen compartido)
- Que demuestra:
- Evidencia: evidencia cruzada (Filezilla + navegador) demostrando que lo subido al SFTP se ve en la web (por ejemplo `localhost:8080`).


9) Despliegue multi-sitio
- Que demuestra:
- Evidencia:  captura del navegador en `http://localhost:8080/reloj` mostrando el reloj funcionando.


### Fase 4: Seguridad HTTPS

10) Cifrado SSL
- Que demuestra:
- Evidencia: captura del navegador accediendo por `https://...` mostrando el candado (o alerta de certificado autofirmado) y el puerto configurado (ej. `8443`).


11) Redireccion forzada
- Que demuestra:
- Evidencia:  captura de la pestaña Network (DevTools) mostrando `301 Moved Permanently` al intentar entrar por HTTP.


---

## Parte 2 — Evaluacion RA2 (a–j)

### a) Parametros de administracion
- Respuesta:
- Evidencias:
  - evidencias/a-01-grep-nginxconf.png
  - evidencias/a-02-nginx-t.png
  - evidencias/a-03-reload.png

### b) Ampliacion de funcionalidad + modulo investigado
- Opcion elegida (B1 o B2):
- Respuesta:
- Evidencias (B1 o B2):
  - evidencias/b1-01-gzipconf.png
  - evidencias/b1-02-compose-volume-gzip.png
  - evidencias/b1-03-nginx-t.png
  - evidencias/b1-04-curl-gzip.png
  - evidencias/b2-01-defaultconf-headers.png
  - evidencias/b2-02-nginx-t.png
  - evidencias/b2-03-curl-https-headers.png

#### Modulo investigado: <NOMBRE>
- Para que sirve:
- Como se instala/carga:
- Fuente(s):

### c) Sitios virtuales / multi-sitio
- Respuesta:
- Evidencias:
  - evidencias/c-01-root.png
  - evidencias/c-02-reloj.png
  - evidencias/c-03-defaultconf-inside.png

### d) Autenticacion y control de acceso
- Respuesta:
- Evidencias:
  - evidencias/d-01-admin-html.png
  - evidencias/d-02-defaultconf-auth.png
  - evidencias/d-03-curl-401.png
  - evidencias/d-04-curl-200.png

### e) Certificados digitales
- Respuesta:
- Evidencias:
  - evidencias/e-01-ls-certs.png
  - evidencias/e-02-compose-certs.png
  - evidencias/e-03-defaultconf-ssl.png

### f) Comunicaciones seguras
- Respuesta:
- Evidencias:
  - evidencias/f-01-https.png
  - evidencias/f-02-301-network.png

### g) Documentacion
- Respuesta:
- Evidencias: enlaces a todas las capturas

### h) Ajustes para implantacion de apps
- Respuesta:
- Evidencias:
  - evidencias/h-01-root.png
  - evidencias/h-02-reloj.png

### i) Virtualizacion en despliegue
- Respuesta:
- Evidencias:
  - evidencias/i-01-compose-ps.png

### j) Logs: monitorizacion y analisis
- Respuesta:
- Evidencias:
  - evidencias/j-01-logs-follow.png
  - evidencias/j-02-metricas.png

---

## Checklist final

### Parte 1
- [ ] 1) Servicio Nginx activo
- [ ] 2) Configuracion cargada
- [ ] 3) Resolucion de nombres
- [ ] 4) Contenido Web (Cloud Academy)
- [ ] 5) Conexion SFTP exitosa
- [ ] 6) Permisos de escritura
- [ ] 7) Contenedores activos
- [ ] 8) Persistencia (Volumen compartido)
- [ ] 9) Despliegue multi-sitio (/reloj)
- [ ] 10) Cifrado SSL
- [ ] 11) Redireccion forzada (301)

### Parte 2 (RA2)
- [ ] a) Parametros de administracion
- [ ] b) Ampliacion de funcionalidad + modulo investigado
- [ ] c) Sitios virtuales / multi-sitio
- [ ] d) Autenticacion y control de acceso
- [ ] e) Certificados digitales
- [ ] f) Comunicaciones seguras
- [ ] g) Documentacion
- [ ] h) Ajustes para implantacion de apps
- [ ] i) Virtualizacion en despliegue
- [ ] j) Logs: monitorizacion y analisis
