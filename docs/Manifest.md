# 📘 Descripción general del manifiesto de la app

El archivo `AndroidManifest.xml` es esencial en cualquier proyecto de aplicación Android. Se encuentra en la raíz del conjunto de orígenes del proyecto y proporciona información crucial tanto para las herramientas de compilación de Android como para el sistema operativo y Google Play.

## ¿Qué es el archivo de manifiesto?

*_Este archivo describe información esencial sobre tu app, incluyendo:_*

- El nombre del paquete de la aplicación.
- Las actividades, servicios, receptores de difusión y proveedores de contenido que componen la aplicación.
- Los permisos que la aplicación requiere.
- Las características de hardware y software que la aplicación necesita.
- La configuración de la aplicación, como el ícono, la etiqueta y el tema.

## Componentes del archivo de manifiesto

*_El archivo `AndroidManifest.xml` debe declarar los siguientes componentes:_*

1. **`<manifest>`**: Elemento raíz que contiene todos los demás elementos.
2. **`<application>`**: Define la configuración global de la aplicación.
3. **`<activity>`**: Declara una actividad que representa una pantalla de la aplicación.
4. **`<service>`**: Define un servicio que realiza operaciones en segundo plano.
5. **`<receiver>`**: Declara un receptor de difusión que escucha eventos del sistema o de otras aplicaciones.
6. **`<provider>`**: Define un proveedor de contenido que gestiona el acceso a datos compartidos.

## Permisos y características

*_El archivo de manifiesto también se utiliza para declarar:_*

- **Permisos**: Especifica los permisos que la aplicación necesita para acceder a recursos protegidos, como la cámara o el acceso a Internet.
- **Características**: Define las características de hardware y software que la aplicación requiere, como la cámara o la conectividad Bluetooth.

## Ejemplo de archivo AndroidManifest.xml

![Ejemplo de archivo AndroidManifest.xml](https://www.researchgate.net/profile/Kun-Sun-2/publication/272910798/figure/fig4/AS:669113618091520@1536631456719/Example-AndroidManifestxml-from-which-the-app-attributes-are-extracted.png)

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.myapp">
    <application
        android:label="My App"
        android:icon="@drawable/ic_launcher">
        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>
</manifest>
```

## Recomendaciones

- *Organización*: Mantén el archivo `AndroidManifest.xml` bien estructurado y organizado para facilitar su mantenimiento.
- *Declaración de componentes*: Asegúrate de declarar todos los componentes necesarios para el correcto funcionamiento de la aplicación.
- *Permisos*: Solicita solo los permisos que realmente necesita la aplicación para evitar problemas de privacidad y seguridad.

Para más detalles, puedes consultar la [página oficial de Android sobre el manifiesto de la app](https://developer.android.com/guide/topics/manifest/manifest-intro?hl=es-419).

[Enlace a la pagina](https://developer.android.com/guide/topics/manifest/manifest-intro?hl=es-419)