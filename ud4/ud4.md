# UD4. Puertos y Conexiones

Herramientas para inspeccionar las conexiones de red activas, los puertos abiertos y la información de los equipos en la red.

---

### ss

![Comando ss](ss.png)

**Explicación:** El comando `ss` (Socket Statistics) es una herramienta moderna y más rápida que `netstat` para investigar sockets (puntos de comunicación de red).
* `ss -plunt`: Es una combinación de opciones muy común:
    * `-p`: Muestra el **proceso** (programa) que está usando el socket.
    * `-l`: Muestra solo los sockets que están **"escuchando"** (`LISTEN`), es decir, esperando conexiones entrantes.
    * `-u`: Muestra sockets **UDP**.
    * `-n`: Muestra los puertos y direcciones en formato **numérico** (no resuelve nombres DNS).
    * `-t`: Muestra sockets **TCP**.
* `ss -ntp`: Muestra las conexiones **TCP** (`-t`) activas (no solo las que escuchan) en formato **numérico** (`-n`) y el **proceso** (`-p`) asociado.

---

### whois

![Comando whois](whois.png)

**Explicación:** El comando `whois` se utiliza para consultar bases de datos públicas y obtener **información de registro sobre un dominio o una dirección IP**.
* En la captura (parte superior), se usa `ss -tnp` para ver una conexión establecida con la IP `34.107.243.93`.
* A continuación, se usa `whois 34.107.243.93` para averiguar a quién pertenece esa IP.
* La salida de `whois` revela que la IP pertenece a **Google LLC** y es parte de la infraestructura de **Google Cloud**.

---

### arp

![Comando arp](arp.png)

**Explicación:** El comando `arp` se usa para ver y manipular la **caché ARP** (Address Resolution Protocol) del sistema. Esta caché es una tabla que **traduce direcciones IP (Capa 3) a direcciones MAC (Capa 2)** dentro de la red local.
* `arp -n`: Muestra la tabla ARP, usando direcciones IP numéricas (`-n`) en lugar de intentar resolver nombres de host.
* **DirecciónHW (MAC):** Si aparece `(incompleto)`, significa que el sistema preguntó por la MAC de esa IP pero no obtuvo respuesta. Si aparece una dirección (ej. `fc:34:97:b0:62:fa`), esa es la dirección física del dispositivo con esa IP.

---

### nmap (Ping Scan)

![Comando nmap ping scan](equipos-disponibles.png)
![Comando nmap ping scan 2](nmap.png)

**Explicación:** `nmap` (Network Mapper) es una potente herramienta para descubrir hosts y servicios en una red.
* `nmap -sn 172.26.1.0/24`: Este comando realiza un **"Ping Scan"** (`-sn`) sobre todo el rango de red `172.26.1.0/24`.
* `-sn` (Scan, No port): Le indica a `nmap` que **solo verifique qué hosts están "vivos"** (responden a ping) pero que **no realice un escaneo de puertos**. Es la forma más rápida de descubrir qué IPs están en uso en la red.
* La segunda imagen (`nmap.png`) muestra el mismo comando (`-sn`) pero dirigido a un solo host (`172.26.11.190`), confirmando que el host está activo (`Host is up`).

---

### nmap (Escaneo de Puertos)

![Comando nmap top ports](top-ports.png)

**Explicación:** Este es un uso más avanzado de `nmap` para **descubrir servicios** que se ejecutan en un host.
* `nmap --top-ports 100 -sV 172.26.10.99`:
    * `--top-ports 100`: Limita el escaneo a los **100 puertos más comunes** (en lugar de los 1000 por defecto), haciéndolo más rápido.
    * `-sV`: (Service Version) Intenta **detectar la versión del servicio** que se está ejecutando en los puertos abiertos. En la captura, detecta `Apache httpd 2.4.58` en los puertos 80 y 8081.
* `nmap ... 172.26.10.227`: En el segundo escaneo al host `.227`, `nmap` informa que "Host seems down" (parece caído) porque probablemente el host **bloquea las peticiones de ping (ICMP)**.
* `nmap ... -Pn ...`: (No se ve en el comando ejecutado, pero es la solución) Si un host bloquea pings, se debe usar la opción `-Pn` (No Ping) para forzar a `nmap` a escanear los puertos sin comprobar primero si el host está vivo.
