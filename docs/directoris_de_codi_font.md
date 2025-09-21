# 📥 Cómo descargar el código fuente de Android

Este documento proporciona un **resumen** de la página oficial de Android sobre cómo descargar el código fuente de AOSP.  
Es ideal para desarrolladores que deseen *contribuir* o personalizar el sistema operativo Android.

![Android Robot](https://www.gstatic.com/devrel-devsite/prod/v1cad304eab6ed28f3b327880a58163a09173752cefc8a71a602c8a68a1fc9d70/androidsource/images/lockup.png)

## 🔧 Requisitos previos

Antes de comenzar, asegúrate de tener instalados los siguientes programas:

- **Git**: sistema de control de versiones distribuido.
- **Repo**: herramienta de Google para gestionar múltiples repositorios de Git.
- **Python**: necesario para ejecutar Repo.
- **Herramientas de desarrollo**: como `make`, `curl`, `gcc`, entre otras.

## 🛠️ Pasos para descargar el código fuente

1. **Crea y navega a un directorio de trabajo**

   ```bash
   mkdir WORKING_DIRECTORY
   cd WORKING_DIRECTORY
   ```

2. **Inicializa el cliente Repo**

   ```bash
   repo init --partial-clone --no-use-superproject -b android-latest-release -u https://android.googlesource.com/platform/manifest
   ```

   > **Nota:** Este comando configura Repo para usar la rama `android-latest-release`.

3. **Sincroniza el repositorio**

   ```bash
   repo sync -c -j8
   ```

   > **Resaltado:** Este proceso puede tardar más de una hora dependiendo de tu conexión a Internet.

## 📦 Descarga de binarios propietarios

Para ejecutar AOSP en hardware real, necesitarás binarios específicos del dispositivo.  
Puedes obtenerlos desde el [sitio oficial de binarios](https://android.googlesource.com/platform/manifest/+/refs/heads/android-latest-release).

> Una vez descargados, extrae los archivos y ejecuta el script incluido desde el directorio raíz del código fuente.

## 🧪 Verificación del código

Si deseas verificar la autenticidad del código fuente, utiliza claves PGP para confirmar que proviene de una fuente oficial.  
Consulta la documentación oficial para más detalles sobre cómo realizar esta verificación.

---

Para más información y detalles, visita la página oficial de Android:

[https://source.android.com/docs/setup/download?hl=es-419](https://source.android.com/docs/setup/download?hl=es-419)