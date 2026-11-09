# Guali Tutor — Desarrollo de la interfaz para Android

**Universidad Mariano Gálvez de Guatemala**  
**Facultad de Ingeniería · Programación II**  
**Fase 3**  
**Estudiante:** Fátima Alexandra Monterroso Avendaño  
**Carné:** 3190-24-16684  
**Catedrático:** Ing. MGSI. César Hernández

## Introducción

Este tutorial presenta la estructura y el desarrollo del *frontend* móvil de **Guali Tutor**, una adaptación para Android de la interfaz de la aplicación de escritorio. La propuesta reúne las secciones principales del sistema: lecciones, editor de código, botones de acción, consola, configuración, historial y ayuda.

El alcance de esta fase se concentra en la **interfaz de usuario**. Los botones permiten recorrer y observar el diseño, pero el prototipo móvil no incorpora un compilador Java ni realiza ejecuciones reales de código. Tampoco necesita conectarse a la API REST de la fase anterior para mostrar sus pantallas.

## 1. Herramientas y requisitos

Para trabajar con el proyecto se necesita:

- **Android Studio**, disponible en <https://developer.android.com/studio>.
- **Android SDK Platform 35** y herramientas de compilación correspondientes, instalables desde el SDK Manager.
- **JDK 17**, que puede configurarse mediante el runtime incluido con Android Studio.
- Conexión a Internet para la primera sincronización de Gradle.
- Un emulador Android o dispositivo físico, en caso de querer realizar pruebas de ejecución. No es indispensable para revisar el código y el diseño.

### Instalación básica

1. Descargar Android Studio desde su página oficial e instalarlo en Windows.
2. Abrir el programa y completar la configuración inicial.
3. En **More Actions > SDK Manager**, revisar las plataformas y herramientas instaladas. Instalar **Android API 35** si hace falta.
4. En la configuración de Gradle, elegir un JDK 17 compatible.
5. Si se desea probar la aplicación, preparar un dispositivo desde **Device Manager** o conectar un teléfono Android con la depuración USB habilitada.

## 2. Abrir y reconocer el proyecto

El código fuente está organizado como un proyecto de Android Studio denominado `GualiTutorAndroid`.

1. Abrir Android Studio y seleccionar **Open**.
2. Elegir la carpeta `GualiTutorAndroid` (no el archivo ZIP).
3. Autorizar el proyecto si Android Studio solicita confianza.
4. Permitir que Gradle sincronice las dependencias y revisar los mensajes de la ventana **Build**.

Los archivos principales son:

```text
GualiTutorAndroid/
├── build.gradle
├── settings.gradle
└── app/
    ├── build.gradle
    └── src/main/
        ├── AndroidManifest.xml
        ├── java/com/guali/tutorandroid/MainActivity.java
        └── res/
            ├── layout/activity_main.xml
            ├── values/strings.xml
            └── drawable/box.xml
```

`activity_main.xml` define la presentación de la pantalla, mientras que `MainActivity.java` administra las acciones del usuario.

## 3. Construcción de la interfaz principal

Para diseñar la pantalla se utiliza un archivo XML en `res/layout/activity_main.xml`. La organización parte de un contenedor vertical, que distribuye las zonas de la aplicación.

La pantalla incluye:

1. **Encabezado:** identifica a Guali Tutor.
2. **Navegación:** opciones Lecciones, Configuración, Historial y Ayuda.
3. **Lección activa:** muestra el título y las instrucciones de la actividad seleccionada.
4. **Editor de código:** área de texto editable y multilínea para escribir Java.
5. **Acciones:** botones Compilar y Ejecutar.
6. **Consola:** espacio para comunicar los resultados y mensajes del sistema.

Cada elemento interactivo tiene un identificador (`android:id`) para relacionarlo con su lógica en Java. Esta distribución se inspira en la sección **Interfaz Principal** del enunciado y se adapta al tamaño de una pantalla móvil.

## 4. Programación de la actividad principal

