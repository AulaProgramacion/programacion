# UT2.3 Estructuras de Repetición

## 📋 Índice de contenidos

1. [Introducción: Control de entrada por teclado](#1-introducci%C3%B3n-control-de-entrada-por-teclado)
    1. [La clase Teclado](#11-la-clase-teclado)
    2. [Validación con if](#12-validaci%C3%B3n-con-if)
    3. [Buenas prácticas en la entrada de datos](#13-buenas-pr%C3%A1cticas-en-la-entrada-de-datos)
    4. [Ejemplo: menú con validación](#14-ejemplo-men%C3%BA-con-validaci%C3%B3n)
2. [Práctica 7: Control de datos en todos los programas](#2-pr%C3%A1ctica-7-control-de-datos-en-todos-los-programas)
    1. [Objetivos y tareas](#21-objetivos-y-tareas)
    2. [Ejemplo de implementación](#22-ejemplo-de-implementaci%C3%B3n)
    3. [Criterios de evaluación](#23-criterios-de-evaluaci%C3%B3n)
3. [Anexo: Scanner y validación de tipo (código legacy)](#3-anexo-scanner-y-validaci%C3%B3n-de-tipo-c%C3%B3digo-legacy)

## 1. Introducción: Control de entrada por teclado

En cualquier aplicación interactiva, **leer y validar datos introducidos por el usuario** es fundamental para evitar errores y asegurar el correcto funcionamiento del programa.

### Problemas comunes sin validación

- **Excepciones no controladas** que terminan el programa abruptamente
- **Comportamientos inesperados** con datos no válidos
- **Experiencia de usuario deficiente** sin mensajes de error claros

> [!WARNING]
> **Error típico del programador novato**: Asumir que el usuario siempre introducirá datos correctos.

La validación de entrada no solo previene errores, sino que también mejora significativamente la experiencia del usuario al proporcionar retroalimentación clara sobre qué tipo de datos se esperan.

### 1.1 La clase `Teclado`

Ya sabemos que `IO.readln` siempre devuelve un `String`, y que convertirlo directamente a número con `Integer.parseInt`/`Double.parseDouble` puede romper el programa si el texto no es válido. A partir de ahora usaremos una pequeña clase de apoyo, `Teclado`, que nos dice si un texto se puede convertir de forma segura:

```java
public class Teclado {

    public static boolean esEntero(String texto) {
        if (texto == null || texto.isBlank()) return false;
        return texto.trim().matches("-?\\d+");
    }

    public static boolean esDecimal(String texto) {
        if (texto == null || texto.isBlank()) return false;
        String preparado = texto.trim().replace(',', '.');
        return preparado.matches("-?\\d+(\\.\\d+)?");
    }

    public static boolean esBooleano(String texto) {
        if (texto == null || texto.isBlank()) return false;
        String limpio = texto.trim().toLowerCase();
        return limpio.equals("true") || limpio.equals("false");
    }
}
```

> [!NOTE]
> No es necesario que entendáis todavía cómo funciona `matches` en detalle (lo veremos en la unidad de expresiones regulares). De momento, usad estos métodos como una herramienta ya construida: os dicen `true` o `false` según si el texto es válido.

### 1.2 Validación con `if`

Los métodos de `Teclado` solo responden `true`/`false`; sois vosotros quienes decidís, con `if`, qué hacer con esa respuesta:

```java
public class ValidacionSimple {
    public static void main(String[] args) {
        String entrada = IO.readln("Introduce tu edad: ");

        if (Teclado.esEntero(entrada)) {
            int edad = Integer.parseInt(entrada);
            IO.println("Tienes " + edad + " años");
        } else {
            IO.println("Error: debes introducir un número entero válido.");
        }
    }
}
```

> [!IMPORTANT]
> Con las herramientas que conocemos hasta ahora, si el dato es incorrecto solo podemos **informar del error y continuar sin ese dato** (o terminar el programa). Todavía no sabemos "insistir" pidiéndolo de nuevo: eso requiere una estructura repetitiva (`while`), que veremos en la próxima unidad. Por ahora, `Teclado.esEntero`/`esDecimal` solo responden a la pregunta "¿es válido?"; qué hacer con la respuesta lo decidís vosotros con `if`.

### 1.3 Buenas prácticas en la entrada de datos

- **Valida SIEMPRE** antes de convertir cualquier dato introducido por el usuario.
- **Proporciona mensajes de error claros** para que el usuario entienda qué ha hecho mal.
- Con `IO.readln` no existe el problema de "limpiar el buffer" que sí tenía `Scanner` (ver Anexo): cada `readln` consume siempre una línea completa.

### 1.4 Ejemplo: menú con validación

```java
public class MenuConValidacion {
    public static void main(String[] args) {
        IO.println("¡Bienvenido al sistema de gestión! 🎉");
        IO.println("\n🏪 MENÚ PRINCIPAL");
        IO.println("================");
        IO.println("1️⃣  Ver productos");
        IO.println("2️⃣  Añadir producto");
        IO.println("3️⃣  Eliminar producto");
        IO.println("4️⃣  Calcular total");
        IO.println("0️⃣  Salir");

        String textoOpcion = IO.readln("\n👉 Selecciona una opción (0-4): ");

        if (Teclado.esEntero(textoOpcion)) {
            int opcion = Integer.parseInt(textoOpcion);

            if (opcion >= 0 && opcion <= 4) {
                switch (opcion) {
                    case 1:
                        IO.println("📋 Mostrando productos...");
                        break;
                    case 2:
                        IO.println("➕ Añadiendo producto...");
                        break;
                    case 3:
                        IO.println("🗑️ Eliminando producto...");
                        break;
                    case 4:
                        IO.println("🧮 Calculando total...");
                        break;
                    case 0:
                        IO.println("👋 ¡Hasta luego!");
                        break;
                }
            } else {
                IO.println("❌ Opción no válida. Debe ser entre 0 y 4");
            }
        } else {
            IO.println("❌ Debes introducir un número entero");
        }
    }
}
```

> [!NOTE]
> Este menú se muestra y se resuelve **una sola vez**. En la unidad de estructuras repetitivas aprenderemos a hacer que se repita automáticamente hasta que el usuario elija "Salir".

## 2. Práctica 7: Control de datos en todos los programas

### 2.1 Objetivos y tareas

**Objetivo:** Modificar todos los programas realizados hasta ahora para que implementen un **control robusto de los datos introducidos por teclado**.

**Tareas a realizar:**

- Revisar cada programa desarrollado hasta este punto.
- Añadir validación con `Teclado.esEntero`/`esDecimal` para todas las entradas del usuario.
- Incluir mensajes de error informativos y claros con `if`.
- Probar con entradas incorrectas y comprobar que el programa informa del error sin romperse.

### 2.2 Ejemplo de implementación

**Versión sin control de datos (NO RECOMENDADO):**

```java
String textoNum = IO.readln("Introduce un número: ");
int num = Integer.parseInt(textoNum); // Puede fallar si la entrada no es un entero
```

**Versión con control de datos (RECOMENDADO):**

```java
String textoNum = IO.readln("Introduce un número entero no negativo: ");

if (Teclado.esEntero(textoNum)) {
    int num = Integer.parseInt(textoNum);
    if (num < 0) {
        IO.println("⚠️ Error: el número no puede ser negativo.");
    } else {
        IO.println("Número válido introducido: " + num);
    }
} else {
    IO.println("⚠️ Error: solo se aceptan números enteros.");
}
```

> [!IMPORTANT]
> Esta práctica es esencial para desarrollar programas robustos que no fallen cuando el usuario introduce datos incorrectos. Con las herramientas actuales, "robusto" significa que el programa **informa del error en vez de romperse**, no que insista automáticamente — eso llegará con las estructuras repetitivas.

### 2.3 Criterios de evaluación

- **Funcionalidad:** El programa debe funcionar correctamente tanto con entradas válidas como inválidas.
- **Mensajes claros:** El usuario debe comprender qué ha hecho mal y por qué el programa no ha podido continuar.
- **Robustez:** El programa nunca debe terminar de forma abrupta o inesperada por una `NumberFormatException` no controlada.
- **Código limpio:** Uso adecuado de `Teclado.esEntero`/`esDecimal` y estructura `if` clara.

> [!CAUTION]
> Prueba tus programas con diferentes tipos de entradas: letras cuando se esperan números, valores fuera de rango, etc. El objetivo es que el programa nunca se bloquee ni lance excepciones inesperadas.

## 3. Anexo: Scanner y validación de tipo (código legacy)

> [!WARNING]
> Este anexo se explica de forma independiente al hilo principal de la asignatura. La clase `Scanner` fue durante muchos años la forma estándar de validar y leer datos por teclado en Java, y todavía la encontraréis en código existente y documentación antigua. Debéis conocerla para poder leer ese código, pero **no** es la forma de trabajar que seguiremos este curso.

### 3.1 Inicialización del Scanner

```java
import java.util.Scanner;

public class EjemploScanner {
    public static void main(String[] args) {
        Scanner lector = new Scanner(System.in);

        // ... código del programa ...

        lector.close(); // IMPORTANTE: cerrar el Scanner al final
    }
}
```

**Métodos básicos de lectura:**

| Método | Tipo de retorno | Descripción | Ejemplo |
|---|---|---|---|
| `next()` | `String` | Lee la siguiente palabra (hasta espacio en blanco) | `"Hola"` |
| `nextLine()` | `String` | Lee toda la línea (hasta Enter) | `"Hola mundo"` |
| `nextInt()` | `int` | Lee un número entero | `42` |
| `nextDouble()` | `double` | Lee un número decimal | `3.14` |
| `nextBoolean()` | `boolean` | Lee un valor booleano | `true`/`false` |

**Ejemplo básico sin validación:**

```java
import java.util.Scanner;

public class LecturaBasica {
    public static void main(String[] args) {
        Scanner lector = new Scanner(System.in);

        System.out.print("Introduce tu nombre: ");
        String nombre = lector.nextLine();

        System.out.print("Introduce tu edad: ");
        int edad = lector.nextInt(); // ⚠️ PELIGRO: Puede fallar

        System.out.println("Hola " + nombre + ", tienes " + edad + " años");
        lector.close();
    }
}
```

> [!CAUTION]
> El código anterior fallará si el usuario introduce texto en lugar de un número para la edad.

### 3.2 Métodos de validación de tipo (`hasNextX`)

`Scanner` incluye métodos para comprobar el tipo de dato **antes** de leerlo:

| Método | Tipo verificado | Descripción |
|---|---|---|
| `hasNextByte()` | `byte` | Verifica si la siguiente entrada es un byte válido |
| `hasNextShort()` | `short` | Verifica si la siguiente entrada es un short válido |
| `hasNextInt()` | `int` | Verifica si la siguiente entrada es un int válido |
| `hasNextLong()` | `long` | Verifica si la siguiente entrada es un long válido |
| `hasNextFloat()` | `float` | Verifica si la siguiente entrada es un float válido |
| `hasNextDouble()` | `double` | Verifica si la siguiente entrada es un double válido |
| `hasNextBoolean()` | `boolean` | Verifica si la siguiente entrada es un boolean válido |
| `hasNext()` | `String` | Verifica si hay más entrada disponible |
| `hasNextLine()` | `String` | Verifica si hay una línea completa disponible |

**Ejemplo de uso con `if` (una sola comprobación, sin bucle):**

```java
Scanner lector = new Scanner(System.in);
System.out.print("Introduce un número entero: ");

if (lector.hasNextInt()) {
    int numero = lector.nextInt();
    lector.nextLine(); // Consume el resto de la línea
    System.out.println("✅ Número introducido correctamente: " + numero);
} else {
    System.out.println("❌ Error: no has introducido un número entero válido.");
}

lector.close();
```

> [!TIP]
> Los métodos `hasNextX()` **no consumen** la entrada, solo la verifican. Después de validar, aún necesitas leer el valor con el método correspondiente (`nextInt()`, `nextDouble()`, etc.).

### 3.3 Buenas prácticas en la entrada de datos (legacy)

- **Valida SIEMPRE** antes de leer cualquier dato introducido por el usuario.
- **Proporciona mensajes de error claros** para guiar al usuario.
- **Cierra el Scanner** al final del programa con `lector.close()` para liberar recursos.

> [!WARNING]
> No cerrar el `Scanner` puede provocar advertencias del compilador y posibles problemas de recursos.

### 3.4 Ejemplo: menú con validación (legacy)

```java
import java.util.Scanner;

public class MenuConValidacionLegacy {
    public static void main(String[] args) {
        Scanner lector = new Scanner(System.in);

        System.out.println("¡Bienvenido al sistema de gestión! 🎉");
        System.out.println("\n🏪 MENÚ PRINCIPAL");
        System.out.println("================");
        System.out.println("1️⃣  Ver productos");
        System.out.println("2️⃣  Añadir producto");
        System.out.println("3️⃣  Eliminar producto");
        System.out.println("4️⃣  Calcular total");
        System.out.println("0️⃣  Salir");
        System.out.print("\n👉 Selecciona una opción (0-4): ");

        if (lector.hasNextInt()) {
            int opcion = lector.nextInt();

            if (opcion >= 0 && opcion <= 4) {
                switch (opcion) {
                    case 1:
                        System.out.println("📋 Mostrando productos...");
                        break;
                    case 2:
                        System.out.println("➕ Añadiendo producto...");
                        break;
                    case 3:
                        System.out.println("🗑️ Eliminando producto...");
                        break;
                    case 4:
                        System.out.println("🧮 Calculando total...");
                        break;
                    case 0:
                        System.out.println("👋 ¡Hasta luego!");
                        break;
                }
            } else {
                System.out.println("❌ Opción no válida. Debe ser entre 0 y 4");
            }
        } else {
            System.out.println("❌ Debes introducir un número entero");
        }

        lector.close();
    }
}
```

<p align="center">📚 <em>Fin del apartado UT2.2 - Programación estructurada: Entrada por teclado y control de datos</em></p>

***