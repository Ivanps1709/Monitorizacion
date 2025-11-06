# UD1. Procesos

A continuación se muestran capturas de pantalla de los comandos más comunes para la monitorización de procesos en Linux.

---

### ps au

![ps au](ud1/img/ps1.png)

**Explicación:** El comando `ps au` se utiliza para ver los procesos en ejecución.
* `a`: Muestra los procesos de **todos los usuarios**, no solo los del usuario actual.
* `u`: Muestra un formato **"orientado al usuario"**, que incluye detalles como el propietario del proceso (USER), el PID, el %CPU, el %MEM, y el comando que lo inició (COMMAND).

---

### ps aux

![ps aux](ud1/img/ps2.png)

**Explicación:** El comando `ps aux` es una versión más completa que `ps au`.
* `a`: Muestra procesos de todos los usuarios.
* `u`: Formato orientado al usuario.
* `x`: Incluye procesos que **no están asociados a ninguna terminal** (tty), como los servicios del sistema o demonios que corren en segundo plano.

---

### ps -u [usuario]

![ps -u alumno](ud1/img/ps3.png)

**Explicación:** El comando `ps -u alumno` filtra la lista de procesos para mostrar únicamente aquellos que pertenecen al **usuario especificado**, en este caso, "alumno".

---

### ps (formato personalizado y ordenado)

![ps sort](ud1/img/ejercicio1.png)

**Explicación:** Este es un comando más avanzado para filtrar procesos y ordenarlos.
* `ps -eo pid,user,comm,%cpu`: Muestra **todos los procesos** (`-e`) pero solo con las columnas que especificamos (`-o`): PID, usuario, nombre del comando y porcentaje de CPU.
* `--sort=-%cpu`: **Ordena** la lista completa de procesos según la columna %CPU. El signo `-` indica que el orden es **descendente** (de mayor a menor consumo).
* `| head -n 6`: Envía el resultado ordenado al comando `head`, que se encarga de mostrar solo las **primeras 6 líneas** (la cabecera y los 5 procesos que más CPU están consumiendo).

---

### top

![top](ud1/img/top1.png)

**Explicación:** El comando `top` inicia un monitor de sistema **interactivo y en tiempo real**. A diferencia de `ps` (que es una foto fija), `top` muestra una vista que se actualiza constantemente de los procesos y el estado general del sistema (carga media, uso de CPU, memoria RAM y SWAP). Por defecto, ordena los procesos por el porcentaje de uso de CPU (%CPU).

---

### top (modo batch)

![top batch mode](ud1/img/top2.png)

**Explicación:** Este comando ejecuta `top` de una forma no interactiva, ideal para guardar informes.
* `-b`: (Batch mode) Ejecuta `top` en **"modo batch"**, para que su salida se pueda redirigir a un archivo en lugar de mostrarse interactivamente.
* `-n 3`: Especifica el **número de "iteraciones"** o veces que `top` debe actualizarse antes de salir. En este caso, tomará 3 instantáneas.
* `> top.info`: **Redirige la salida** del comando (las 3 instantáneas) y la guarda en un archivo llamado `top.info`.

---

### htop

![htop](ud1/img/htop.png)

**Explicación:** El comando `htop` es un monitor de procesos interactivo, considerado una **versión mejorada de `top`**. Ofrece una interfaz más visual y amigable:
* Muestra el uso de cada **núcleo de la CPU** y el uso de memoria/swap con barras gráficas.
* Usa **colores** para resaltar prioridades y estados.
* Permite **desplazarse (scroll)** vertical y horizontalmente por la lista de procesos.
* Facilita la gestión de procesos mediante **teclas de función** (ej. F9 para "matar" un proceso, F6 para ordenar).
