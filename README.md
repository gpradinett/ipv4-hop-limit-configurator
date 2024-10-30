# IPv4 Hop Limit Configurator

## Descripción

Este repositorio contiene un script que utiliza la utilidad de línea de comandos `netsh` para configurar el límite de saltos (TTL) predeterminado para paquetes IPv4 en sistemas operativos Windows. El límite de saltos, conocido como TTL (Time To Live) en IPv4, define el número máximo de routers o puntos intermedios que un paquete puede atravesar antes de ser descartado.

### ¿Qué Hace el Script?
El script ejecuta el siguiente comando para establecer el valor del límite de saltos predeterminado a 65:
Copiar código
```shell
netsh int ipv4 set glob defaultcurhoplimit=65
```
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

Puedes verificar el valor actual del límite de saltos con el siguiente comando:
Copiar código
```shell
netsh int ipv4 show global
```
![Texto alternativo de la imagen](ruta/a/tu/imagen.png](https://github.com/gpradinett/ipv4-hop-limit-configurator/blob/main/image/netsh%20int%20ipv4%20show%20global.png))


Contribuciones
Las contribuciones son bienvenidas. Si encuentras un problema o tienes sugerencias, por favor abre un issue o envía una solicitud de extracción (pull request).

Licencia
Este proyecto está licenciado bajo la Licencia MIT.
