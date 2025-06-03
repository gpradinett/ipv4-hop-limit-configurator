# IPv4 Hop Limit Configurator

### Descripción

Este repositorio contiene un script que utiliza la utilidad de línea de comandos `netsh` para configurar el límite de saltos (TTL) predeterminado para paquetes IPv4 en sistemas operativos Windows. El TTL (Time To Live) define el número máximo de routers o puntos intermedios que un paquete puede atravesar antes de ser descartado.

### Motivación para el Uso del Script

Este script es especialmente útil para usuarios que desean compartir su conexión de datos móviles desde un dispositivo Android o iPhone hacia otros equipos, como laptops, cuando el proveedor de servicios de red limita el uso de datos gratuitos al dispositivo móvil. Al ajustar el valor del TTL en la configuración de red, el script permite que los paquetes de datos se transmitan sin problemas a dispositivos adicionales. Sin esta configuración, los dispositivos conectados a través de la conexión compartida pueden establecer conexión, pero no navegar debido a restricciones impuestas por el operador.
Puedes verificar el valor actual del límite de saltos con el siguiente comando:

Copiar código
```shell
netsh int ipv4 show global
```
![Output del comando netsh int ipv4 show global](https://github.com/gpradinett/ipv4-hop-limit-configurator/raw/main/image/netsh%20int%20ipv4%20show%20global.png)

Ahora configuraremos el limite de salto de 128 a 65 con el siguente comando 

Copiar código
```shell
netsh int ipv4 set glob defaultcurhoplimit=65
```
verificamos el cambio con:
```shell
netsh int ipv4 show global
```
![Ejemplo de comando netsh int ipv4 set glob defaultcurhoplimit=65](https://github.com/gpradinett/ipv4-hop-limit-configurator/raw/main/image/netsh%20int%20ipv4%20set%20glob%20defaultcurhoplimit%3D65.png)

Nota: Asegúrate de ejecutar el comando en una ventana con permisos de administrador, ya que modificar la configuración de red requiere privilegios elevados.

### Requisitos
Sistema operativo Windows
Privilegios de administrador

### Notas
Cambiar el límite de saltos puede afectar la forma en que los paquetes son enrutados en la red. Asegúrate de entender las implicaciones antes de aplicar el cambio.


```
C:\Users\gprad>netstat -nao | findstr ESTABLISHED
  TCP    192.168.18.33:49261    140.82.113.25:443      ESTABLISHED     7152
  TCP    192.168.18.33:49265    185.199.110.154:443    ESTABLISHED     7152
  TCP    192.168.18.33:49267    18.164.13.35:443       ESTABLISHED     7152
  TCP    192.168.18.33:49273    3.141.191.95:443       ESTABLISHED     7152
  TCP    192.168.18.33:49278    18.164.13.97:443       ESTABLISHED     7152
  TCP    192.168.18.33:49289    151.101.0.176:443      ESTABLISHED     7152
  TCP    192.168.18.33:49290    18.164.13.89:443       ESTABLISHED     7152
  TCP    192.168.18.33:49405    65.8.248.64:443        ESTABLISHED     7152
  TCP    192.168.18.33:50361    104.208.203.89:443     ESTABLISHED     4708
  TCP    192.168.18.33:65508    185.199.110.154:443    ESTABLISHED     7152
  TCP    192.168.18.33:65530    18.164.5.142:443       ESTABLISHED     7152
```

````
## Ver conexiones establecidas con `netstat`

El siguiente comando permite listar todas las conexiones de red activas en estado **ESTABLISHED** en un sistema Windows:

```bash
netstat -nao | findstr ESTABLISHED
````

### ¿Qué hace cada parte?

* `netstat`: Muestra estadísticas de red, conexiones activas, puertos en escucha, etc.
* `-n`: Muestra direcciones IP y números de puerto en formato numérico, sin intentar resolver nombres.
* `-a`: Muestra todas las conexiones y puertos en escucha.
* `-o`: Muestra el ID del proceso (PID) asociado con cada conexión.
* `| findstr ESTABLISHED`: Filtra solo las conexiones que están en estado **ESTABLISHED**, es decir, conexiones TCP que están activas actualmente.

### ¿Para qué sirve?

Este comando es útil para:

* Ver qué conexiones activas tiene tu sistema.
* Identificar posibles conexiones sospechosas o no autorizadas.
* Relacionar conexiones activas con procesos específicos usando el PID (puedes usar `tasklist` para saber qué proceso corresponde a un PID).

### Ejemplo de salida

```text
TCP    192.168.1.5:50352    93.184.216.34:443    ESTABLISHED     1234
```

Esto indica que el proceso con PID `1234` tiene una conexión establecida entre tu IP local y el servidor remoto en el puerto 443 (HTTPS).

### Ver el nombre del proceso desde el PID

Puedes usar el siguiente comando para ver a qué proceso corresponde un PID:

```bash
tasklist /FI "PID eq 1234"
```

Esto mostrará el nombre del programa que está usando esa conexión de red.

### (Opcional) Cerrar el proceso si es sospechoso

Si identificas un proceso sospechoso y deseas terminarlo, puedes usar:

```bash
taskkill /PID 1234 /F
```

> ⚠️ **Precaución:** Cerrar procesos críticos del sistema puede causar inestabilidad o pérdida de datos.

```

Este bloque es totalmente compatible con Markdown para GitHub, GitLab, VS Code, etc. Si quieres que lo exporte como archivo `.md`, solo dímelo.
```





Contribuciones
Las contribuciones son bienvenidas. Si encuentras un problema o tienes sugerencias, por favor abre un issue o envía una solicitud de extracción (pull request).

Licencia
Este proyecto está licenciado bajo la Licencia MIT.
