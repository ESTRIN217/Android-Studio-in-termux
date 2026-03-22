# 🚀 Android Studio en Termux (ARM64)

Esta guía detalla cómo ejecutar Android Studio en un entorno Linux dentro de Termux, utilizando las librerías nativas de IntelliJ IDEA para habilitar la compatibilidad con la arquitectura **ARM64 (aarch64)**.

---

## 📋 Requisitos Previos

| Recurso | Requisito Mínimo |
| :--- | :--- |
| **RAM** | 6 GB (8 GB recomendados) |
| **Espacio** | 10 GB de almacenamiento libre |
| **SO** | Entorno Linux (PRoot/Chroot) como Ubuntu o Debian |
| **GUI** | Servidor X11 o VNC configurado |

---

## 🛠️ Paso 1: Descarga de Componentes

Necesitaremos ambos paquetes para realizar un "híbrido" funcional:

1.  **Android Studio (Linux 64-bit):** [Descargar aquí](https://developer.android.com/studio?hl=es-419)
2.  **IntelliJ IDEA Community (Linux ARM64):** [Descargar aquí](https://www.jetbrains.com/idea/download/?section=linux)

> [!IMPORTANT]
> Asegúrate de descargar la versión **Linux ARM64** de IntelliJ IDEA. Los archivos para Windows o Linux x86 no funcionarán en esta arquitectura.

---

## 📦 Paso 2: Extracción de Archivos

Puedes usar un gestor gráfico o la terminal dentro de tu entorno Linux:

```bash
# Extraer Android Studio
tar -xzvf android-studio-*-linux.tar.gz

# Extraer IntelliJ IDEA
tar -xzvf ideaIC-*-aarch64.tar.gz
```

### 🔧 Paso 3: Parche de Compatibilidad ARM64
Android Studio no incluye por defecto binarios nativos para ARM64 en Linux. Vamos a mover los de IntelliJ (que sí los tiene) hacia la carpeta de Android Studio.

Acción: Reemplaza el contenido de las siguientes carpetas en android-studio/lib/ con las carpetas correspondientes de idea/lib/:

android-studio/lib/jna/ ⬅️ (Reemplazar con) ⬅️ idea/lib/jna/

android-studio/lib/native/ ⬅️ (Reemplazar con) ⬅️ idea/lib/native/

android-studio/lib/pty4j/ ⬅️ (Reemplazar con) ⬅️ idea/lib/pty4j/

### ☕ Paso 4: Configuración del Java Runtime (JBR)
Android Studio viene con una versión de Java para x86_64 que no funcionará. Debemos vincular el JDK de tu sistema Linux en Termux.

Borra la carpeta interna:

```bash
rm -rf ~/android-studio/jbr
```
Instala un JDK compatible (si no lo tienes):

```bash
sudo apt update && sudo apt install openjdk-21-jdk
```
Crea el enlace simbólico:
Identifica la ruta de tu JDK (comúnmente en /usr/lib/jvm/) y ejecuta:

```bash
ln -s /usr/lib/jvm/java-21-openjdk-arm64 ~/android-studio/jbr
```
## 🚀 Paso 5: Ejecución
Para iniciar el entorno, entra a la carpeta bin de Android Studio y ejecuta el script de inicio:

```bash
cd ~/android-studio/bin
./studio.sh
```
## 📦 Anexo: SDK de Android
Para gestionar herramientas de compilación y plataformas, puedes consultar el repositorio de herramientas adaptadas:
👉 Herramientas de HomuHomu833 (GitHub)

### https://github.com/HomuHomu833

⚠️ Advertencia: El emulador de Android Studio no funcionará dentro de Termux debido a la falta de soporte de virtualización (KVM) en la mayoría de los kernels de Android. Deberás usar un dispositivo físico mediante ADB para probar tus apps.

