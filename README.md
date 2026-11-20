<<<<<<< HEAD
# My Application

A Spring Boot + Vaadin project. Build your UI in pure Java — no HTML, no JavaScript.

> **New to Vaadin?** The 5-minute [Quickstart](https://vaadin.com/quickstart) walks you from here to your first running app, a live code change, and an AI-assisted edit with Copilot.

---

## Fastest start — no plugin needed

From the project folder:

```bash
./mvnw spring-boot:run        # Windows: mvnw.cmd spring-boot:run
```

Then open **http://localhost:8080**.

The first start takes ~30 seconds while Maven downloads dependencies. This project has no views yet, so the browser shows a *Could not navigate to ''* (route not found) page. That means the app is running: add your first view, a class annotated with `@Route("")`, to replace it.

> **Port 8080 already in use?** Stop the other process, or set `server.port=8081` in `src/main/resources/application.properties` and open that port instead.
>
> **To stop the app:** press `Ctrl+C` in the terminal (or the red Stop button if you launched from your IDE).

## Optional upgrade — instant hotswap

Running with `spring-boot:run` works, but Java code changes need a server restart. For **live reload** — edit Java, see it in the browser without restarting — install the **Vaadin plugin** and start the app through it:

- **IntelliJ IDEA:** install *Vaadin* from the JetBrains Marketplace → **Debug using Hotswap Agent** (dropdown next to Run). *Just installed it? Let IntelliJ finish indexing, or restart it, if the menu item isn't there yet.*
- **VS Code:** install the *Vaadin* extension → **Vaadin: Debug using Hotswap Agent** from the command palette.
- **Eclipse:** install the *Vaadin* plugin → right-click the project → **Run As → Vaadin Application**.

This is what makes the edit-and-see-it loop feel instant — and it's required for the AI edits in [Vaadin Copilot](https://vaadin.com/docs/latest/tools/copilot).

> **Run the app one way at a time.** `./mvnw spring-boot:run`, your IDE, and the Dev Loop all serve on port 8080, so stop one before starting another. If an AI coding agent edits the code for you, use the Dev Loop instead of the IDE — see [Agentic Development](#agentic-development).

---

## Ask your AI assistant about Vaadin (optional)

If you use Claude Code, Cursor, or another AI coding assistant, connect it to the **Vaadin MCP server** so it answers against real Vaadin docs and the exact API of your installed version — instead of guessing from outdated training data.

The one-time setup is described in [Vaadin MCP server](https://vaadin.com/docs/latest/building-apps/mcp).

---

## Agentic Development

If you develop with an AI coding agent, such as Claude Code or Codex, enable the Vaadin Dev Loop. It lets the agent make
its changes live in the running application with a single command, and tells it whether they took effect, without
restarting the application or checking screenshots. To enable it, run:

```bash
./mvnw vaadin:install-dev-cli
```

This installs the Dev Loop CLI into `.vaadin/`, and skills that teach your agent how to use it into `.agents/skills/` and
`.claude/skills/`. Commit these files with the rest of the project, and run the command again after upgrading Vaadin.

Once it is enabled, start the application through the Dev Loop, and leave the page open in the browser:

```bash
.vaadin/vaadin-dev start      # Windows: .vaadin\vaadin-dev.cmd start
```

The Dev Loop owns the application process and brings its own Hotswap Agent, so do not also start the application with
`./mvnw spring-boot:run` or an IDE run or debug configuration: the second launcher fights the Dev Loop for port 8080. Use
`.vaadin/vaadin-dev status` to see whether the application is running, and `.vaadin/vaadin-dev restart` instead of
restarting it from the IDE.

The Dev Loop is a preview feature. To learn more, including how to give your agent access to the Vaadin documentation,
see the [Dev Loop tutorial](https://vaadin.com/docs/v25/building-apps/agentic-development/dev-loop-tutorial).

---

## Build for production

```bash
./mvnw package
java -jar target/*.jar
```

To build a Docker image, run:

```bash
docker build -t my-application:latest .
```

If you use commercial components, pass the license key as a build secret:

```bash
docker build --secret id=proKey,src=$HOME/.vaadin/proKey -t my-application:latest .
```

To run the image, run:

```bash
docker run -p 8080:8080 -m 2g my-application:latest
```

The application is then available at http://localhost:8080. The `-m` option sets the memory limit of the container. The
application uses up to 75% of it for the Java heap, which holds the UI state of all users, so adjust the limit to fit
your application.

## Learn more

- [Vaadin Quickstart](https://vaadin.com/quickstart) — the 5-minute getting-started path
- [Components](https://vaadin.com/docs/latest/components) — 50+ UI components, all callable from Java
- [Vaadin Copilot](https://vaadin.com/docs/latest/tools/copilot) — visual + AI editing in the browser
- [Full documentation](https://vaadin.com/docs)
=======
# Conversor de Temperatura

Aplicación web para convertir valores entre unidades de temperatura (Celsius, Fahrenheit, Kelvin, Rankine y Réaumur), desarrollada con **Vaadin 24**, **Spring Boot 3** y **Java 17**, aplicando los cuatro pilares de la Programación Orientada a Objetos.

## Integrantes

| Integrante | Rol / aporte |
|---|---|
| Miguel Posada | *(completar: p. ej. modelo y jerarquía de clases)* |
| Luis Enrique Vergara | *(completar: p. ej. servicio y lógica de negocio)* |
| Maria Isabel Correa | *(completar: p. ej. interfaz Vaadin, validaciones y documentación)* |

> Ajusten la columna de aportes según lo que realmente hizo cada uno.

---

## 1. Descripción del proyecto

El usuario ingresa un valor, elige la unidad de origen y la de destino, y la aplicación:

1. Muestra el resultado de la conversión.
2. Muestra una tabla de **equivalencias** del mismo valor en todas las unidades disponibles.
3. Guarda un **historial** de conversiones de la sesión.
4. Permite **intercambiar** origen y destino con un botón.
5. Valida los datos y muestra mensajes de error claros.

## 2. Tecnologías y dependencias

| Tecnología | Versión | Uso |
|---|---|---|
| Java | 17 | Lenguaje |
| Spring Boot | 3.3.5 | Inyección de dependencias y arranque |
| Vaadin | 24.5.5 | Interfaz web 100 % en Java |
| Maven | 3.8+ | Gestión de dependencias y build |

Dependencias principales (definidas en `pom.xml`): `vaadin-spring-boot-starter`, `spring-boot-devtools` y `spring-boot-starter-test`.

## 3. Estructura del proyecto

```
conversor-temperatura/
├── pom.xml
└── src/main/
    ├── java/com/example/conversor/
    │   ├── Application.java
    │   ├── model/
    │   │   ├── Unidad.java                (interfaz)
    │   │   ├── Convertible.java           (interfaz)
    │   │   ├── UnidadTemperatura.java     (clase abstracta)
    │   │   ├── Celsius.java
    │   │   ├── Fahrenheit.java
    │   │   ├── Kelvin.java
    │   │   ├── Rankine.java
    │   │   ├── Reaumur.java
    │   │   └── RegistroConversion.java
    │   ├── service/
    │   │   └── ConversorService.java
    │   └── view/
    │       └── ConversorView.java
    └── resources/
        └── application.properties
```

### Arquitectura por capas

| Capa | Paquete | Responsabilidad |
|---|---|---|
| Modelo | `model` | Reglas de conversión y representación de las unidades |
| Servicio | `service` | Orquesta las conversiones y administra el historial |
| Vista | `view` | Interfaz de usuario con Vaadin, validación de entradas y mensajes |

Cada capa tiene una única responsabilidad y depende solo de la capa inferior: la vista usa el servicio, y el servicio usa el modelo. El modelo no conoce ni a Vaadin ni al servicio.

## 4. Cómo ejecutar

Requisitos: JDK 17 y Maven. Vaadin necesita Node.js; si no está instalado, lo descarga automáticamente.

```bash
mvn clean install
mvn spring-boot:run
```

Abrir http://localhost:8080. La primera ejecución tarda más porque Vaadin construye el frontend.

---

## 5. Cómo se implementó la funcionalidad

### 5.1 Algoritmo de conversión (unidad pivote)

En lugar de escribir una fórmula por cada par de unidades (con 5 unidades serían 20 fórmulas), se usa **Celsius como unidad base**. Cada unidad solo sabe convertirse **hacia** Celsius y **desde** Celsius:

```
origen ──aBase()──▶ Celsius ──desdeBase()──▶ destino
```

Esto está implementado en `UnidadTemperatura.convertirA()`:

```java
public final double convertirA(UnidadTemperatura destino, double valor) {
    double celsius = this.aBase(valor);
    // validación de cero absoluto...
    return destino.desdeBase(celsius);
}
```

Se necesitan solo **2 fórmulas por unidad**, y agregar una unidad nueva no obliga a modificar las existentes.

| Unidad | `aBase` (a Celsius) | `desdeBase` (desde Celsius) |
|---|---|---|
| Celsius | `c` | `c` |
| Fahrenheit | `(f - 32) × 5/9` | `c × 9/5 + 32` |
| Kelvin | `k - 273.15` | `c + 273.15` |
| Rankine | `(r - 491.67) × 5/9` | `c × 9/5 + 491.67` |
| Réaumur | `re × 5/4` | `c × 4/5` |

### 5.2 Servicio

`ConversorService` recibe **todas** las unidades registradas como `List<UnidadTemperatura>` mediante inyección de dependencias de Spring. Ofrece:

- `convertir(origen, destino, valor)`: realiza la conversión y la registra en el historial.
- `convertirATodas(origen, valor)`: devuelve un `Map` con el valor en todas las unidades (alimenta la tabla de equivalencias).
- `getUnidades()` y `getHistorial()`: consulta de datos de solo lectura.
- `limpiarHistorial()`: borra el historial.

### 5.3 Flujo completo de una conversión

1. El usuario pulsa **Convertir** en `ConversorView`.
2. La vista lee y valida los campos.
3. Llama a `ConversorService.convertir(...)`.
4. El servicio invoca `origen.convertirA(destino, valor)` (modelo).
5. Se crea un `RegistroConversion` y se agrega al historial.
6. La vista actualiza la etiqueta de resultado, la tabla de equivalencias y el historial.

---

## 6. Cómo se implementó Vaadin

Vaadin permite construir la interfaz web **íntegramente en Java**, sin escribir HTML, CSS ni JavaScript. Todo está en `ConversorView`.

| Elemento Vaadin | Uso en el proyecto |
|---|---|
| `@Route("")` | Publica la vista en la ruta raíz `/` |
| `@PageTitle` | Define el título de la pestaña del navegador |
| `VerticalLayout` / `HorizontalLayout` | Organización de los componentes en columnas y filas |
| `NumberField` | Entrada numérica del valor a convertir |
| `ComboBox<UnidadTemperatura>` | Selección de unidad de origen y destino |
| `Button` + `ButtonVariant` | Acciones: Convertir, Intercambiar y Limpiar historial |
| `Grid` | Tabla de equivalencias y tabla de historial |
| `Notification` + `NotificationVariant.LUMO_ERROR` | Mensajes de error visibles al usuario |
| `H1` / `H2` | Títulos y resultado |

Puntos de integración con Spring:

- La vista recibe el servicio por **inyección en el constructor** (`ConversorView(ConversorService servicio)`).
- `@Application implements AppShellConfigurator` es el punto de entrada requerido por Vaadin.
- Los `ComboBox` se llenan directamente con objetos del modelo y usan `setItemLabelGenerator(UnidadTemperatura::getDescripcion)` para mostrar el texto, de modo que la vista no duplica nombres ni símbolos de unidades.

---

## 7. Por qué el proyecto cumple con POO y con una buena estructura

### 7.1 Abstracción

`UnidadTemperatura` es una **clase abstracta** que define *qué* debe hacer una unidad (convertir hacia y desde la base) sin definir *cómo* lo hace cada una. Los métodos `aBase()` y `desdeBase()` se declaran en la interfaz `Convertible` y quedan sin implementar en la clase abstracta. Además, las interfaces `Unidad` y `Convertible` separan dos conceptos distintos: **identidad** de una unidad (nombre, símbolo) y **capacidad** de convertirse.

### 7.2 Herencia

`Celsius`, `Fahrenheit`, `Kelvin`, `Rankine` y `Reaumur` **extienden** `UnidadTemperatura`. Heredan el constructor con nombre y símbolo, los getters, `toString()` y el algoritmo `convertirA()`. Cada subclase solo aporta lo que la diferencia: sus dos fórmulas.

### 7.3 Polimorfismo

- `convertirA()` llama a `this.aBase()` y `destino.desdeBase()` sin saber con qué unidades concretas trabaja; en tiempo de ejecución se ejecuta la versión de la subclase correspondiente.
- `ConversorService` y `ConversorView` operan siempre con el tipo `UnidadTemperatura`, nunca con `Celsius` o `Kelvin` directamente.
- `Unidad.getDescripcion()` es un método `default` que todas las unidades usan sin reimplementarlo.

### 7.4 Encapsulamiento

- Los atributos (`nombre`, `simbolo`) son `private final` y se acceden solo por getters.
- Las constantes `CERO_ABSOLUTO_C` y `TOLERANCIA` son `private static final`.
- `convertirA()` es `final`: ninguna subclase puede alterar el algoritmo ni saltarse la validación.
- `RegistroConversion` es **inmutable** (todos sus campos son `final` y no tiene setters).
- El servicio no expone sus listas internas: devuelve `Collections.unmodifiableList(...)`.

### 7.5 Principios de diseño y estructura

| Principio | Cómo se cumple |
|---|---|
| **Responsabilidad única** | El modelo convierte, el servicio orquesta, la vista presenta |
| **Abierto/Cerrado** | Agregar una unidad (p. ej. Delisle) es crear una clase `@Component` que extienda `UnidadTemperatura`; no se modifica servicio ni vista |
| **Inversión de dependencias** | La vista y el servicio dependen de abstracciones (`UnidadTemperatura`), y Spring inyecta las implementaciones |
| **Bajo acoplamiento** | El modelo no conoce Vaadin ni Spring más allá de la anotación `@Component` |
| **Patrón Template Method** | `convertirA()` define el esqueleto del algoritmo; las subclases rellenan los pasos |
| **Organización en paquetes** | `model`, `service` y `view` separan claramente las capas |

---

## 8. Validación y manejo de datos

### 8.1 Validación de entradas (capa de vista)

| Validación | Dónde | Efecto |
|---|---|---|
| Solo se aceptan números | `NumberField` | El componente rechaza texto no numérico en el navegador |
| Campos obligatorios | `ConversorView.convertir()` comprueba `valor == null`, `origen == null`, `destino == null` | Muestra "Completa todos los campos" y no ejecuta la conversión |
| Solo unidades existentes | `ComboBox.setAllowCustomValue(false)` | El usuario no puede escribir una unidad inventada |
| Valores iniciales seguros | `campoValor.setValue(0.0)` y unidades preseleccionadas | La pantalla nunca arranca en un estado inválido |

### 8.2 Validación de reglas de negocio (capa de modelo)

La regla física más importante es el **cero absoluto**: ninguna temperatura puede estar por debajo de -273.15 °C (0 K). `UnidadTemperatura.convertirA()` convierte primero a Celsius y valida:

```java
if (celsius < CERO_ABSOLUTO_C - TOLERANCIA) {
    throw new IllegalArgumentException("Por debajo del cero absoluto. ...");
}
```

- La validación se hace **una sola vez, en la unidad base**, por lo que protege a las cinco unidades (y a cualquiera que se agregue en el futuro) sin duplicar código.
- La `TOLERANCIA` (`1e-9`) evita falsos errores por redondeo de números decimales: por ejemplo, 0 K o -459.67 °F, que equivalen exactamente al cero absoluto, no se rechazan por imprecisión de punto flotante.
- El mensaje de error indica el **mínimo válido en la unidad que el usuario eligió**, no en Celsius, lo que lo hace comprensible.

### 8.3 Manejo de errores

La vista captura la `IllegalArgumentException` lanzada por el modelo y la transforma en una `Notification` roja en la parte superior de la pantalla:

```java
try {
    double resultado = servicio.convertir(origen, destino, valor);
    ...
} catch (IllegalArgumentException ex) {
    mostrarError(ex.getMessage());
}
```

La aplicación no se rompe ni muestra una traza al usuario; la validación vive en el modelo y la vista solo se encarga de comunicarla.

### 8.4 Manejo de datos

| Aspecto | Implementación |
|---|---|
| **Aislamiento por usuario** | `ConversorService` es `@VaadinSessionScope`: cada sesión del navegador tiene su propio historial |
| **Inmutabilidad** | `RegistroConversion` no puede modificarse después de creado, por lo que el historial es confiable |
| **Protección de las colecciones** | Los getters devuelven listas no modificables; la lista de unidades se copia en el constructor (copia defensiva) |
| **Orden consistente** | Las unidades se ordenan por nombre; el historial muestra lo más reciente primero (`add(0, ...)`) |
| **Equivalencias ordenadas** | Se usa `LinkedHashMap` para mantener el orden de inserción en la tabla |
| **Formato de salida** | Todos los números se muestran con `String.format("%.2f", ...)` para una presentación uniforme |
| **Sin fallos silenciosos** | Los errores se lanzan como excepciones y se muestran al usuario |

---

## 9. Extensión del proyecto

Para agregar una nueva unidad, por ejemplo Delisle, basta con crear una clase:

```java
@Component
public class Delisle extends UnidadTemperatura {
    public Delisle() { super("Delisle", "°De"); }

    @Override public double aBase(double v)       { return 100 - v * 2 / 3; }
    @Override public double desdeBase(double c)   { return (100 - c) * 3 / 2; }
}
```

Spring la detecta automáticamente y aparece en los desplegables, en la tabla de equivalencias y en el historial, sin modificar ninguna otra clase.

## 10. Posibles mejoras

- Pruebas unitarias con JUnit para cada unidad (ya incluye `spring-boot-starter-test`).
- Conversión automática al escribir, sin pulsar el botón.
- Soporte para otras magnitudes (longitud, peso) reutilizando las interfaces `Unidad` y `Convertible`.
- Persistencia del historial en base de datos.
>>>>>>> 53fd105052da004909467020ad91f69174e32dd0
