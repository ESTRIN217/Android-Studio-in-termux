# Guía de Instalación: Android Studio en Termux (ARM64)
Esta guía detalla cómo ejecutar Android Studio en un entorno Linux dentro de Termux, utilizando las librerías nativas de IntelliJ IDEA para compatibilidad con arquitectura ARM64.

## 📋 Requisitos Previos
Hardware: Mínimo 6 GB de RAM (8 GB recomendados).

Almacenamiento: 10 GB de espacio libre.

Software: Un entorno Linux instalado en Termux (PRoot o Chroot) como Ubuntu o Debian, con un servidor X11 o VNC configurado para la interfaz gráfica.

## 🛠️ Paso 1: Descarga de Componentes
Necesitaremos ambos paquetes para realizar un "híbrido" funcional.

Android Studio (Linux de 64 bits): Descargar aquí

IntelliJ IDEA Community (Linux ARM64): Descargar aquí

Nota crítica: Asegúrate de descargar la versión Linux ARM64 de IntelliJ, no la de Windows.

## 📦 Paso 2: Extracción de Archivos
Puedes usar la terminal o un gestor de archivos gráfico (File Roller). En terminal, usa:

Bash
### Extraer Android Studio
tar -xzvf android-studio-*-linux.tar.gz

### Extraer IntelliJ IDEA
tar -xzvf ideaIC-*-aarch64.tar.gz

### 🔧 Paso 3: Parche de Compatibilidad ARM64
Android Studio no incluye por defecto binarios nativos para ARM64 en Linux. Vamos a mover los de IntelliJ (que sí los tiene) hacia la carpeta de Android Studio.

Acción: Reemplaza el contenido de las siguientes carpetas en android-studio/lib/ con las carpetas correspondientes de idea/lib/:

android-studio/lib/jna/ ⬅️ (Reemplazar con) ⬅️ idea/lib/jna/

android-studio/lib/native/ ⬅️ (Reemplazar con) ⬅️ idea/lib/native/

android-studio/lib/pty4j/ ⬅️ (Reemplazar con) ⬅️ idea/lib/pty4j/

### ☕ Paso 4: Configuración del Java Runtime (JBR)
Android Studio viene con una versión de Java para x86_64 que no funcionará. Debemos vincular el JDK de tu sistema Linux en Termux.

Borra la carpeta interna:

Bash
rm -rf ~/android-studio/jbr

Instala un JDK compatible (si no lo tienes):

Bash
sudo apt update && sudo apt install openjdk-21-jdk

Crea el enlace simbólico:
Identifica la ruta de tu JDK (comúnmente en /usr/lib/jvm/) y ejecuta:

Bash
ln -s /usr/lib/jvm/java-21-openjdk-arm64 ~/android-studio/jbr
## 🚀 Paso 5: Ejecución
Para iniciar el entorno, entra a la carpeta bin de Android Studio y ejecuta el script de inicio:

Bash
cd ~/android-studio/bin
./studio.sh
## 📦 Anexo: SDK de Android
Para gestionar herramientas de compilación y plataformas, puedes consultar el repositorio de herramientas adaptadas:
👉 Herramientas de HomuHomu833 (GitHub)

### https://github.com/HomuHomu833

⚠️ Advertencia: El emulador de Android Studio no funcionará dentro de Termux debido a la falta de soporte de virtualización (KVM) en la mayoría de los kernels de Android. Deberás usar un dispositivo físico mediante ADB para probar tus apps.
