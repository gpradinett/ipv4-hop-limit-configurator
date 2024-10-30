# IPv4 Hop Limit Configurator

### Descripción

Este repositorio contiene un script que utiliza la utilidad de línea de comandos `netsh` para configurar el límite de saltos (TTL) predeterminado para paquetes IPv4 en sistemas operativos Windows. El TTL (Time To Live) define el número máximo de routers o puntos intermedios que un paquete puede atravesar antes de ser descartado.

### Motivación para el Uso del Script

Este script es especialmente útil para usuarios que desean compartir su conexión de datos móviles desde un dispositivo Android o iPhone hacia otros equipos, como laptops, cuando el proveedor de servicios de red limita el uso de datos gratuitos al dispositivo móvil. Al ajustar el valor del TTL en la configuración de red, el script permite que los paquetes de datos se transmitan sin problemas a dispositivos adicionales. Sin esta configuración, los dispositivos conectados a través de la conexión compartida pueden establecer conexión, pero no navegar debido a restricciones impuestas por el operador.

### ¿Qué Hace el Script?
El script ejecuta el siguiente comando para establecer el valor del límite de saltos predeterminado a 65:

Puedes verificar el valor actual del límite de saltos con el siguiente comando:
Copiar código
```shell
netsh int ipv4 show global
```
Salida
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
Salida
![Ejemplo de comando netsh int ipv4 set glob defaultcurhoplimit=65](https://github.com/gpradinett/ipv4-hop-limit-configurator/raw/main/image/netsh%20int%20ipv4%20set%20glob%20defaultcurhoplimit%3D65.png)

### ¿Cómo Usar el Script?
Clona este repositorio en tu máquina local usando el siguiente comando:
Copiar código
```shell
git clone https://github.com/gpradinett/ipv4-hop-limit-configurator.git
```

### Ejecuta el Script
Abre una ventana de línea de comandos con privilegios de administrador y navega a la carpeta del repositorio clonado. Luego, ejecuta el script en la línea de comandos:
Copiar código
```shell
netsh int ipv4 set glob defaultcurhoplimit=65
```
Nota: Asegúrate de ejecutar el comando en una ventana con permisos de administrador, ya que modificar la configuración de red requiere privilegios elevados.

### Requisitos
Sistema operativo Windows
Privilegios de administrador

### Notas
Cambiar el límite de saltos puede afectar la forma en que los paquetes son enrutados en la red. Asegúrate de entender las implicaciones antes de aplicar el cambio.



Contribuciones
Las contribuciones son bienvenidas. Si encuentras un problema o tienes sugerencias, por favor abre un issue o envía una solicitud de extracción (pull request).

Licencia
Este proyecto está licenciado bajo la Licencia MIT.
