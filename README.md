# Interfaz REACT para TEO

## Proyecto original

Ángel Gilabert de la Encina, Desarrollo de una interfaz web en React y ROS 2 para el robot humanoide TEO, Trabajo Fin de Grado, Universidad Carlos III de Madrid, 2025. https://github.com/angelGilabert/TFG_Interfaz-ROS2-REACT-para-TEO

## Pasos a seguir

### Comandos a ejecutar antes de iniciar:

Para  poder usar las funcionalidades básicas de la aplicación, se deberá ejecutar:

1.- Inicialzar el servidor de yarp
```bash
yarp server --write
```

2.- Iniciar gazebo con el mundo de teo.fixed
```bash
# Sustituya la URL por la correspondiente en su dispositivo
YARP_COLORED_OUTPUT=1 gazebo /home/angel/repos/teo-gazebo-models/worlds/teo_fixed.world
```

3.- Lanzar servidor rosbridge que conecta ros2 con react mediante Websockets.
```bash
ros2 launch rosbridge_server  rosbridge_websocket_launch.xml
```

4.- Arrancar la aplicación
```bash
# En la carpeta del proyecto
npm run dev
```

### Control de las articulaciones de la cabeza mediante el móvil.

Es necesario tener un servidor Socket.IO corriendo para permitir la transmisión de mensajes desde el móvil hacia nuestra aplicación.

Para iniciar el servidor:
```bash
# En la carpeta del proyecto
node server.js
```

Cabe destacar que la mayoría de los sensores de un móvil están capados para no funcionar en conexiones no seguras (como HTTP). Como se quiere acceder al giroscopio, se deberá tener una conexión segura, para ello:
1.- En el móvil irse a **Opciones de Desarrollador** y activar la opción de **Depuración por USB**
2.- Conectar mediante un cable el móvil al ordenador.
3.- Mediante la herramienta adb hacer que el movil detecte el puerto 3002 del ordenador como suyo (localhost)
```bash
# Instalar adb (Ubuntu)
sudo apt install adb

# Comprobar que tu movil es reconocido como un dispositivo
adb devices

# Redirige conexiones a puerto 3002 del móvil al puerto 3002 del ordenador (donde se ejecuta el servidor)
adb reverse tcp:3002 tcp:3002
```
En la ventana de la cabeza habrá un QR que al escanearlo se obtendrá la URL que al introducirla provocará que el servidor envie al móvil los archivos estáticos.

Cabe destacar que las pruebas han sido realizadas con un **móvil Android**, para Iphones se deberá usar una alternativa a ADB.

### Visualización de cámaras.

Para visualizar las cámaras del robot se usará el paquete ros_web_server
```bash
# Instalación en Ubuntu
sudo apt-get install ros-humble-web-video-server

# Ejecución servidor
ros2 run web_video_server web_video_server
```

## Cómo citar

Bartek Łukawski, Mercedes Rebollo, Ángel Gilabert, Juan G. Victores, Carlos Balaguer, and Alberto Jardón. YARP Cartesian controller layers over ROS 2 for teleoperation and web applications. In *XLVI Jornadas de Automática*. Universidade da Coruña, 2025. DOI: [10.17979/ja-cea.2025.46.12252](https://doi.org/10.17979/ja-cea.2025.46.12252)

```bibtex
@inproceedings{lukawski2025jjaa,
    author    = {{\L}ukawski, Bartek and Mercedes, Rebollo and Gilabert, Ángel and Victores, Juan G. and Balaguer, Carlos and Jardón, Alberto},
    title     = {{YARP} {Cartesian} controller layers over {ROS} 2 for teleoperation and web applications},
    booktitle = {XLVI Jornadas de Automática},
    year      = {2025},
    publisher = {Universidade da Coruña},
    doi       = {10.17979/ja-cea.2025.46.12252},
}
```
