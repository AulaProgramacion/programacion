# UT2.2 Programación estructurada: Entrada por teclado y control de datos

## 📋 Índice de contenidos

1. [Introducción: Control de entrada por teclado](#1-introducci%C3%B3n-control-de-entrada-por-teclado)
    1. [Inicialización del Scanner](#11-inicializaci%C3%B3n-del-scanner)
    2. [Métodos de validación de tipo](#12-m%C3%A9todos-de-validaci%C3%B3n-de-tipo)
    3. [Buenas prácticas en la entrada de datos](#13-buenas-pr%C3%A1cticas-en-la-entrada-de-datos)
    4. [Ejemplo](#14-ejemplo)
2. [Práctica 7: Control de datos en todos los programas](#2-pr%C3%A1ctica-7-control-de-datos-en-todos-los-programas)
    1. [Objetivos y tareas](#21-objetivos-y-tareas)
    2. [Ejemplo de implementación](#22-ejemplo-de-implementaci%C3%B3n)
    3. [Criterios de evaluación](#23-criterios-de-evaluaci%C3%B3n)

## 1. Introducción: Control de entrada por teclado

En cualquier aplicación interactiva, **leer y validar datos introducidos por el usuario** es fundamental para evitar errores y asegurar el correcto funcionamiento del programa.

### Problemas comunes sin validación

- **Excepciones no controladas** que terminan el programa abruptamente
- **Comportamientos inesperados** con datos no válidos
- **Bucles infinitos** por entradas incorrectas
- **Experiencia de usuario deficiente** sin mensajes de error claros

> [!WARNING]
> **Error típico del programador novato**: Asumir que el usuario siempre introducirá datos correctos

La validación de entrada no solo previene errores, sino que también mejora significativamente la experiencia del usuario al proporcionar retroalimentación clara sobre qué tipo de datos se esperan.

### 1.1 Inicialización del Scanner

En Java, la clase `Scanner` es la herramienta principal para leer datos desde diferentes fuentes de entrada, siendo la más común la entrada estándar (`System.in`) que representa el teclado.

#### Importación y creación

```java
import java.util.Scanner;

public class EjemploScanner {
    public static void main(String[] args) {
        // Crear el objeto Scanner para leer desde teclado
        Scanner lector = new Scanner(System.in);
        
        // ... código del programa ...
        
        // IMPORTANTE: Cerrar el Scanner al final
        lector.close();
    }
}
```

### Métodos básicos de lectura

| Método | Tipo de retorno | Descripción | Ejemplo |
| :-- | :-- | :-- | :-- |
| `next()` | `String` | Lee la siguiente palabra (hasta espacio en blanco) | `"Hola"` |
| `nextLine()` | `String` | Lee toda la línea (hasta Enter) | `"Hola mundo"` |
| `nextInt()` | `int` | Lee un número entero | `42` |
| `nextDouble()` | `double` | Lee un número decimal | `3.14` |
| `nextBoolean()` | `boolean` | Lee un valor booleano | `true`/`false` |

### Ejemplo básico sin validación

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

### 1.2 Métodos de validación de tipo

La clase `Scanner` proporciona métodos para **comprobar el tipo de dato** que introduce el usuario **antes de intentar leerlo**. Esto evita errores de ejecución y bloqueos inesperados.

| Método | Tipo verificado | Descripción |
| :-- | :-- | :-- |
| `hasNextByte()` | `byte` | Verifica si la siguiente entrada es un byte válido (-128 a 127) |
| `hasNextShort()` | `short` | Verifica si la siguiente entrada es un short válido (-32,768 a 32,767) |
| `hasNextInt()` | `int` | Verifica si la siguiente entrada es un int válido |
| `hasNextLong()` | `long` | Verifica si la siguiente entrada es un long válido |
| `hasNextFloat()` | `float` | Verifica si la siguiente entrada es un float válido |
| `hasNextDouble()` | `double` | Verifica si la siguiente entrada es un double válido |
| `hasNextBoolean()` | `boolean` | Verifica si la siguiente entrada es un boolean válido |
| `hasNext()` | `String` | Verifica si hay más entrada disponible |
| `hasNextLine()` | `String` | Verifica si hay una línea completa disponible |

**Ejemplo de uso**:

Los métodos `hasNext*()` devuelven un **valor booleano**:

- **`true`**: La siguiente entrada ES del tipo especificado ✅
- **`false`**: La siguiente entrada NO es del tipo especificado ❌

```java
Scanner lector = new Scanner(System.in);
System.out.print("Introduce un número entero: ");
while (!lector.hasNextInt()) {
    System.out.println("Error: Debes introducir un número entero válido.");
    System.out.print("Inténtalo de nuevo: ");
    lector.nextLine(); // Consumir la entrada incorrecta
}
int numero = lector.nextInt();
lector.nextLine(); //Consume el resto de la línea por si más adelante queremos leer otros datos.
System.out.println("✅ Número introducido correctamente: " + numero);
```

> [!TIP]
> Los métodos de validación **no consumen** la entrada, solo la verifican. Después de validar, aún necesitas leer el valor.

---

> [!TIP]
> En caso de querer leer un solo dato por línea, siempre utiliza `nextLine()` o `next()` tras la entrada, para evitar bucles infinitos y limpiar el buffer.

### 1.3 Buenas prácticas en la entrada de datos

- **Valida SIEMPRE** antes de leer cualquier dato introducido por el usuario.
- **Proporciona mensajes de error claros** para guiar al usuario.
- **Consume las entradas inválidas** para evitar bucles infinitos.
- **Cierra el Scanner** al final del programa con `lector.close()` para liberar recursos.

```java
// ❌ MAL - Bucle infinito
while (!lector.hasNextInt()) {
    System.out.println("Error: introduce un número");
    // No limpiamos la entrada incorrecta
}

// ✅ BIEN - Limpieza correcta
while (!lector.hasNextInt()) {
    System.out.println("Error: introduce un número");
    lector.next(); // Consume y descarta la entrada incorrecta
}
```

> [!WARNING]
> No cerrar el Scanner puede provocar advertencias del compilador y posibles problemas de recursos.

### 1.4 Ejemplo

```java
import java.util.Scanner;

public class MenuConValidacion {
      
    public static void main(String[] args) {
        Scanner lector = new Scanner(System.in);
        int opcion;
        
        System.out.println("¡Bienvenido al sistema de gestión! 🎉");
        
        do {            
            while (true) {
                System.out.println("\n🏪 MENÚ PRINCIPAL");
                System.out.println("================");
                System.out.println("1️⃣  Ver productos");
                System.out.println("2️⃣  Añadir producto");
                System.out.println("3️⃣  Eliminar producto");
                System.out.println("4️⃣  Calcular total");
                System.out.println("0️⃣  Salir");
                System.out.print("\n👉 Selecciona una opción (0-4): ");
                
                if (lector.hasNextInt()) {
                    opcion = lector.nextInt();
                    lector.nextLine();
                    if (opcion >= 0 && opcion <= 4) {
                        break;
                    } else {
                        System.out.println("❌ Opción no válida. Debe ser entre 0 y 4");
                    }
                } else {
                    System.out.println("❌ Debes introducir un número entero");
                    lector.nextLine();
                }
            }
            
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
            
        } while (opcion != 0);
        
        lector.close();
    }
}
```

## 2. Práctica 7: Control de datos en todos los programas

### 2.1 Objetivos y tareas

**Objetivo:**
Modificar todos los programas realizados hasta ahora para que implementen un **control robusto de los datos introducidos por teclado**.

**Tareas a realizar:**

- Revisar cada programa desarrollado hasta este punto.
- Añadir validación para todas las entradas del usuario.
- Incluir mensajes de error informativos y claros.
- Probar exhaustivamente con entradas incorrectas y no válidas.

### 2.2 Ejemplo de implementación

**Versión sin control de datos (NO RECOMENDADO):**

```java
Scanner lector = new Scanner(System.in);
System.out.print("Introduce un número: ");
int num = lector.nextInt(); // Puede fallar si la entrada no es un entero
```

**Versión con control de datos (RECOMENDADO):**

```java
Scanner lector = new Scanner(System.in);
int num;

do {
    System.out.print("Introduce un número entero: ");
    while (!lector.hasNextInt()) {
        System.out.println("⚠️  Error: Solo se aceptan números enteros.");
        System.out.print("Inténtalo de nuevo: ");
        lector.next(); // Consumir entrada inválida
    }
    num = lector.nextInt();
} while (num < 0); // Ejemplo de validación adicional

System.out.println("Número válido introducido: " + num);
lector.close();
```

> [!IMPORTANT]
> Esta práctica es esencial para desarrollar programas robustos que no fallen cuando el usuario introduce datos incorrectos.

### 2.3 Criterios de evaluación

- **Funcionalidad:** El programa debe funcionar correctamente tanto con entradas válidas como inválidas.
- **Mensajes claros:** El usuario debe comprender qué ha hecho mal y cómo corregirlo.
- **Robustez:** El programa nunca debe finalizar inesperadamente por una entrada incorrecta.
- **Código limpio:** Uso adecuado de los métodos de validación y estructura clara.

> [!CAUTION]
> Prueba tus programas con diferentes tipos de entradas: letras cuando se esperan números, números fuera de rango, etc. El objetivo es que el programa nunca se bloquee ni lance excepciones inesperadas.

<p align="center">📚 <em>Fin del apartado UT2.2 - Programación estructurada: Entrada por teclado y control de datos</em></p>