La clase `MainActivity.java` se encarga de cargar el diseño y responder a las acciones realizadas por el usuario. El método `onCreate()` establece la vista y obtiene los componentes necesarios.

```java
@Override
public void onCreate(Bundle state) {
    super.onCreate(state);
    setContentView(R.layout.activity_main);
    // Aquí se inicializan los controles y sus eventos.
}
```

Los botones de navegación reciben eventos mediante `setOnClickListener`. Por ejemplo:

```java
findViewById(R.id.tabLessons)
    .setOnClickListener(v -> chooseLesson());
findViewById(R.id.tabHistory)
    .setOnClickListener(v -> showHistory());
```

De esta forma se separa la organización visual del comportamiento de cada opción.

## 5. Lecciones y editor de código

La opción **Lecciones** abre un cuadro de diálogo con tres ejemplos: *Hola Mundo*, *Errores de compilación* y *Ejecución de programas*. Cuando se selecciona una lección, se actualizan su título y descripción, y se prepara un ejemplo de código en el editor.

El editor es un componente `EditText` de varias líneas. Para facilitar la lectura del código, se utiliza una presentación apropiada para texto de programación. El propósito es que el estudiante pueda escribir y modificar el ejemplo de forma manual.

La información de las lecciones se encuentra definida de manera local en la actividad. Esta fase muestra el diseño de interacción; no implementa la descarga de contenido desde una base de datos.

## 6. Botones Compilar y Ejecutar

Los botones reproducen visualmente las acciones presentes en la aplicación de escritorio. En este frontend móvil, **Compilar** muestra un mensaje de demostración en la consola. **Ejecutar** permanece deshabilitado porque no existe un proceso de compilación real que produzca un programa ejecutable.

Esta decisión evita presentar como exitosas acciones que el prototipo todavía no realiza. Para una etapa posterior podrían evaluarse servicios adicionales de compilación, pero no forman parte de este frontend.

## 7. Configuración, historial y ayuda

La opción **Configuración** abre un cuadro de diálogo con un ajuste de demostración. El valor se conserva localmente mediante `SharedPreferences`.

El **Historial** registra la fecha, el nombre de la lección abierta y su estado inicial *Pendiente*. Estos datos también se guardan de forma local para que permanezcan disponibles cuando se abra nuevamente la aplicación.

La sección **Ayuda** explica de forma breve cómo abrir lecciones, utilizar el editor y revisar la consola.

## 8. Revisión del proyecto

Una vez completada la instalación de los componentes de Android Studio, se recomienda realizar la siguiente comprobación:

1. Abrir `GualiTutorAndroid` y verificar la sincronización de Gradle.
2. Revisar `activity_main.xml` en el editor de diseño o código.
3. Compilar el módulo de la aplicación desde el menú **Build**.
4. Si se dispone de un dispositivo o emulador, iniciar la aplicación.
5. Comprobar la navegación entre las secciones, el contenido de las lecciones y los mensajes de la consola.

**Estado de validación:** este documento describe el proyecto y el procedimiento previsto. No se incluyen capturas de una ejecución verificada; la prueba en Android Studio debe realizarse en el equipo donde se instale.

## 9. Publicación del tutorial

Para compartir el procedimiento, se crea un repositorio **público** en GitHub y se agrega este archivo Markdown. Después de cargarlo se debe verificar que el contenido pueda consultarse sin iniciar sesión.

Las capturas del proceso, cuando estén disponibles, pueden almacenarse en una carpeta `capturas/` del repositorio y añadirse al documento utilizando la sintaxis habitual de Markdown:

```markdown
![Estructura del proyecto](capturas/estructura-proyecto.png)
```

El enlace público del archivo Markdown es el que debe incluirse en el manual técnico PDF de la fase 3.

## Conclusión

La organización del frontend de Guali Tutor para Android permite representar los componentes principales del sistema original mediante una interfaz móvil. La separación entre diseño XML y comportamiento Java facilita comprender cómo se construye una pantalla Android y cómo se vinculan sus controles con las acciones del usuario. El resultado es un punto de partida para futuras ampliaciones de la aplicación.
