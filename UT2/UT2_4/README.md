# UT2.4 Pruebas y Depuración

## 📋 Índice de contenidos

1. [Introducción a las pruebas y la depuración](#1-introducci%C3%B3n-a-las-pruebas-y-la-depuraci%C3%B3n)
2. [¿Qué es la depuración?](#2-qu%C3%A9-es-la-depuraci%C3%B3n)
3. [¿Qué es el testing?](#3-qu%C3%A9-es-el-testing)
4. [Diferencias y relación entre pruebas y depuración](#4-diferencias-y-relaci%C3%B3n-entre-pruebas-y-depuraci%C3%B3n)
5. [El proceso de depuración paso a paso](#5-el-proceso-de-depuraci%C3%B3n-paso-a-paso)
6. [Herramientas de depuración en NetBeans](#6-herramientas-de-depuraci%C3%B3n-en-netbeans)
    1. [Identificación del error](#61-identificaci%C3%B3n-del-error)
    2. [Análisis de código](#62-an%C3%A1lisis-de-c%C3%B3digo)
    3. [Uso de breakpoints](#63-uso-de-breakpoints)
    4. [Inspección de variables](#64-inspecci%C3%B3n-de-variables)
    5. [Ejecución paso a paso](#65-ejecuci%C3%B3n-paso-a-paso)
    6. [Otras herramientas útiles](#66-otras-herramientas-%C3%BAtiles)
7. [Documentación y registro de la depuración](#7-documentaci%C3%B3n-y-registro-de-la-depuraci%C3%B3n)
8. [Buenas prácticas en depuración](#8-buenas-pr%C3%A1cticas-en-depuraci%C3%B3n)
9. [Ejemplo práctico de depuración](#9-ejemplo-pr%C3%A1ctico-de-depuraci%C3%B3n)
10. [Prácticas propuestas](#10-pr%C3%A1cticas-propuestas)

## 1. Introducción a las pruebas y la depuración

### 1.1 Pruebas (Testing)

Las **pruebas** (*testing*) son fundamentales para asegurar que el software cumple con las especificaciones y funciona correctamente en diferentes situaciones.

**Objetivos de las pruebas:**

- **Verificación del cumplimiento** de requisitos funcionales
- **Validación del comportamiento** en diferentes escenarios
- **Detección proactiva** de posibles errores antes del despliegue
- **Garantía de calidad** antes de la entrega al usuario final

**Tipos de pruebas:**


| Tipo de prueba | Descripción | Ejemplo |
| :-- | :-- | :-- |
| **Unitarias** | Prueban componentes individuales | Probar una función específica |
| **Integración** | Prueban la interacción entre módulos | Comunicación entre clases |
| **Sistema** | Prueban el sistema completo | Funcionamiento global |
| **Aceptación** | Validan requisitos del usuario | Casos de uso reales |

> [!NOTE]
> La parte de testing se trabajará con más detalle en el módulo profesional de **Entornos de Desarrollo**.

### 1.2 Depuración (Debugging)

La **depuración** (*debugging*) se centra en identificar, analizar y corregir errores en el código. En el módulo profesional de **Programación**, nos enfocaremos específicamente en la depuración.

**Características de la depuración:**

- **🔍 Identificación**: Localizar dónde se produce el error
- **🧪 Análisis**: Comprender la causa raíz del problema
- **🔧 Resolución**: Implementar la solución adecuada
- **✅ Verificación**: Confirmar que el error se ha corregido sin crear nuevos

> [!IMPORTANT]
> Este proceso es crucial para garantizar la calidad del código y el correcto funcionamiento del software desarrollado.

## 2. ¿Qué es la depuración?

La **depuración** es el proceso sistemático de encontrar, aislar y resolver errores de codificación (bugs) en un programa. Su objetivo es garantizar que el software funcione correctamente y cumpla con las especificaciones establecidas.

**🎯 Objetivo principal:**
Asegurar que el programa funcione correctamente según las especificaciones establecidas.

**🛠️ Herramientas necesarias:**
Los **IDE** (Entornos de Desarrollo Integrados) disponen de potentes herramientas de depuración que facilitan este proceso.

**📊 Tipos de errores comunes:**


| Tipo de error | Descripción | Ejemplo |
| :-- | :-- | :-- |
| **Sintaxis** | Violación de reglas del lenguaje | `IO.pritln()` (falta 'n') |
| **Lógico** | Error en la lógica del programa | Condición incorrecta en `if` |
| **Ejecución** | Error durante la ejecución | División por cero |
| **Semántico** | Código sintácticamente correcto pero incorrecto conceptualmente | Usar `=` en lugar de `==` |

> [!WARNING]
> Un programa que compila correctamente no garantiza que funcione como se espera. Los errores lógicos pueden ser los más difíciles de detectar.

La depuración ayuda a:

- Descubrir la causa raíz de los errores.
- Mejorar la estabilidad y fiabilidad del software.
- Optimizar el rendimiento y la experiencia de usuario.


## 3. ¿Qué es el testing?

El **testing** consiste en ejecutar el programa en diferentes situaciones para comprobar que cumple los requisitos y funciona correctamente. Permite identificar defectos, tanto en condiciones normales como anómalas, y desencadena el proceso de depuración cuando se detectan fallos.

- **Testing dinámico**: ejecuta el código y comprueba su comportamiento.
- **Testing estático**: analiza el código sin ejecutarlo (por ejemplo, revisiones de código o análisis estático).

> [!TIP]
> El testing descubre defectos, la depuración los elimina.

## 4. Diferencias y relación entre pruebas y depuración

| Aspecto | Testing (Pruebas) | Depuración (Debugging) |
| :-- | :-- | :-- |
| Objetivo | Descubrir defectos | Eliminar defectos |
| Método | Ejecutar y analizar resultados | Analizar y corregir código |
| Resultado | Informe de fallos | Corrección de errores |
| Relación | Detecta el fallo | Encuentra y soluciona la causa |

- El testing **provoca** la aparición de errores.
- La depuración **analiza** y **corrige** esos errores.


## 5. El proceso de depuración paso a paso

La depuración suele seguir una serie de pasos estructurados:

1. **Reproducir el error**: Ejecutar el programa en las condiciones que provocan el fallo.
2. **Identificar el error**: Localizar el punto exacto donde ocurre el problema.
3. **Determinar la causa raíz**: Analizar el código y los datos para entender por qué ocurre el error.
4. **Corregir el error**: Modificar el código para solucionar el problema.
5. **Probar la corrección**: Ejecutar el programa de nuevo para asegurarse de que el error ha desaparecido y no se han introducido nuevos fallos.
6. **Documentar el proceso**: Registrar el error, la causa, la solución y las pruebas realizadas.

> [!TIP]
> Al depurar, adopta una mentalidad "saboteadora": desconfía de los resultados y busca activamente posibles errores.

## 6. Herramientas de depuración en NetBeans

Los entornos de desarrollo integrados (IDE) como **NetBeans** ofrecen potentes herramientas para facilitar la depuración del código Java:

### 6.1 Identificación del error

<img src="assets/imatge4.jpg" alt="Imatge 4">

El primer paso en cualquier proceso de depuración es la **identificación clara del error**. NetBeans facilita esta tarea mediante varios mecanismos:

**🚨 Consola de errores:**

- Analiza los mensajes de error mostrados en la consola de NetBeans
- Los mensajes incluyen información sobre el tipo y ubicación del problema
- Proporciona trazas de pila (*stack traces*) con la secuencia de llamadas

**🎨 Indicadores visuales:**

- El IDE marca con colores y símbolos las líneas problemáticas
- Subrayado rojo para errores de sintaxis
- Iconos de advertencia para problemas potenciales

**📝 Tipos de mensajes:**

```java
// Ejemplo de código con error
public class EjemploError {
    public static void main(String[] args) {
        int numero = 10;
        int divisor = 0;
        int resultado = numero / divisor; // ¡Error de ejecución!
        IO.println(resultado);
    }
}
```

**Mensaje en consola:**

```
Exception in thread "main" java.lang.ArithmeticException: / by zero
    at EjemploError.main(EjemploError.java:5)
```

> [!TIP]
> Lee siempre los mensajes de error completamente, ya que a menudo contienen información valiosa sobre la causa del problema.

### 6.2 Análisis de código

<img src="assets/imatge5.jpg" alt="Imatge 5">

Una vez identificado el error, es necesario realizar un **análisis exhaustivo del código**. Este proceso incluye:

**🔍 Revisión de la lógica:**

- Asegurar que el código Java sigue los flujos esperados
- Verificar que los algoritmos implementados son correctos
- Comprobar que las operaciones se realizan en el orden adecuado

**✅ Verificación de condiciones:**

- Comprobar que las estructuras condicionales (`if`, `else`, `switch`) funcionan correctamente
- Validar que las expresiones booleanas evalúan como se espera
- Verificar los rangos de valores en las comparaciones

**🔄 Análisis de bucles:**

- Revisar bucles (`for`, `while`, `do-while`) para evitar bucles infinitos
- Comprobar las condiciones de entrada y salida
- Verificar que las variables de control se modifican correctamente

**📊 Validación de tipos de datos:**

- Confirmar que las variables tienen los tipos adecuados
- Verificar conversiones de tipos implícitas y explícitas
- Comprobar que los rangos de valores son apropiados

**🔐 Comprobación de permisos y ámbito:**

- Verificar que las variables y métodos son accesibles desde el punto donde se utilizan
- Comprobar el ámbito (*scope*) de las variables
- Validar los modificadores de acceso (`public`, `private`, `protected`)



### 6.3 Uso de breakpoints

<img src="assets/imatge6.jpg" alt="Imatge 6">

Los **breakpoints** (puntos de ruptura) permiten pausar la ejecución del programa en una línea específica para analizar el estado del programa en ese momento.

**🎯 Propósito de los breakpoints:**

- Analizar el estado del programa en un punto específico
- Examinar valores de variables en tiempo de ejecución
- Verificar el flujo de ejecución paso a paso
- Identificar dónde se producen comportamientos inesperados

**Cómo colocar un breakpoint en NetBeans:**

1. Haz clic en la línea de código deseada y selecciona "Toggle Line Breakpoint" o pulsa `Ctrl+F8`.
2. Ejecuta el programa en modo depuración (`Ctrl+Shift+F5` o el icono de depurar).

<img src="assets/imatge7.jpg" alt="Imatge 7">

<img src="assets/imatge8.jpg" alt="Imatge 8">

Cuando el programa se detiene en un breakpoint, puedes examinar el valor de las variables y el flujo de ejecución.

**Ejemplo práctico:**

```java
public class DepuracionEjemplo {
    public static void main(String[] args) {
        int suma = 0;
        for (int i = 1; i <= 5; i++) {  // ← Breakpoint aquí
            suma += i;
            IO.println("i = " + i + ", suma = " + suma);  // ← Y aquí
        }
        IO.println("Suma final: " + suma);
    }
}
```

> [!NOTE]
> Cuando el programa se ejecuta en **modo de depuración**, se pausa automáticamente en cada breakpoint configurado, permitiendo examinar el estado del programa.

**Tipos de breakpoints:**


| Tipo | Descripción | Cuándo usar |
| :-- | :-- | :-- |
| **Línea** | Se para al llegar a una línea específica | Para examinar el flujo básico |
| **Condicional** | Se para solo si se cumple una condición | Para casos específicos |
| **Método** | Se para al entrar o salir de un método | Para analizar llamadas a funciones |
| **Excepción** | Se para cuando se lanza una excepción | Para capturar errores específicos |

### 6.4 Inspección de variables

<img src="assets/imatge9.jpg" alt="Imatge 9">

<img src="assets/imatge10.jpg" alt="Imatge 10">


Durante la ejecución en modo depuración, NetBeans ofrece potentes herramientas para la **inspección de variables**:

#### 📋 Ventana "Variables"

**Características:**

- Muestra los valores actuales de todas las variables en el ámbito actual
- Permite expandir objetos complejos para ver sus propiedades
- Se actualiza automáticamente los valores a medida que se ejecuta el código
- Organiza las variables por ámbito (local, parámetros, campos de clase)

**Información mostrada:**

- **Nombre** de la variable
- **Tipo** de dato
- **Valor** actual
- **Ámbito** donde está definida


#### 👁️ Ventana "Watches"

**Funcionalidades:**

- Permite añadir expresiones específicas para monitorizar durante la ejecución
- Útil para seguir el valor de cálculos complejos o propiedades de objetos
- Se puede configurar para evaluar expresiones personalizadas
- Mantiene las expresiones entre sesiones de depuración

> [!TIP]
> Utiliza la ventana "Watches" para monitorizar expresiones complejas como `array.length` o `object.getProperty()`.

**Ejemplo de inspección de variables:**

```java
public class EjemploInspeccion {
    public static void main(String[] args) {
        int[] numeros = {1, 2, 3, 4, 5};
        int suma = 0;
        
        for (int i = 0; i < numeros.length; i++) {  // ← Breakpoint
            suma += numeros[i];
            // En este punto podemos inspeccionar:
            // - i (valor del contador)
            // - numeros[i] (elemento actual)
            // - suma (suma acumulativa)
            // - numeros.length (longitud del array)
        }
        
        double promedio = (double) suma / numeros.length;  // ← Breakpoint
        IO.println("Promedio: " + promedio);
    }
}
```

### 6.5 Ejecución paso a paso

La **ejecución paso a paso** (*Step-by-Step Execution*) permite a los desarrolladores ejecutar el código una línea a la vez, facilitando la comprensión del flujo de ejecución y la identificación exacta de dónde se producen los errores.

[!NOTE]
Estos ejemplos evitan métodos propios (los veremos en UT4) y arrays (UT3). Por eso, Step Into/Step Out/Call Stack se ilustran aquí de forma limitada, apoyándonos en métodos ya existentes de la librería estándar (String.length(), Math.max()). Estas herramientas ganarán todo su sentido cuando escribamos nuestros propios métodos.

#### Tipos de ejecución paso a paso:

**🔍 Step Into (F7) <img src="assets/imatge12.jpg" alt="Imatge 12">**

**Comportamiento:**

- Executa la línea de código actual
- Si la línea contiene una llamada a una función o método, **entra dentro** de esa función
- Permite ver la ejecución detallada dentro del método llamado

**Cuándo usar:**

- Para depurar funciones propias donde sospechas que hay un error
- Cuando necesitas entender cómo funciona un método específico
- Para verificar el paso de parámetros entre métodos

```java
public class StepIntoEjemplo {
    public static void main(String[] args) {
        String texto = "Hola";
        int longitud = texto.length();  // Técnicamente "Step Into" entraría en el código fuente de la JDK
        IO.println("Longitud: " + longitud);
    }
}
```

[!TIP]
En la práctica, casi nunca se usa Step Into sobre métodos de la librería estándar (su código no suele ser útil de depurar); se reserva para nuestros propios métodos a partir de UT4.

**🔄 Step Over (F8) <img src="assets/imatge11.jpg" alt="Imatge 11">**

**Comportamiento:**

- Ejecuta la línea de código actual
- Si la línea contiene una llamada a una función, la ejecuta completamente **sin entrar**
- Útil para avanzar rápidamente cuando no necesitamos ver la ejecución interna

**Cuándo usar:**

- Para funciones de sistema o librerías externas
- Cuando sabemos que un método funciona correctamente
- Para avanzar rápidamente por código conocido

```java
public class StepOverEjemplo {
    public static void main(String[] args) {
        String texto = "Hola Mundo";
        int longitud = texto.length();  // ← Step Over ejecutará length() sin entrar
        IO.println(longitud);   // ← Continuará aquí directamente
    }
}
```

**⚡ Step Over Expression (Shift+F8) <img src="assets/imatge13.jpg" alt="Imatge 13">**

**Comportamiento:**

- Ejecuta la siguiente expresión dentro de la línea actual
- Útil cuando quieres ver la ejecución paso a paso de una línea con múltiples expresiones
- Permite analizar operaciones complejas parte por parte

**Ejemplo:**

```java
public class StepOverExpressionEjemplo {
    public static void main(String[] args) {
        int a = 5, b = 3, c = 2;
        // Esta línea tiene múltiples expresiones
        int resultado = (a + b) * c - Math.max(a, b);
        //              ^^^^^   ^^^   ^^^^^^^^^^^^^
        //               1      2         3
        // Step Over Expression ejecutará cada parte por separado
    }
}
```

**📤 Step Out (Shift+F7) <img src="assets/imatge14.jpg" alt="Imatge 14">**

**Comportamiento:**

- Continúa la ejecución hasta que se sale del método actual
- Útil cuando ya estás dentro de un método y quieres volver al método que lo llamó
- Ejecuta el resto del método actual y se para en la línea siguiente de quien lo llamó

**Cuándo usar:**

- Cuando has verificado que un método funciona correctamente
- Para salir rápidamente de métodos largos
- Cuando accidentalmente entraste en un método con Step Into

**Continue (F5) <img src="assets/imatge15.jpg" alt="Imatge 15">**

**Comportamiento:**

- Continúa la ejecución del programa hasta el siguiente breakpoint o hasta que termine
- Útil cuando has identificado y corregido errores
- Permite verificar si el programa funciona correctamente más allá del punto de inspección

**Run to Cursor (F4) <img src="assets/imatge16.jpg" alt="Imatge 16">**

**Comportamiento:**

- Permite ejecutar el programa hasta la línea donde se encuentra el cursor
- Muy útil para saltar rápidamente a una parte específica del código
- Evita tener que configurar breakpoints manuales temporales

**Ejemplo práctico de uso:**

```java
public class EjemploPasoAPaso {
    public static void main(String[] args) {
        int contador = 0;   // ← Breakpoint inicial
        int suma = 0;

        while (contador < 5) {   // ← Step Over para avanzar iteración a iteración
            suma += contador;
            contador++;
        }

        double promedio = (double) suma / contador;  // ← Run to Cursor para llegar aquí rápido
        IO.println("Promedio: " + promedio);
    }
}
```

[!NOTE]
Cuando en UT3 (arrays) y UT4 (métodos) dispongamos de más herramientas del lenguaje, retomaremos este mismo ejemplo dividido en varios métodos para explotar todo el potencial de Step Into, Step Out y Call Stack.


### 6.6 Otras herramientas útiles

<img src="assets/imatge20.jpg" alt="Imatge 20">


NetBeans incluye herramientas adicionales que complementan el proceso de depuración:

#### 📚 Call Stack (Pila de llamadas)

**Funcionalidad:**

- Muestra la secuencia completa de llamadas a métodos
- Permite navegar por la pila de llamadas para entender el flujo de ejecución
- Útil para identificar cómo se ha llegado al punto actual del programa

**Información que proporciona:**

- **Orden de llamadas**: Qué método llamó a qué
- **Parámetros**: Valores pasados entre métodos
- **Ubicación**: Línea exacta de cada llamada
- **Contexto**: Estado de variables en cada nivel

**Ejemplo de Call Stack:**

```
Thread main
├── EjemploCallStack.main(String[]) línea: 5
├── EjemploCallStack.metodoA(int) línea: 10
├── EjemploCallStack.metodoB(int, String) línea: 15
└── EjemploCallStack.metodoC() línea: 20  ← Punto actual
```


#### 🧵 Threads (Hilos de ejecución)

**Características:**

- Visualiza los diferentes hilos de ejecución activos
- Permite cambiar entre threads para depurar aplicaciones multihilo
- Esencial para aplicaciones concurrentes

**Cuándo es útil:**

- Aplicaciones con múltiples hilos
- Problemas de concurrencia
- Deadlocks y race conditions
- Aplicaciones con interfaces gráficas


#### 💾 Memory View (Vista de memoria)

**Funcionalidades:**

- Muestra información sobre el uso de memoria
- Ayuda a identificar posibles fugas de memoria (*memory leaks*)
- Permite optimizar el rendimiento de la aplicación

**Métricas importantes:**

- **Heap Usage**: Uso del montón de memoria
- **Objects Count**: Número de objetos en memoria
- **GC Activity**: Actividad del recolector de basura


<img src="assets/imatge21.jpg" alt="Imatge 21">

## 7. Documentación y registro de la depuración

La **documentación y el registro** son partes cruciales del proceso de depuración. Aseguran que el trabajo realizado durante la identificación y resolución de errores quede bien registrado y pueda ser utilizado por futuros desarrolladores o para la mejora continua del proyecto.

### 📋 Elementos clave de la documentación:

#### 🚨 Anotación de los errores encontrados

**Información esencial a registrar:**


| Campo | Descripción | Ejemplo |
| :-- | :-- | :-- |
| **Descripción detallada** | Qué hace el error y cuándo se produce | "El programa se cuelga al introducir un número negativo" |
| **Condiciones de reproducción** | Pasos específicos para recrear el error | "1. Ejecutar programa 2. Introducir -5 3. Presionar Enter" |
| **Impacto** | Cómo afecta el error al funcionamiento del programa | "Impide que el usuario pueda continuar con el cálculo" |
| **Prioridad** | Clasificación de la gravedad del error | "Alta/Media/Baja" |

**Plantilla de registro de errores:**

<blockquote>

## Error #001
**Fecha**: 2024-01-15
**Reportado por**: Juan Pérez
**Módulo afectado**: CalculadoraDescuentos.java
**Línea**: 45

### Descripción
División por cero cuando el precio introducido es 0.

### Pasos para reproducir
1. Ejecutar CalculadoraDescuentos
2. Introducir precio: 0
3. Seleccionar calcular descuento
4. Se produce ArithmeticException

### Impacto
- Severidad: Alta
- El programa termina inesperadamente
- Pérdida de datos introducidos

### Estado
☐ Pendiente ☑ En proceso ☐ Resuelto ☐ Verificado

</blockquote>


#### 🧪 Registro de las pruebas realizadas

**Elementos a documentar:**

- **Casos de prueba ejecutados**: Qué pruebas se han realizado
- **Resultados obtenidos**: Resultados esperados vs. resultados reales
- **Datos de prueba utilizados**: Valores de entrada utilizados en las pruebas
- **Entorno de prueba**: Configuración del sistema donde se han ejecutado las pruebas

**Ejemplo de registro de pruebas:**

```java
/*
 * REGISTRO DE PRUEBAS - CalculadoraDescuentos
 * ==========================================
 * 
 * Caso de prueba 1: Precio válido con descuento
 * - Entrada: precio = 150.0, descuento = 10%
 * - Esperado: 135.0
 * - Obtenido: 135.0
 * - Estado: ✅ PASADO
 * 
 * Caso de prueba 2: Precio límite
 * - Entrada: precio = 100.0, descuento = 10%
 * - Esperado: 90.0
 * - Obtenido: 90.0
 * - Estado: ✅ PASADO
 * 
 * Caso de prueba 3: Precio por debajo del límite
 * - Entrada: precio = 50.0
 * - Esperado: No aplicar descuento, precio = 50.0
 * - Obtenido: 50.0
 * - Estado: ✅ PASADO
 * 
 * Caso de prueba 4: Precio cero (ERROR DETECTADO)
 * - Entrada: precio = 0.0
 * - Esperado: Mensaje de error o precio = 0.0
 * - Obtenido: ArithmeticException
 * - Estado: ❌ FALLIDO
 */
```


#### 💡 Soluciones implementadas

**Documentación de las correcciones:**

- **Descripción de la solución**: Cómo se ha resuelto el error
- **Código modificado**: Qué líneas o métodos se han cambiado
- **Razonamiento**: Por qué se ha elegido esta solución específica
- **Pruebas de verificación**: Cómo se ha confirmado que la solución funciona

**Ejemplo de documentación de solución:**

```java
/*
 * SOLUCIÓN IMPLEMENTADA - Error #001
 * ==================================
 * 
 * Problema: División por cero en calcularDescuento()
 * Línea afectada: 45
 * 
 * Solución aplicada:
 * - Añadida validación de entrada antes del cálculo
 * - Implementado manejo de casos especiales
 * 
 * Código anterior:
 *   double porcentajeDescuento = descuento / precio * 100;
 * 
 * Código corregido:
 *   if (precio <= 0) {
 *       IO.println("Error: El precio debe ser mayor que cero");
 *   }
 *   else {
 *       double porcentajeDescuento = descuento / precio * 100;
 *   }

 * 
 * Justificación:
 * - Previene la división por cero
 * - Proporciona retroalimentación clara al usuario
 * - Mantiene la funcionalidad para casos válidos
 * 
 * Verificación:
 * - Probado con precio = 0: Muestra mensaje de error ✅
 * - Probado con precio = -5: Muestra mensaje de error ✅
 * - Probado con precio = 100: Funciona correctamente ✅
 */
```

> [!IMPORTANT]
> Mantener un registro detallado ayuda a evitar errores similares en el futuro y facilita el mantenimiento del código.

## 8. Buenas prácticas en depuración

Seguir buenas prácticas en la depuración no solo mejora la eficiencia del proceso, sino que también ayuda a prevenir futuros errores:

### 🧠 Comprender el código

**📖 Lectura completa:**

- Asegúrate de entender completamente la lógica del código antes de intentar depurarlo
- Lee comentarios y documentación asociada
- Comprende el propósito y funcionalidad del módulo que se está depurando

**🎯 Análisis del contexto:**

- Entiende qué está tratando de hacer el programa
- Identifica las entradas esperadas y las salidas deseadas
- Comprende el flujo de datos general

**Ejemplo de análisis:**

```java
/*
 * ANÁLISIS DEL CÓDIGO
 * ===================
 *
 * Propósito: Calcular el promedio de notas de un estudiante
 * Entrada: Notas decimales introducidas por teclado, una por una (0.0 - 10.0)
 * Salida: Promedio calculado
 *
 * Flujo esperado:
 * 1. Pedir cada nota por teclado
 * 2. Validar que la nota esté en rango válido
 * 3. Acumular la suma
 * 4. Dividir por el número de notas
 * 5. Mostrar el resultado
 */
```


### 🚫 Evitar suposiciones

**🔍 Evidencia objetiva:**

- No hagas suposiciones sobre dónde se encuentra el error sin evidencia
- Utiliza siempre herramientas de depuración para confirmar hipótesis
- Verifica cada suposición con datos reales

**📊 Verificación sistemática:**

- Comprueba cada paso del flujo de ejecución
- Valida los valores de las variables en puntos clave
- No asumas que una parte del código funciona correctamente solo porque "debería"

**Ejemplo de verificación:**

```java
public class VerificacionEjemplo {
    public static void main(String[] args) {
        int cantidadNotas = 5;
        int notasValidas = 0;
        double sumaNotas = 0;
        int contador = 0;

        // ❌ Suposición: "todas las notas estarán siempre en rango válido"
        // ✅ Verificación: comprobar cada nota antes de sumarla
        while (contador < cantidadNotas) {
            String textoNota = IO.readln("Introduce la nota " + (contador + 1) + ": ");

            if (Teclado.esDecimal(textoNota)) {
                double nota = Double.parseDouble(textoNota);
                if (nota < 0 || nota > 10) {
                    IO.println("Error: nota fuera de rango: " + nota);
                } else {
                    sumaNotas += nota;
                    notasValidas++;
                }
            } else {
                IO.println("Error: debes introducir un número decimal válido.");
            }
            contador++;
        }

        if (notasValidas > 0) {
            IO.println("Promedio: " + (sumaNotas / notasValidas));
        } else {
            IO.println("No se ha podido calcular el promedio: no hay notas válidas.");
        }
    }
}
```


### 🔧 Simplificar el problema

**📉 Reducción del código:**

- Reduce el código a su forma más simple para identificar el error
- Comenta partes del código para aislar el problema
- Crea versiones mínimas que reproduzcan el error

**🔬 Aislamiento:**

- Aísla las partes del código para reducir la complejidad
- Prueba cada componente por separado
- Utiliza datos de entrada simples y conocidos

**Ejemplo de simplificación:**

```java
// ❌ Código denso: todo mezclado en un único bucle, difícil de depurar
public class ComplejoEjemplo {
    public static void main(String[] args) {
        double totalIngresos = 0;
        int totalVentas = 0;
        int contador = 0;

        while (contador < 5) {
            String textoVenta = IO.readln("Introduce el importe de la venta " + (contador + 1) + ": ");
            if (Teclado.esDecimal(textoVenta)) {
                double venta = Double.parseDouble(textoVenta);
                if (venta > 0) {
                    totalIngresos += venta;
                    totalVentas++;
                    if (venta > 100) {
                        totalIngresos = totalIngresos - (venta * 0.05); // descuento oculto mezclado aquí
                    }
                } else {
                    IO.println("Venta no válida, se ignora.");
                }
            } else {
                IO.println("Entrada no numérica, se ignora.");
            }
            contador++;
        }

        double mediaVentas = totalIngresos / totalVentas; // ⚠️ posible división por cero
        IO.println("Ingresos totales: " + totalIngresos);
        IO.println("Media por venta: " + mediaVentas);
    }
}
```

```java
// ✅ Versión simplificada para depuración: aislamos solo el cálculo problemático
public class SimplificadoEjemplo {
    public static void main(String[] args) {
        // Usamos valores fijos y conocidos para eliminar variables
        double totalIngresos = 250.0;
        int totalVentas = 0; // ← Provocamos el caso límite a propósito

        double mediaVentas = totalIngresos / totalVentas; // ← Aquí está el error: división por cero
        IO.println("Media por venta: " + mediaVentas);
    }
}
```


### 🔄 Hacer pruebas incrementales

**🎯 Cambios pequeños:**

- Realiza cambios pequeños y pruébalos inmediatamente
- No hagas múltiples cambios simultáneamente
- Mantén un registro de qué cambios funcionan y cuáles no

**📊 Impacte controlado:**

- Identifica el impacto de cada cambio individual
- Revierte cambios que no mejoren la situación
- Construye la solución paso a paso

**Ejemplo de enfoque incremental:**

```java
// Paso 1: Identificar el problema
int contador = 0;
double suma = 0;
while (contador < 5) {
    String texto = IO.readln("Introduce una nota: ");
    double nota = Double.parseDouble(texto); // ¿Problema si el texto no es válido?
    suma += nota;
    contador++;
}
double promedio = suma / contador;

// Paso 2: Añadir depuración básica
int contador = 0;
double suma = 0;
while (contador < 5) {
    String texto = IO.readln("Introduce una nota: ");
    IO.println("DEBUG: texto leído = " + texto);
    double nota = Double.parseDouble(texto);
    suma += nota;
    IO.println("DEBUG: suma actual = " + suma);
    contador++;
}
double promedio = suma / contador;
IO.println("DEBUG: promedio final = " + promedio);

// Paso 3: Añadir validación (con if, sin excepciones)
int contador = 0;
double suma = 0;
int notasValidas = 0;
while (contador < 5) {
    String texto = IO.readln("Introduce una nota: ");
    if (Teclado.esDecimal(texto)) {
        double nota = Double.parseDouble(texto);
        suma += nota;
        notasValidas++;
    } else {
        IO.println("Entrada no válida, se ignora esta nota.");
    }
    contador++;
}
if (notasValidas > 0) {
    IO.println("Promedio: " + (suma / notasValidas));
} else {
    IO.println("No se ha podido calcular el promedio.");
}

// Paso 4: versión final, ya limpia de mensajes de depuración (igual que el paso 3 sin los DEBUG)
```


### 👥 Revisión de código

**👀 Perspectiva externa:**

- Comparte el código con otros programadores para una revisión
- A menudo, un nuevo par de ojos puede identificar problemas que el autor original pasó por alto
- Explica tu código a otros: el proceso de explicación puede revelar errores

**📚 Aprendizaje mutuo:**

- La revisión beneficia tanto al revisor como al autor
- Aprende de las soluciones propuestas por otros
- Comparte tu conocimiento y aprende nuevas técnicas

**Proceso de revisión de código:**

<blockquote>

## REVISIÓN DE CÓDIGO - CalculadoraDescuentos.java

### Revisor: María García
### Fecha: 2024-01-15
### Autor original: Juan Pérez

### Problemas encontrados:

1. **Línea 25**: Falta validación de entrada
   - Problema: No se verifica si el precio es negativo
   - Sugerencia: Añadir `if (precio < 0) return error;`

2. **Línea 42**: Variable sin inicializar
   - Problema: `descuentoAplicado` puede usarse sin valor
   - Sugerencia: Inicializar a 0.0

3. **Línea 58**: Lógica de descuento confusa
   - Problema: Difícil de entender el cálculo
   - Sugerencia: Dividir en pasos más claros

### Aspectos positivos:
- Buenos nombres de variables
- Comentarios claros
- Estructura lógica

</blockquote>


### 📝 Documentación del código

**🏷️ Nombres significativos:**

```java
// ❌ Nombres poco descriptivos
double s = 0;
int c = 0;
while (c < 5) {
    s += Double.parseDouble(IO.readln("Nota: "));
    c++;
}
double prom = s / c;

// ✅ Nombres descriptivos
double sumaTotal = 0;
int contadorNotas = 0;
while (contadorNotas < 5) {
    sumaTotal += Double.parseDouble(IO.readln("Nota: "));
    contadorNotas++;
}
double promedioNotas = sumaTotal / contadorNotas;
```

**📋 Estructuras claras:**

```java
public class CalculoNotasOrganizado {
    public static void main(String[] args) {
        // Paso 1: leer las notas
        int cantidadNotas = 5;
        double sumaTotal = 0;
        int contador = 0;

        while (contador < cantidadNotas) {
            String textoNota = IO.readln("Introduce la nota " + (contador + 1) + ": ");

            // Paso 2: validar cada nota antes de sumarla
            if (Teclado.esDecimal(textoNota)) {
                double nota = Double.parseDouble(textoNota);
                if (nota >= 0.0 && nota <= 10.0) {
                    sumaTotal += nota; // Paso 3: acumular
                } else {
                    IO.println("Nota fuera de rango: " + nota);
                }
            } else {
                IO.println("Entrada no válida.");
            }
            contador++;
        }

        // Paso 4: calcular y mostrar el resultado
        IO.println("Promedio: " + (sumaTotal / cantidadNotas));
    }
}
```

[!NOTE]
En UT4 aprenderemos a dividir este mismo código en métodos independientes (leerNotas, validar, calcularPromedio, mostrarResultado), lo que hará el código aún más claro y reutilizable.

**🚫 Evitar duplicación:**

```java
// ❌ Código duplicado: la misma lógica de cálculo repetida dos veces
double sumaGrupoA = 0;
int contadorA = 0;
while (contadorA < 3) {
    sumaGrupoA += Double.parseDouble(IO.readln("Nota Grupo A: "));
    contadorA++;
}
IO.println("Promedio Grupo A: " + (sumaGrupoA / 3));

double sumaGrupoB = 0;
int contadorB = 0;
while (contadorB < 3) {
    sumaGrupoB += Double.parseDouble(IO.readln("Nota Grupo B: "));
    contadorB++;
}
IO.println("Promedio Grupo B: " + (sumaGrupoB / 3));
```
[!IMPORTANT]
En UT4 aprenderemos a extraer esta lógica repetida a un único método reutilizable (por ejemplo, calcularPromedio(...)), eliminando la duplicación de forma definitiva. Por ahora, saber identificar la duplicación ya es un primer paso útil.

[!WARNING]
La depuración es un proceso iterativo. No esperes resolver todos los errores de una vez.

[!CAUTION]
Siempre haz copias de seguridad del código antes de implementar cambios significativos durante la depuración.

## 9. Ejemplo práctico de depuración

### Ejemplo 1: Depuración de un bucle infinito

**Código problemático:**

```java
public class BucleInfinito {
    public static void main(String[] args) {
        int suma = 0;
        for (int i = 1; i != 10; i += 2) {  // ¡Problema aquí!
            suma += i;
            IO.println("i = " + i + ", suma = " + suma);
        }
        IO.println("Suma final: " + suma);
    }
}
```

**Proceso de depuración:**

1. **Identificación**: El programa no termina nunca
2. **Breakpoint**: Colocar en la línea del `for`
3. **Inspección**: Observar valores de `i` en cada iteración
4. **Análisis**: `i` va de 1, 3, 5, 7, 9, 11... nunca es exactamente 10
5. **Solución**: Cambiar `i != 10` por `i < 10`

**Código corregido:**

```java
public class BucleCorregido {
    public static void main(String[] args) {
        int suma = 0;
        for (int i = 1; i < 10; i += 2) {  // ✅ Corrección aplicada
            suma += i;
            IO.println("i = " + i + ", suma = " + suma);
        }
        IO.println("Suma final: " + suma);
    }
}
```


### Ejemplo 2: Depuración de un error de lógica

**Código problemático:**

```java
public class ErrorLogica {
    public static void main(String[] args) {
        int cantidadNotas = 5;
        int aprobados = 0;
        int contador = 0;

        while (contador <= cantidadNotas) {  // ¡Error de límite! Pide 6 notas en vez de 5
            String textoNota = IO.readln("Introduce la nota " + (contador + 1) + ": ");
            double nota = Double.parseDouble(textoNota);
            if (nota >= 5) {
                aprobados++;
            }
            contador++;
        }

        IO.println("Estudiantes aprobados: " + aprobados);
    }
}
```

**Traza de depuración:**


| Iteración | contador | ¿Se pide nota?         | ¿Error?                     |
| --------- | -------- | ---------------------- | --------------------------- |
| 1–5       | 0–4      | Sí (esperado)          | No                          |
| 6         | 5        | Sí, no debería pedirse | ✅ Bug: pide una nota de más |

**Código corregido:**

```java
public class ErrorLogicaCorregido {
    public static void main(String[] args) {
        int cantidadNotas = 5;
        int aprobados = 0;
        int contador = 0;

        // ✅ Cambiar <= por < para pedir exactamente cantidadNotas notas
        while (contador < cantidadNotas) {
            String textoNota = IO.readln("Introduce la nota " + (contador + 1) + ": ");
            double nota = Double.parseDouble(textoNota);
            if (nota >= 5) {
                aprobados++;
            }
            contador++;
        }

        IO.println("Estudiantes aprobados: " + aprobados);
    }
}
```


### Ejemplo 3: Depuración con breakpoints condicionales

**Código a depurar:**

```java
public class BreakpointCondicional {
    public static void main(String[] args) {
        int numero = 1;

        while (numero <= 100) {
            if (numero % 7 == 0 && numero > 30) {  // ← Breakpoint condicional aquí
                IO.println("Encontrado: primer múltiplo de 7 mayor que 30 = " + numero);
                break;
            }
            numero++;
        }
    }
}
```

**Configuración del breakpoint condicional:**

- **Condición**: `numero == objetivo`
- **Efecto**: Solo se para cuando encuentra el número buscado
- **Ventaja**: No para en cada iteración, solo cuando es relevante

> [!TIP]
> Los breakpoints condicionales son especialmente útiles cuando buscas condiciones específicas en bucles largos.

**Resultado de la depuración:**

- Permite inspeccionar el estado en el momento exacto del hallazgo
- Facilita la verificación de que la lógica de búsqueda es correcta


## 10. Prácticas propuestas

1. **Reproduce un error intencionado** en un programa sencillo y depúralo usando breakpoints y ejecución paso a paso.
2. **Corrige un bucle infinito** modificando la condición del bucle.
3. **Documenta el proceso de depuración**: describe el error, cómo lo encontraste, cómo lo solucionaste y cómo comprobaste que estaba resuelto.
4. **Comparte tu código corregido** y tus notas de depuración con un compañero para revisión cruzada.
5. **Explora otras herramientas del IDE** como la vista de memoria, el call stack o la gestión de hilos.

> [!NOTE]
> La depuración y las pruebas son habilidades esenciales para cualquier programador profesional. Dominar estas técnicas te permitirá desarrollar software más robusto, eficiente y fácil de mantener.

---
<p align="center">📚 <em>Fin del apartado UT2.4 - Pruebas y depuración</em></p>

---
<small>© 2026 José Ramón Mas Davó. Todo el material docente original se distribuye bajo licencia [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/). Para más detalles, consulta el archivo [`LICENSE`](../LICENSE) del repositorio.</small>

