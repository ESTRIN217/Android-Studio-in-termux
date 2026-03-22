## 🛠️ Solución de Problemas Comunes

### 1. Error de "Permission Denied" al ejecutar `studio.sh`
Si al intentar iniciar Android Studio recibes un error de permisos, otorga permisos de ejecución a la carpeta `bin`:
```bash
chmod +x ~/android-studio/bin/*.sh
```
### 2. Pantalla en blanco o parpadeo (Problemas de Renderizado)
Si la interfaz no se ve correctamente en tu servidor VNC/X11, prueba desactivando la aceleración de hardware para Java agregando esto al final de tu archivo ~/.bashrc:

```bash
export _JAVA_OPTIONS="-Dsun.java2d.xrender=false"
```
### ⚡ Optimización de Memoria (RAM)
Si tienes solo 6GB de RAM, Android Studio puede cerrarse inesperadamente. Puedes limitar el consumo de memoria editando el archivo de opciones:

Ve a android-studio/bin/

Abre studio64.vmoptions (o studio.vmoptions) con un editor de texto.

Cambia los valores -Xms y -Xmx:
```
-Xms512m
-Xmx2048m  # Limita el uso a 2GB para dejar espacio al sistema
```
