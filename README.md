# Portracker en Docker | Rastreador de torrents autoalojado

Portracker es un rastreador de torrents ligero y autoalojado que puedes desplegar fácilmente en Docker. Ideal para crear tu propio tracker privado o gestionar torrents de forma interna en tu red.

📦 **Servicios incluidos**
- Portracker (interfaz web y backend)
- Volumen persistente para configuración y datos

---

⚙️ **docker-compose.yml**
```yaml
services:
  portracker:
    image: mostafawahied/portracker:latest
    container_name: portracker
    restart: unless-stopped
    ports:
      - "2710:2710"         # Puerto del tracker
      - "8081:8081"         # Interfaz web
    environment:
      - TZ=Europe/Madrid
      - NODE_ENV=production
    volumes:
      - ./data:/app/data
      - ./config:/app/config
```

---

▶️ **Instrucciones de uso**

1. **Clonar o crear el archivo `docker-compose.yml`**  
   Guarda el contenido anterior en una carpeta, por ejemplo `/docker/portracker`.

2. **Levantar el servicio**
   ```bash
   docker compose up -d
   ```

3. **Acceder al panel web**  
   Abre tu navegador y entra a:  
   👉 `http://localhost:8081`  
   (O `http://IP_DEL_SERVIDOR:8081` desde tu LAN)

4. **Configurar el tracker**  
   Portracker usa el puerto `2710` como endpoint del tracker:  
   ```
   http://IP_DEL_SERVIDOR:2710/announce
   ```
   Añade esa URL en tus archivos `.torrent` o clientes BitTorrent.

---

🧹 **Comandos útiles**
- Ver logs del contenedor:
  ```bash
  docker logs -f portracker
  ```
- Reiniciar el servicio:
  ```bash
  docker compose restart portracker
  ```
- Detener y eliminar:
  ```bash
  docker compose down
  ```

---

🧱 **Volúmenes y persistencia**
Los datos de Portracker se guardan en `./data` y `./config`, permitiendo conservar usuarios, configuraciones y estadísticas incluso tras reiniciar los contenedores.
