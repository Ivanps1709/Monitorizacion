# UD3. Tráfico de red

Comandos y herramientas para la monitorización del tráfico y el uso del ancho de banda en la red.

---

### tcpdump

![Comando tcpdump](/ud3/img/tcpdump.png)

**Explicación:** El comando `tcpdump` es un **analizador de paquetes** (o "sniffer") para la línea de comandos. Es una herramienta de bajo nivel que permite capturar e inspeccionar el tráfico de red en detalle.
* En la captura, `sudo tcpdump` está imprimiendo en la terminal una descripción de cada paquete que pasa por la interfaz de red.
* Muestra la hora, el protocolo (TCP, UDP, etc.), las IPs y puertos de origen/destino, y los "flags" de la conexión (como `[S]` para SYN, `[.]` para ACK).
* Requiere `sudo` (permisos de administrador) para poder "escuchar" la tarjeta de red.

---

### tcptrack

![Comando tcptrack](/ud3/img/tcptrack.png)

**Explicación:** `tcptrack` es un monitor de conexiones TCP en tiempo real, similar a como `top` monitoriza los procesos.
* Muestra una lista ordenada de todas las conexiones TCP activas en ese momento.
* Para cada conexión, indica el **Cliente** (origen) y el **Servidor** (destino), el **Estado** de la conexión (ej. `ESTABLISHED`, `CLOSED`), el tiempo de inactividad (`Idle`) y la **velocidad** (`Speed`) de transferencia actual.

---

### iptraf-ng

![Comando iptraf-ng](/ud3/img/iptraf.png)

**Explicación:** `iptraf-ng` (o `iptraf`) es un monitor de red interactivo basado en ncurses (interfaz de texto). Ofrece un desglose estadístico del tráfico.
* En la captura se pueden ver dos paneles principales:
    1.  **TCP Connections**: Lista las conexiones TCP activas, mostrando puertos de origen/destino, paquetes y bytes transferidos.
    2.  **UDP Packets**: Muestra los paquetes UDP capturados, lo cual es útil para protocolos como DNS (puerto 53), visible en la imagen.

---

### bmon

![Comando bmon](/ud3/img/bmon.png)

**Explicación:** `bmon` (Bandwidth Monitor) es una utilidad sencilla para monitorizar el ancho de banda de la red **en tiempo real y de forma gráfica** en la terminal.
* **Panel Superior**: Muestra una lista de las interfaces de red del sistema (como `enp1s0f1`, `docker0`, etc.).
* **Columnas `RX bps` y `TX bps`**: Indican la velocidad de **Recepción (RX)** y **Transmisión (TX)** en bits por segundo.
* **Panel Inferior**: Muestra un gráfico histórico del tráfico (en la captura, la línea verde es RX y la roja es TX).
* *(Nota: La ventana de la derecha con `ping` solo se está usando para generar tráfico y así poder verlo en `bmon`)*.
