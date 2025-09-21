# Writing Build Scripts


## 1. Anatomía de un script de construcción

- Los scripts de Gradle se escriben en **Groovy DSL** (`*.gradle`) o **Kotlin DSL** (`*.gradle.kts`)
- El script puede configurar objetos de tipo *Settings*, *Project* y (también) *Gradle* (aunque lo de *Gradle* no entra en el nivel intermedio).  
- Se compone de dos tipos principales de elementos:  
  1. **Statements**: expresiones de nivel superior que se ejecutan inmediatamente (fase de inicialización o configuración).   
  2. **Blocks** (bloques): se pasan como closures (Groovy) o lambdas (Kotlin) a métodos de configuración, para configurar objetos internos como `project`, `repositories`, `dependencies`  

---

## 2. Clausuras, lambdas, delegados / receptores

- En **Groovy**, los bloques son *closures* y Gradle usa delegación dinámica para resolver llamadas a métodos o propiedades dentro del closure. 
- En **Kotlin**, se usan *lambdas con receptor*; el receptor (`this`) está tipado estáticamente. 
- Dentro de bloques comunes como `repositories { ... }`, se configura un objeto receptor específico (por ejemplo `RepositoryHandler`). Llamadas como `mavenCentral()` no necesitan calificativo explícito.
---

## 3. Variables y propiedades

- **Variables locales**:  
  - En Kotlin: `val`  
  - En Groovy: `def` 
- **Propiedades extra (extra / ext)**: permiten añadir datos definidos por el usuario a objetos mejorados como `project`. Tienen un ámbito más amplio que las variables locales.

---

## 4. Ejecución paso a paso

- El script de construcción se ejecuta *línea a línea* durante la fase de configuración.  
- Las **instrucciones externas** a bloques se ejecutan inmediatamente; para lógica tardía se recomiendan APIs perezosas o `Provider`. 
- El orden de declaración puede afectar el comportamiento; por ejemplo, definir variables o tareas en un cierto orden es relevante. 

---

## 5. Ejemplo práctico: análisis de un script

Se presenta un ejemplo en ambos DSL (Groovy y Kotlin) con varias secciones, para ilustrar:

1. Aplicar plugins (`plugins { ... }`)  
2. Definir repositorios (`repositories { ... }`)  
3. Añadir dependencias (`dependencies { ... }`)  
4. Establecer propiedades del proyecto (`application { mainClass = ... }`)  
5. Registrar y configurar tareas (`tasks.register`, `tasks.named`, etc.)  

Dentro del ejemplo, se destaca que se prefiere `tasks.register(...)` sobre `tasks.create(...)` para favorecer la *evitación de configuración temprana* (configuration avoidance). 

## Ejemplo de Build Script

```
kotlin
// build.gradle.kts

plugins {   (1)
    id("application")
}

repositories {  (2)
    mavenCentral()
}

dependencies {  (3)
    testImplementation("org.junit.jupiter:junit-jupiter-engine:5.9.3")
    testRuntimeOnly("org.junit.platform:junit-platform-launcher")
    implementation("com.google.guava:guava:32.1.1-jre")
}

application {   (4)
    mainClass = "com.example.Main"
}

tasks.named<Test>("test") { (5)
    useJUnitPlatform()
}

tasks.named<Javadoc>("javadoc").configure {
    exclude("app/Internal*.java")
    exclude("app/internal/*")
}

tasks.register<Zip>("zip-reports") {
    from("Reports/")
    include("*")
    archiveFileName.set("Reports.zip")
    destinationDirectory.set(file("/dir"))
}

// build.gradle

plugins {   (1)
    id 'application'
}

repositories {  (2)
    mavenCentral()
}

dependencies {  (3)
    testImplementation 'org.junit.jupiter:junit-jupiter-engine:5.9.3'
    testRuntimeOnly 'org.junit.platform:junit-platform-launcher'
    implementation 'com.google.guava:guava:32.1.1-jre'
}

application {   (4)
    mainClass = 'com.example.Main'
}

tasks.named('test', Test) { (5)
    useJUnitPlatform()
}

tasks.named('javadoc', Javadoc).configure {
    exclude 'app/Internal*.java'
    exclude 'app/internal/*'
}

tasks.register('zip-reports', Zip) {
    from 'Reports/'
    include '*'
    archiveFileName = 'Reports.zip'
    destinationDirectory = file('/dir')
}
```

---
## 6. Otros puntos importantes

- **Acceso a propiedades del proyecto**  
  Puedes usar propiedades como `name`, `version`, `group` directamente sin necesidad de calificar con `project.` en muchos casos. 
- **Scripts de Settings**  
  Operan dentro del contexto `Settings`. Propiedades/métodos del objeto `Settings` están disponibles directamente (como `name`, `rootProject.name`). 

- **Importaciones automáticas de script**  
  Gradle añade automáticamente ciertos `import`s para que el código del script sea más conciso (por ejemplo, usar `StopExecutionException` sin tener que escribir su nombre completo). 

---

## Imagen ilustrativa

![Diagrama de inicialización y configuración de proyectos](https://docs.gradle.org/current/userguide/img/gradle-basic-11.png) 

---

## Instrucciones **importantes** para escribir scripts

- *Usa* **`tasks.register(...)`** en lugar de `tasks.create(...)` para evitar configuraciones prematuras.  
- *Define* repositorios antes de declarar dependencias para que Gradle sepa dónde buscar los artefactos. 
- *Aprovecha* las propiedades extra (`ext`/`extra`) para compartir configuración entre proyectos o dentro del mismo script. 

[Visita la página original](https://docs.gradle.org/current/userguide/writing_build_scripts_intermediate.html)
