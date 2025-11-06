# UD2. Memoria, espacio y rendimiento de disco

Comandos para la monitorización de la memoria, el uso del espacio en disco y el rendimiento de E/S (Entrada/Salida) de los discos.

---

### free

![Comando free](/ud2/img/free.png)

**Explicación:** El comando `free` muestra la cantidad de memoria **RAM** (física) y de intercambio (**swap**) libre y utilizada en el sistema.
* `free -h`: Es la opción más común. Muestra la salida en un formato **"legible para humanos"** (human-readable), usando Megabytes (M) o Gigabytes (G) en lugar de bytes.
* `free -c 3`: Repite el comando `free` un número determinado de veces (en este caso, 3 veces).
* `free -s 3`: Repite el comando `free` **cada 3 segundos** (seconds) de forma continua, hasta que se interrumpe (con Ctrl+C).

---

### df

![Comando df](/ud2/img/df.png)

**Explicación:** El comando `df` (Disk Free) se usa para **reportar el espacio libre y utilizado** de los sistemas de archivos (particiones o discos montados).
* `df -h`: Muestra la salida en formato **"legible para humanos"** (human-readable), indicando el espacio en G, M, K, etc.
* `df -hT`: Añade la columna "Tipo" (`-T`), que muestra el **tipo de sistema de archivos** (como `ext4`, `vfat`, `tmpfs`, etc.) para cada partición.

---

### du

![Comando du](/ud2/img/du.png)

**Explicación:** El comando `du` (Disk Usage) se utiliza para **estimar el espacio total que ocupan** archivos o directorios. A diferencia de `df`, que mira la partición completa, `du` calcula el tamaño de carpetas específicas.
* `sudo`: Se usa para tener permisos de administrador y poder leer el tamaño de todas las carpetas, incluso las que pertenecen a otros usuarios.
* `-h`: Muestra el tamaño total en formato **"legible para humanos"**.
* `-s`: (Summary) Muestra solo un **resumen total** para cada argumento (cada carpeta dentro de `/home/`), en lugar de listar el contenido de todas las subcarpetas.
* `/home/*`: Es la ruta. El asterisco (`*`) actúa como comodín para que `du` calcule el tamaño de cada elemento dentro de `/home` por separado (en este caso, las carpetas de los usuarios).

---

### iostat

![Comando iostat](/ud2/img/iostat.png)

**Explicación:** El comando `iostat` (Input/Output Statistics) monitoriza las **estadísticas de E/S (Entrada/Salida) de los dispositivos** de bloque (discos duros, SSDs). Es muy útil para detectar cuellos de botella en el rendimiento del disco.
* Muestra métricas clave como `rKB/s` (kilobytes leídos por segundo), `wKB/s` (kilobytes escritos por segundo), `await` (tiempo de espera) y `%util` (porcentaje de tiempo que el disco ha estado ocupado).
* En la captura, el comando se está ejecutando repetidamente (probablemente con un intervalo, ej. `iostat 2`), mostrando una nueva actualización de las estadísticas cada pocos segundos.

---

### atop

![Comando atop](/ud2/img/atop1.png)

**Explicación:** El comando `atop` es un monitor de rendimiento del sistema avanzado e interactivo (similar a `htop` o `top`).
* Su principal ventaja es que **muestra el uso de TODOS los recursos del sistema** en una sola pantalla: CPU (`CPU`), memoria (`MEM`), disco (`DSK`) y red (`NET`).
* Permite identificar rápidamente qué procesos están consumiendo no solo CPU o RAM, sino también qué procesos están realizando más operaciones de **lectura/escritura en disco** (columnas `RDDSK`/`WRDSK`) o enviando/recibiendo datos por la **red** (`RNET`/`SNET`).
* En la captura se puede ver la sección superior con el resumen del sistema y la sección inferior con el detalle por proceso.
