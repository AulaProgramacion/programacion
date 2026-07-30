# UT3.5 Expresiones regulares en Java (EXTRA)

## 📋 Índice de contenidos

1. [Introducción a las expresiones regulares](#1-introducci%C3%B3n-a-las-expresiones-regulares)
    1. [¿Qué son las expresiones regulares?](#11-qu%C3%A9-son-las-expresiones-regulares)
    2. [Importancia y aplicaciones comunes](#12-importancia-y-aplicaciones-comunes)
    3. [Conceptos fundamentales](#13-conceptos-fundamentales)
    4. [Beneficios del uso de expresiones regulares](#14-beneficios-del-uso-de-expresiones-regulares)
2. [Sintaxis básica de expresiones regulares](#2-sintaxis-b%C3%A1sica-de-expresiones-regulares)
    1. [Metacaracteres](#21-metacaracteres)
    2. [Caracteres literales](#22-caracteres-literales)
    3. [Grupos y capturas](#23-grupos-y-capturas)
    4. [Cuantificadores](#24-cuantificadores)
    5. [Conjuntos de caracteres](#25-conjuntos-de-caracteres)
    6. [Otros metacaracteres útiles](#26-otros-metacaracteres-%C3%BAtiles)
    7. [Disyunción y conjunción](#27-disyunci%C3%B3n-y-conjunci%C3%B3n)
3. [Clases e interfaces en Java](#3-clases-e-interfaces-en-java)
    1. [java.util.regex.Pattern](#31-javautilregexpattern)
    2. [java.util.regex.Matcher](#32-javautilregexmatcher)
    3. [java.util.regex.PatternSyntaxException](#33-javautilregexpatternsyntaxexception)
4. [Uso de Pattern y Matcher](#4-uso-de-pattern-y-matcher)
    1. [Búsqueda de patrones en cadenas](#41-b%C3%BAsqueda-de-patrones-en-cadenas)
    2. [Validación de formatos específicos](#42-validaci%C3%B3n-de-formatos-espec%C3%ADficos)
    3. [Sustitución de texto](#43-sustituci%C3%B3n-de-texto)
    4. [División de cadenas](#44-divisi%C3%B3n-de-cadenas)
    5. [Uso de flags](#45-uso-de-flags)
5. [Buenas prácticas](#5-buenas-pr%C3%A1cticas)
    1. [Escritura clara y documentación](#51-escritura-clara-y-documentaci%C3%B3n)
    2. [Uso de nombres significativos](#52-uso-de-nombres-significativos)
    3. [Optimización de la eficiencia](#53-optimizaci%C3%B3n-de-la-eficiencia)

## 1. Introducción a las expresiones regulares

### 1.1 ¿Qué son las expresiones regulares?

Las **expresiones regulares**, también conocidas como **regex** o **regexp**, son patrones utilizados para la búsqueda y manipulación de cadenas de texto. Se pueden utilizar para comprobar si una cadena cumple un patrón específico, para encontrar coincidencias dentro de una cadena, o para sustituir fragmentos de texto.

> [!NOTE]
> Las expresiones regulares son una herramienta potente y universal presente en la mayoría de lenguajes de programación. Aunque pueden parecer complejas al principio, su dominio te permitirá resolver problemas de texto de manera muy eficiente.

**Ejemplo básico:**

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class RegexBasico {
    public static void main(String[] args) {
        String texto = "Bienvenido al curso de DAW!";
        String patron = "DAW";

        Pattern pattern = Pattern.compile(patron);
        Matcher matcher = pattern.matcher(texto);

        boolean encontrado = matcher.find();
        System.out.println("Patrón encontrado: " + encontrado); // true
    }
}
```

### 1.2 Importancia y aplicaciones comunes

Las expresiones regulares son esenciales en muchos ámbitos de la programación y el tratamiento de datos:

- **🔍 Validación de datos**: Verificar que las entradas del usuario (emails, teléfonos, códigos postales) sean válidas
- **🔄 Búsqueda y sustitución**: Encontrar y reemplazar substrings dentro de cadenas de texto
- **📊 Extracción de datos**: Extraer información específica de textos complejos, como logs o documentos HTML
- **🧹 Limpieza de datos**: Formatear y normalizar información textual

**Ejemplo de validación de email:**

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class ValidacionEmail {
    public static void main(String[] args) {
        String email = "ejemplo@dominio.com";
        String patron = "^[A-Za-z0-9+_.-]+@(.+)$";

        Pattern pattern = Pattern.compile(patron);
        Matcher matcher = pattern.matcher(email);

        boolean esValido = matcher.matches();
        System.out.println("Email válido: " + esValido); // true
    }
}
```

### 1.3 Conceptos fundamentales

Las expresiones regulares funcionan definiendo un **patrón** que describe un conjunto de cadenas posibles. Este patrón se compara con una cadena de texto para ver si hay coincidencia.

**Elementos clave:**

- **Patrón**: La expresión regular que define qué buscamos
- **Texto objetivo**: La cadena donde buscamos el patrón
- **Coincidencia**: Cuando el patrón se encuentra en el texto
- **Captura**: Extraer partes específicas del texto que coincide

**Ejemplo de múltiples coincidencias:**

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class MultiplesCoincidencias {
    public static void main(String[] args) {
        String texto = "Java es genial. Java es potente. Java está en todas partes.";
        String patron = "\\bJava\\b";

        Pattern pattern = Pattern.compile(patron);
        Matcher matcher = pattern.matcher(texto);

        int contador = 0;
        while (matcher.find()) {
            contador++;
            System.out.println("Encontrado en índice: " + matcher.start());
        }
        System.out.println("Total encontrado: " + contador + " veces");
    }
}
```

### 1.4 Beneficios del uso de expresiones regulares

- **⚡ Eficiencia**: Permiten procesar grandes volúmenes de texto de manera rápida
- **🔧 Flexibilidad**: Son muy versátiles para una amplia variedad de tareas
- **📝 Reducción de código**: Simplifican la lógica de procesamiento de texto
- **🌐 Universalidad**: El conocimiento se transfiere entre diferentes lenguajes

**Ejemplo de sustitución de texto:**

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class SustitucionTexto {
    public static void main(String[] args) {
        String texto = "Hola, Mundo!";
        String patron = "Mundo";
        String reemplazo = "DAW";

        Pattern pattern = Pattern.compile(patron);
        Matcher matcher = pattern.matcher(texto);

        String nuevoTexto = matcher.replaceAll(reemplazo);
        System.out.println(nuevoTexto); // "Hola, DAW!"
    }
}
```

## 2. Sintaxis básica de expresiones regulares

### 2.1 Metacaracteres

Los **metacaracteres** son caracteres especiales que tienen significado propio dentro de una expresión regular. No se pueden utilizar literalmente a menos que se escapen con una barra invertida (`\`).

> [!WARNING]
> **Importante:** En Java, para representar el símbolo `\` en un String se debe escapar, por tanto debemos escribir `\\`.

**Metacaracteres básicos:**

| Metacarácter | Descripción |
| :-- | :-- |
| `.` | Coincide con cualquier carácter excepto nueva línea |
| `^` | Coincide con el comienzo de la cadena |
| `$` | Coincide con el final de la cadena |
| `*` | Coincide con cero o más repeticiones del patrón anterior |
| `+` | Coincide con una o más repeticiones del patrón anterior |
| `?` | Coincide con cero o una repetición del patrón anterior |
| `{n}` | Coincide exactamente con n repeticiones |
| `{n,}` | Coincide con n o más repeticiones |
| `{n,m}` | Coincide con entre n y m repeticiones |
| `[]` | Coincide con cualquiera de los caracteres entre corchetes |
| `()` | Define un grupo y captura |
| `\|` | Opera como OR lógico entre patrones |
| `\` | Escape de metacaracteres |

**Metacaracteres de clases de caracteres:**

| Metacarácter | Descripción |
| :-- | :-- |
| `\d` | Coincide con cualquier dígito (`[0-9]`) |
| `\D` | Coincide con cualquier carácter que no sea dígito |
| `\w` | Coincide con cualquier carácter de palabra (`[a-zA-Z_0-9]`) |
| `\W` | Coincide con cualquier carácter que no sea de palabra |
| `\s` | Coincide con cualquier espacio en blanco |
| `\S` | Coincide con cualquier carácter que no sea espacio en blanco |

**Ejemplo:**

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class EjemploMetacaracteres {
    public static void main(String[] args) {
        String texto = "abc123";
        String patron = "abc\\d+"; // abc seguido de uno o más dígitos

        Pattern pattern = Pattern.compile(patron);
        Matcher matcher = pattern.matcher(texto);

        boolean encontrado = matcher.find();
        System.out.println("Patrón encontrado: " + encontrado); // true
    }
}
```

### 2.2 Caracteres literales

Los **caracteres literales** son aquellos que representan a sí mismos dentro de la expresión regular. Incluyen letras, números y algunos símbolos.

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class CaracteresLiterales {
    public static void main(String[] args) {
        String texto = "Hola, mundo!";
        String patron = "Hola, mundo!";

        Pattern pattern = Pattern.compile(patron);
        Matcher matcher = pattern.matcher(texto);

        boolean encontrado = matcher.find();
        System.out.println("Patrón encontrado: " + encontrado); // true
    }
}
```

### 2.3 Grupos y capturas

Los **paréntesis `()`** se utilizan para agrupar partes de una expresión regular. También permiten capturar el texto que coincide con el grupo para utilizarlo más tarde.

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class GruposYCapturas {
    public static void main(String[] args) {
        String texto = "2024-08-02";
        String patron = "(\\d{4})-(\\d{2})-(\\d{2})";

        Pattern pattern = Pattern.compile(patron);
        Matcher matcher = pattern.matcher(texto);

        if (matcher.find()) {
            System.out.println("Fecha completa: " + matcher.group(0)); // 2024-08-02
            System.out.println("Año: " + matcher.group(1));            // 2024
            System.out.println("Mes: " + matcher.group(2));             // 08
            System.out.println("Día: " + matcher.group(3));             // 02
        }
    }
}
```

### 2.4 Cuantificadores

Los **cuantificadores** especifican el número de ocurrencias del patrón anterior que se permiten.

| Cuantificador | Descripción |
| :-- | :-- |
| `*` | Cero o más veces |
| `+` | Una o más veces |
| `?` | Cero o una vez |
| `{n}` | Exactamente n veces |
| `{n,}` | Al menos n veces |
| `{n,m}` | Entre n y m veces |

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class EjemploCuantificadores {
    public static void main(String[] args) {
        String texto = "abccc";
        String patron = "abc{3}"; // abc seguido de exactamente 3 c's

        Pattern pattern = Pattern.compile(patron);
        Matcher matcher = pattern.matcher(texto);

        boolean encontrado = matcher.find();
        System.out.println("Patrón encontrado: " + encontrado); // true
    }
}
```

### 2.5 Conjuntos de caracteres

Los **conjuntos de caracteres** permiten definir un conjunto de posibles caracteres en una posición específica de la cadena.

| Conjunto | Descripción |
| :-- | :-- |
| `[abc]` | Coincide con `a`, `b` o `c` |
| `[^abc]` | Coincide con cualquier carácter excepto `a`, `b` o `c` |
| `[a-z]` | Coincide con cualquier letra minúscula |
| `[A-Z]` | Coincide con cualquier letra mayúscula |
| `[0-9]` | Coincide con cualquier dígito |
| `[a-zA-Z]` | Coincide con cualquier letra |
| `[a-zA-Z0-9]` | Coincide con cualquier letra o dígito |

> [!IMPORTANT]
> Los conjuntos de caracteres coinciden con **exactamente un carácter** de las opciones especificadas.

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class ConjuntosCaracteres {
    public static void main(String[] args) {
        String texto = "a1b2c3";
        String patron = "[a-z][0-9]"; // letra minúscula seguida de dígito

        Pattern pattern = Pattern.compile(patron);
        Matcher matcher = pattern.matcher(texto);

        while (matcher.find()) {
            System.out.println("Coincidencia: " + matcher.group());
        }
        // Output: a1, b2, c3
    }
}
```

### 2.6 Otros metacaracteres útiles

| Metacarácter | Descripción |
| :-- | :-- |
| `\b` | Coincide con una frontera de palabra |
| `\B` | Coincide con una posición que no es frontera de palabra |
| `\A` | Coincide con el comienzo de la cadena |
| `\Z` | Coincide con el final de la cadena |
| `\G` | Coincide donde terminó la última coincidencia |

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class FronterasPalabra {
    public static void main(String[] args) {
        String texto = "Java es genial y JavaScript también";
        String patron = "\\bJava\\b"; // Solo la palabra completa "Java"

        Pattern pattern = Pattern.compile(patron);
        Matcher matcher = pattern.matcher(texto);

        while (matcher.find()) {
            System.out.println("Encontrado en posición: " + matcher.start());
        }
        // Solo encuentra "Java", no "JavaScript"
    }
}
```

### 2.7 Disyunción y conjunción

**Disyunción**: Utiliza el carácter `|` para definir opciones alternativas.

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class Disyuncion {
    public static void main(String[] args) {
        String texto = "xabc";
        String patron = "a|b|c"; // coincide con a, b o c

        Pattern pattern = Pattern.compile(patron);
        Matcher matcher = pattern.matcher(texto);

        while (matcher.find()) {
            System.out.println("Coincidencia: " + matcher.group());
        }
        // Output: a, b, c
    }
}
```

**Conjunción**: Utiliza `&&` para definir conjunciones en conjuntos de caracteres.

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class Conjuncion {
    public static void main(String[] args) {
        String texto = "a B y Z 1 Y";
        String patron = "[a-zA-Z0-9&&[^Yy]]"; // alfanumérico excepto Y e y

        Pattern pattern = Pattern.compile(patron);
        Matcher matcher = pattern.matcher(texto);

        while (matcher.find()) {
            System.out.println("Coincidencia: " + matcher.group());
        }
        // Output: a, B, Z, 1 (pero no Y ni y)
    }
}
```

## 3. Clases e interfaces en Java

### 3.1 java.util.regex.Pattern

La clase `Pattern` representa una expresión regular compilada en un patrón que se puede utilizar para la coincidencia de cadenas de texto.

**Métodos principales:**

- `compile(String regex)`: Compila la expresión regular en un patrón
- `compile(String regex, int flags)`: Compila con flags opcionales
- `pattern()`: Retorna la expresión regular original
- `matches(String regex, CharSequence input)`: Comprueba coincidencia completa

```java
import java.util.regex.Pattern;

public class EjemploPattern {
    public static void main(String[] args) {
        String regex = "\\d+";
        Pattern pattern = Pattern.compile(regex);

        String texto = "123";
        boolean coincide = pattern.matcher(texto).matches();
        System.out.println("Coincidencia completa: " + coincide); // true
        
        // Método estático directo
        boolean coincideDirecto = Pattern.matches("\\d+", "456");
        System.out.println("Coincidencia directa: " + coincideDirecto); // true
    }
}
```

### 3.2 java.util.regex.Matcher

La clase `Matcher` se utiliza para operar sobre una cadena de entrada utilizando un patrón `Pattern`.

**Métodos principales:**

- `find()`: Busca la siguiente coincidencia
- `group()`: Retorna la coincidencia más reciente
- `start()` / `end()`: Índices de inicio y final de la coincidencia
- `matches()`: Comprueba si toda la cadena coincide
- `lookingAt()`: Comprueba si el comienzo coincide
- `replaceAll(String replacement)`: Sustituye todas las coincidencias

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class EjemploMatcher {
    public static void main(String[] args) {
        String texto = "ab12cd34";
        String regex = "\\d+";
        
        Pattern pattern = Pattern.compile(regex);
        Matcher matcher = pattern.matcher(texto);

        while (matcher.find()) {
            System.out.println("Coincidencia: " + matcher.group() + 
                             " en posición " + matcher.start() + 
                             "-" + matcher.end());
        }
        // Output: 12 en posición 2-4, 34 en posición 6-8
    }
}
```

### 3.3 java.util.regex.PatternSyntaxException

Esta excepción se lanza cuando hay un error de sintaxis en una expresión regular.

**Métodos principales:**

- `getDescription()`: Descripción del error
- `getIndex()`: Posición del error
- `getPattern()`: Expresión regular que causó el error
- `getMessage()`: Mensaje detallado

```java
import java.util.regex.Pattern;
import java.util.regex.PatternSyntaxException;

public class EjemploExcepcion {
    public static void main(String[] args) {
        String regex = "\\d+*"; // Error de sintaxis
        try {
            Pattern.compile(regex);
        } catch (PatternSyntaxException e) {
            System.out.println("Error de sintaxis: " + e.getDescription());
            System.out.println("Posición del error: " + e.getIndex());
            System.out.println("Expresión: " + e.getPattern());
        }
    }
}
```

## 4. Uso de Pattern y Matcher

### 4.1 Búsqueda de patrones en cadenas

El uso combinado de `Pattern` y `Matcher` permite buscar patrones dentro de cadenas de texto de manera eficiente.

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class BusquedaPatrones {
    public static void main(String[] args) {
        String texto = "La fecha es 2024-08-02 y la hora es 14:35.";
        String regex = "\\d{4}-\\d{2}-\\d{2}";

        Pattern pattern = Pattern.compile(regex);
        Matcher matcher = pattern.matcher(texto);

        if (matcher.find()) {
            System.out.println("Fecha encontrada: " + matcher.group());
            System.out.println("En posición: " + matcher.start() + "-" + matcher.end());
        }
    }
}
```

### 4.2 Validación de formatos específicos

Las expresiones regulares son ideales para validar formatos como emails, teléfonos, etc.

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;
import java.util.Scanner;

public class ValidacionFormatos {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        // Patrones de validación
        String emailRegex = "^[A-Za-z0-9+_.-]+@[A-Za-z0-9+_.-]+\\.[a-z]{2,5}$";
        String telefonoRegex = "^[679]\\d{8}$"; // Móvil español
        String dniRegex = "^\\d{8}[TRWAGMYFPDXBNJZSQVHLCKE]$";
        
        Pattern emailPattern = Pattern.compile(emailRegex);
        Pattern telefonoPattern = Pattern.compile(telefonoRegex);
        Pattern dniPattern = Pattern.compile(dniRegex);
        
        System.out.print("Introduce un email: ");
        String email = scanner.nextLine();
        System.out.println("Email válido: " + emailPattern.matcher(email).matches());
        
        System.out.print("Introduce un teléfono móvil: ");
        String telefono = scanner.nextLine();
        System.out.println("Teléfono válido: " + telefonoPattern.matcher(telefono).matches());
        
        System.out.print("Introduce un DNI: ");
        String dni = scanner.nextLine().toUpperCase();
        System.out.println("DNI válido: " + dniPattern.matcher(dni).matches());
        
        scanner.close();
    }
}
```

### 4.3 Sustitución de texto

Las expresiones regulares permiten realizar sustituciones complejas de texto.

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class SustitucionTexto {
    public static void main(String[] args) {
        String texto = "Hoy es 02/08/2024 y mañana será 03/08/2024";
        String regex = "(\\d{2})/(\\d{2})/(\\d{4})";
        String reemplazo = "$3-$2-$1"; // año-mes-día
        
        Pattern pattern = Pattern.compile(regex);
        Matcher matcher = pattern.matcher(texto);
        
        String resultado = matcher.replaceAll(reemplazo);
        System.out.println("Original: " + texto);
        System.out.println("Resultado: " + resultado);
        
        // También podemos hacer sustituciones más complejas
        String textoHtml = "<p>Hola</p> <b>mundo</b>";
        String sinHtml = textoHtml.replaceAll("<[^>]+>", "");
        System.out.println("Sin HTML: " + sinHtml); // "Hola mundo"
    }
}
```

### 4.4 División de cadenas

Las expresiones regulares se pueden utilizar para dividir cadenas con delimitadores específicos.

```java
import java.util.regex.Pattern;

public class DivisionCadenas {
    public static void main(String[] args) {
        String texto = "manzana, plátano; naranja : kiwi";
        String regex = "[,;:]\\s*"; // coma, punto y coma o dos puntos, seguido de espacios opcionales
        
        Pattern pattern = Pattern.compile(regex);
        String[] frutas = pattern.split(texto);
        
        System.out.println("Frutas encontradas:");
        for (int i = 0; i < frutas.length; i++) {
            System.out.println((i + 1) + ". " + frutas[i].trim());
        }
        
        // También podemos usar el método split directamente en String
        String csv = "Juan,25,Programador,Madrid";
        String[] datos = csv.split(",");
        System.out.println("\nDatos CSV:");
        for (String dato : datos) {
            System.out.println("- " + dato);
        }
    }
}
```

### 4.5 Uso de flags

Los flags modifican cómo se realiza la búsqueda en las expresiones regulares.

**Flags comunes:**

- `Pattern.CASE_INSENSITIVE`: Ignora mayúsculas/minúsculas
- `Pattern.LITERAL`: Caracteres especiales como literales
- `Pattern.MULTILINE`: `^` y `$` coinciden con inicio/final de línea
- `Pattern.DOTALL`: `.` coincide con cualquier carácter incluyendo nueva línea

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class UsoFlags {
    public static void main(String[] args) {
        String texto = "Hola\nMUNDO\nhola mundo";
        
        // Sin flags
        Pattern patron1 = Pattern.compile("mundo");
        Matcher matcher1 = patron1.matcher(texto);
        System.out.println("Sin flags - encontrado: " + matcher1.find());
        
        // Con CASE_INSENSITIVE
        Pattern patron2 = Pattern.compile("mundo", Pattern.CASE_INSENSITIVE);
        Matcher matcher2 = patron2.matcher(texto);
        int contador = 0;
        while (matcher2.find()) {
            contador++;
            System.out.println("Coincidencia " + contador + ": " + matcher2.group());
        }
        
        // Con MULTILINE
        String textoLineas = "inicio\nmedio\nfinal";
        Pattern patron3 = Pattern.compile("^[a-z]+$", Pattern.MULTILINE);
        Matcher matcher3 = patron3.matcher(textoLineas);
        
        while (matcher3.find()) {
            System.out.println("Línea completa: " + matcher3.group());
        }
    }
}
```

## 5. Buenas prácticas

### 5.1 Escritura clara y documentación

Las expresiones regulares pueden ser difíciles de leer. Es importante documentarlas y dividir las complejas en partes manejables.

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class DocumentacionRegex {
    public static void main(String[] args) {
        String email = "usuario@dominio.com";
        
        // Regex documentada para validación de email
        String parteLocal = "^[A-Za-z0-9+_.-]+";     // Parte antes del @
        String arroba = "@";                          // El símbolo @
        String dominio = "[A-Za-z0-9+_.-]+";         // Nombre del dominio
        String extension = "\\.[a-z]{2,5}$";         // Extensión del dominio
        
        String emailRegex = parteLocal + arroba + dominio + extension;
        
        Pattern pattern = Pattern.compile(emailRegex);
        Matcher matcher = pattern.matcher(email);
        
        boolean esValido = matcher.matches();
        System.out.println("Email válido: " + esValido);
        
        // También podemos usar comentarios en regex complejas (modo verbose)
        String regexCompleja = "(?x)" +        // Modo verbose
                              "^" +            // Inicio de cadena
                              "[A-Za-z0-9+_.-]+" + // Parte local
                              "@" +            // Arroba
                              "[A-Za-z0-9+_.-]+" + // Dominio
                              "\\.[a-z]{2,5}" +    // Extensión
                              "$";             // Final de cadena
    }
}
```

### 5.2 Uso de nombres significativos

Definir patrones con nombres significativos mejora la legibilidad del código.

```java
import java.util.regex.Pattern;

public class NombresSignificativos {
    // Constantes para patrones comunes
    private static final String REGEX_EMAIL = "^[A-Za-z0-9+_.-]+@[A-Za-z0-9+_.-]+\\.[a-z]{2,5}$";
    private static final String REGEX_TELEFONO_MOVIL = "^[679]\\d{8}$";
    private static final String REGEX_DNI = "^\\d{8}[TRWAGMYFPDXBNJZSQVHLCKE]$";
    private static final String REGEX_FECHA_ES = "^\\d{2}/\\d{2}/\\d{4}$";
    private static final String REGEX_CODIGO_POSTAL = "^\\d{5}$";
    
    public static void main(String[] args) {
        String[] datosUsuario = {
            "juan@email.com",
            "666123456",
            "12345678Z",
            "02/08/2024",
            "28001"
        };
        
        Pattern[] patrones = {
            Pattern.compile(REGEX_EMAIL),
            Pattern.compile(REGEX_TELEFONO_MOVIL),
            Pattern.compile(REGEX_DNI),
            Pattern.compile(REGEX_FECHA_ES),
            Pattern.compile(REGEX_CODIGO_POSTAL)
        };
        
        String[] nombres = {
            "Email", "Teléfono", "DNI", "Fecha", "Código Postal"
        };
        
        for (int i = 0; i < datosUsuario.length; i++) {
            boolean valido = patrones[i].matcher(datosUsuario[i]).matches();
            System.out.println(nombres[i] + " (" + datosUsuario[i] + "): " + 
                             (valido ? "✓ Válido" : "✗ Inválido"));
        }
    }
}
```

### 5.3 Optimización de la eficiencia

Para mejorar el rendimiento, especialmente con grandes volúmenes de datos:

- Compilar el patrón una sola vez y reutilizarlo
- Evitar cuantificadores costosos como `.*`
- Usar patrones específicos en lugar de genéricos

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class OptimizacionRegex {
    // Compilar una sola vez y reutilizar
    private static final Pattern EMAIL_PATTERN = 
        Pattern.compile("^[A-Za-z0-9+_.-]+@[A-Za-z0-9+_.-]+\\.[a-z]{2,5}$");
    
    public static void main(String[] args) {
        String[] emails = {
            "usuario@dominio.com",
            "email-invalido@",
            "otro.usuario@empresa.es",
            "correo@universidad.edu",
            "sin-dominio@"
        };
        
        // Eficiente: reutilizar el patrón compilado
        long inicio = System.nanoTime();
        for (String email : emails) {
            Matcher matcher = EMAIL_PATTERN.matcher(email);
            boolean valido = matcher.matches();
            System.out.println(email + ": " + (valido ? "Válido" : "Inválido"));
        }
        long fin = System.nanoTime();
        
        System.out.println("Tiempo transcurrido: " + (fin - inicio) / 1_000_000.0 + " ms");
        
        // Ejemplo de patrón específico vs genérico
        String texto = "Buscar números: 123, 456, 789";
        
        // Más específico y eficiente
        Pattern patronEspecifico = Pattern.compile("\\d+");
        
        // Menos eficiente para este caso
        Pattern patronGenerico = Pattern.compile(".*\\d+.*");
        
        Matcher matcher = patronEspecifico.matcher(texto);
        System.out.println("\nNúmeros encontrados:");
        while (matcher.find()) {
            System.out.println("- " + matcher.group());
        }
    }
}
```

> [!IMPORTANT]
> Las expresiones regulares son una herramienta muy potente para el procesamiento de texto. Su dominio te permitirá resolver problemas complejos de validación, búsqueda y manipulación de datos de manera eficiente. Aunque pueden parecer complejas al principio, con práctica se convierten en una herramienta indispensable para cualquier programador.

<p align="center">📚 <em>Fin del apartado UT3.5 - Expresiones regulares en Java</em></p>
