# Anexo I. Inferencia de tipos, records y clases selladas

## 📋 Índice de contenidos

1. [Introducción](#1-introducci%C3%B3n)
2. [Inferencia de tipos con var (JDK 10+)](#2-inferencia-de-tipos-con-var-jdk-10)
3. [Records (JDK 16+)](#3-records-jdk-16)
4. [Clases selladas (JDK 17+)](#4-clases-selladas-jdk-17)
5. [Ejemplo práctico combinado](#5-ejemplo-pr%C3%A1ctico-combinado)

## 1. Introducción

Java ha evolucionado considerablemente desde sus versiones iniciales, añadiendo características que **simplifican el código** y **mejoran la productividad del desarrollador**. En este anexo estudiaremos tres características modernas que encontrarás frecuentemente en código Java actual:

- **var (JDK 10+)**: Inferencia automática de tipos
- **Records (JDK 16+)**: Clases de datos inmutables sin boilerplate
- **Clases selladas (JDK 17+)**: Control sobre la herencia

> [!IMPORTANT]
> Estas características son **ampliamente utilizadas** en el desarrollo Java moderno. Su comprensión es fundamental para entender código actual y para escribir código más limpio y expresivo.

## 2. Inferencia de tipos con var (JDK 10+)

La **inferencia de tipos** es la capacidad del compilador de **determinar automáticamente el tipo de una variable** basándose en el valor que se le asigna

### ¿Qué es var?

**var** permite que el compilador infiera automáticamente el tipo de una variable local:

```java
// Antes de Java 10
String mensaje = "Hola mundo";
ArrayList<String> lista = new ArrayList<>();
HashMap<Integer, String> mapa = new HashMap<>();

// Con var
var mensaje = "Hola mundo";              // String inferido
var lista = new ArrayList<String>();     // ArrayList<String> inferido  
var mapa = new HashMap<Integer, String>(); // HashMap<Integer, String> inferido
```

> [!NOTE]
> **var** no es una palabra clave (keyword) sino un **nombre de tipo reservado**. Esto significa que puedes seguir usando "var" como nombre de variable en otros contextos

### Cuándo usar var

✅ **Usar cuando:**

```java
// Tipo obvio por el contexto
var nombres = new ArrayList<String>();
var archivo = new File("documento.txt");

// Tipos complejos
var mapa = new HashMap<String, List<Integer>>();

// En bucles
for (var elemento : coleccion) {
    // procesar elemento
}
```

❌ **Evitar cuando:**

```java
public class LimitacionesVar {
    // ❌ No se puede usar en campos de clase
    // private var campo = "no permitido";
    
    // ❌ No se puede usar en parámetros de método
    // public void metodo(var parametro) { }
    
    // ❌ No se puede usar como tipo de retorno
    // public var metodo() { return "no"; }
    
    public static void main(String[] args) {
        // ❌ Debe tener inicializador
        // var sinInicializar;
        
        // ❌ No se puede inicializar con null
        // var nulo = null;
        
        // ✅ Uso correcto
        var correcto = "Esto funciona";
    }
}
```

### Práctica: Experimentando con var

**Objetivo:** Experimentar con diferentes usos de var y observar la inferencia de tipos.

<details>
<summary>💻 Solución</summary>

```java
import java.time.LocalDate;
import java.util.*;

public class PracticaVar {
    public static void main(String[] args) {
        PracticaVar practica = new PracticaVar();
        practica.experimentarConVar();
    }
    
    public void experimentarConVar() {
        System.out.println("=== EXPERIMENTACIÓN CON VAR ===");
        
        // 1. Tipos primitivos
        var numeroEntero = 100;
        var numeroDecimal = 99.99;
        var esVerdad = true;
        var letra = 'X';
        
        mostrarTipo("numeroEntero", numeroEntero);
        mostrarTipo("numeroDecimal", numeroDecimal);
        mostrarTipo("esVerdad", esVerdad);
        mostrarTipo("letra", letra);
        
        // 2. Strings y fechas
        var saludo = "¡Hola Java moderno!";
        var fechaHoy = LocalDate.now();
        
        mostrarTipo("saludo", saludo);
        mostrarTipo("fechaHoy", fechaHoy);
        
        // 3. Colecciones
        var listaNumeros = new ArrayList<Integer>();
        listaNumeros.add(1);
        listaNumeros.add(2);
        listaNumeros.add(3);
        
        var conjuntoTextos = new HashSet<String>();
        conjuntoTextos.add("Java");
        conjuntoTextos.add("Python");
        conjuntoTextos.add("JavaScript");
        
        mostrarTipo("listaNumeros", listaNumeros);
        mostrarTipo("conjuntoTextos", conjuntoTextos);
        
        // 4. Uso en bucles
        System.out.println("\n=== USO EN BUCLES ===");
        for (var numero : listaNumeros) {
            System.out.println("Número: " + numero);
        }
        
        for (var texto : conjuntoTextos) {
            System.out.println("Lenguaje: " + texto);
        }
        
        // 5. Comparación de legibilidad
        System.out.println("\n=== COMPARACIÓN DE LEGIBILIDAD ===");
        
        // Sin var (verboso)
        HashMap<String, ArrayList<Integer>> mapaComplejo1 = 
            new HashMap<String, ArrayList<Integer>>();
        
        // Con var (más limpio)
        var mapaComplejo2 = new HashMap<String, ArrayList<Integer>>();
        
        System.out.println("Ambos mapas son del mismo tipo: " + 
            mapaComplejo1.getClass().equals(mapaComplejo2.getClass()));
    }
    
    private void mostrarTipo(String nombreVariable, Object valor) {
        System.out.printf("%-15s -> Tipo: %-15s | Valor: %s%n", 
                         nombreVariable, 
                         valor.getClass().getSimpleName(), 
                         valor);
    }
}
```

</details>

## 3. Records (JDK 16+)

### ¿Qué son los Records?

Los **Records** son una forma concisa de crear clases que actúan como **portadores de datos inmutables**. Eliminan la necesidad de escribir código repetitivo (boilerplate) para clases que simplemente almacenan datos.

```java
// Clase tradicional (¡muchas líneas!)
public class Persona {
    private final String nombre;
    private final int edad;
    
    public Persona(String nombre, int edad) {
        this.nombre = nombre;
        this.edad = edad;
    }
    
    public String getNombre() { return nombre; }
    public int getEdad() { return edad; }
    
    // + equals(), hashCode(), toString()...
}

// ¡Con Record: 1 línea!
public record Persona(String nombre, int edad) {}
```

### Características automáticas

Un record genera automáticamente:

- **Constructor** con todos los componentes
- **Métodos de acceso** (mismo nombre que el componente)
- **equals()**, **hashCode()** y **toString()**

```java
public record Producto(String nombre, double precio) {}

public class EjemploRecord {
    public static void main(String[] args) {
        var producto1 = new Producto("Laptop", 999.99);
        var producto2 = new Producto("Laptop", 999.99);
        
        // Métodos automáticos
        System.out.println("Nombre: " + producto1.nombre());
        System.out.println("Precio: " + producto1.precio());
        System.out.println("ToString: " + producto1);
        System.out.println("¿Iguales? " + producto1.equals(producto2)); // true
    }
}
```

### Records con validación y métodos

Los records permiten **constructores personalizados** para validar datos:

**Constructor compacto:**

```java
public record Temperatura(double celsius) {
    // Constructor compacto para validación
    public Temperatura {
        if (celsius < -273.15) {
            throw new IllegalArgumentException(
                "La temperatura no puede ser menor que el cero absoluto");
        }
    }
}
```

**Constructor alternativo:**

```java
public record Persona(String nombre, int edad) {
    // Constructor alternativo
    public Persona(String nombre) {
        this(nombre, 0); // Edad por defecto
    }
    
    // Constructor compacto con validación
    public Persona {
        if (nombre == null || nombre.trim().isEmpty()) {
            throw new IllegalArgumentException("El nombre no puede estar vacío");
        }
        if (edad < 0) {
            throw new IllegalArgumentException("La edad no puede ser negativa");
        }
        // Normalizar el nombre
        nombre = nombre.trim();
    }
}
```

Los records pueden incluir **métodos personalizados**:

```java
public record Rectangulo(double ancho, double alto) {
    
    // Método personalizado para calcular área
    public double area() {
        return ancho * alto;
    }
    
    // Método personalizado para calcular perímetro
    public double perimetro() {
        return 2 * (ancho + alto);
    }
    
    // Método estático de conveniencia
    public static Rectangulo fromCuadrado(double lado) {
        return new Rectangulo(lado, lado);
    }
    
    // Método de validación
    public boolean esValido() {
        return ancho > 0 && alto > 0;
    }
}
```

### Práctica: Creando Records

**Objetivo:** Crear diferentes records y comparar con clases tradicionales.

<details>
<summary>💻 Solución</summary>

```java
// Record básico para datos de contacto
record Contacto(String nombre, String telefono, String email) {}

// Record con validación
record CuentaBancaria(String numeroCuenta, String titular, double saldo) {
    public CuentaBancaria {
        if (numeroCuenta == null || numeroCuenta.length() != 10) {
            throw new IllegalArgumentException("Número de cuenta debe tener 10 dígitos");
        }
        if (titular == null || titular.trim().isEmpty()) {
            throw new IllegalArgumentException("El titular no puede estar vacío");
        }
        if (saldo < 0) {
            throw new IllegalArgumentException("El saldo no puede ser negativo");
        }
    }
    
    public CuentaBancaria depositar(double cantidad) {
        if (cantidad <= 0) {
            throw new IllegalArgumentException("La cantidad debe ser positiva");
        }
        return new CuentaBancaria(numeroCuenta, titular, saldo + cantidad);
    }
    
    public boolean puedeRetirar(double cantidad) {
        return cantidad > 0 && cantidad <= saldo;
    }
}

// Record con métodos estáticos
record Punto(double x, double y) {
    public static Punto origen() {
        return new Punto(0, 0);
    }
    
    public double distanciaAlOrigen() {
        return Math.sqrt(x * x + y * y);
    }
    
    public Punto trasladar(double deltaX, double deltaY) {
        return new Punto(x + deltaX, y + deltaY);
    }
}

public class PracticaRecords {
    public static void main(String[] args) {
        PracticaRecords practica = new PracticaRecords();
        practica.demostrarRecords();
    }
    
    public void demostrarRecords() {
        System.out.println("=== DEMOSTRACIÓN DE RECORDS ===");
        
        // 1. Record básico
        System.out.println("1. Record básico:");
        var contacto1 = new Contacto("Juan Pérez", "123456789", "juan@email.com");
        var contacto2 = new Contacto("Juan Pérez", "123456789", "juan@email.com");
        
        System.out.println("Contacto: " + contacto1);
        System.out.println("Nombre: " + contacto1.nombre());
        System.out.println("¿Son iguales? " + contacto1.equals(contacto2));
        
        // 2. Record con validación
        System.out.println("\n2. Record con validación:");
        try {
            var cuenta = new CuentaBancaria("1234567890", "María López", 1000.0);
            System.out.println("Cuenta creada: " + cuenta);
            
            var cuentaConDeposito = cuenta.depositar(250.0);
            System.out.println("Después del depósito: " + cuentaConDeposito);
            
            System.out.println("¿Puede retirar 500€? " + cuenta.puedeRetirar(500.0));
            System.out.println("¿Puede retirar 1500€? " + cuenta.puedeRetirar(1500.0));
            
        } catch (IllegalArgumentException e) {
            System.out.println("Error: " + e.getMessage());
        }
        
        // 3. Record con métodos personalizados
        System.out.println("\n3. Record con métodos personalizados:");
        var origen = Punto.origen();
        var punto = new Punto(3, 4);
        
        System.out.println("Origen: " + origen);
        System.out.println("Punto: " + punto);
        System.out.println("Distancia al origen: " + punto.distanciaAlOrigen());
        
        var puntoTrasladado = punto.trasladar(1, 1);
        System.out.println("Punto trasladado: " + puntoTrasladado);
        
        // 4. Inmutabilidad
        System.out.println("\n4. Demostración de inmutabilidad:");
        var puntoOriginal = new Punto(10, 20);
        var puntoModificado = puntoOriginal.trasladar(5, 5);
        
        System.out.println("Punto original: " + puntoOriginal);
        System.out.println("Punto modificado: " + puntoModificado);
        System.out.println("El original no cambió: " + puntoOriginal.equals(new Punto(10, 20)));
    }
}
```

</details>

## 4. Clases selladas (JDK 17+)

### ¿Qué son las clases selladas?

Las **clases selladas** (sealed classes) permiten **controlar qué clases pueden extender** una clase o implementar una interfaz. Proporcionan un control granular sobre la jerarquía de herencia.

**Problema tradicional:**

```java
// Cualquiera puede extender esta clase
public abstract class Forma {
    public abstract double calcularArea();
}

// Extensiones no controladas
class CirculoMalicioso extends Forma {
    public double calcularArea() { return -1; } // ¡Problemático!
}
```

**Solución con clases selladas:**

```java
// Solo las clases especificadas pueden extender Forma
public sealed class Forma 
    permits Circulo, Rectangulo, Triangulo {
    
    public abstract double calcularArea();
}

// ❌ Esta clase no compila - no está en permits
// class FormaMaliciosa extends Forma { }
```

> [!IMPORTANT]
> Las clases selladas crean una **jerarquía cerrada** donde tienes control total sobre qué clases pueden formar parte de la herencia.

### Tipos de subclases

Las clases que extienden una clase sellada deben ser:

```java
// 1. FINAL - No puede ser extendida más
public final class Circulo extends Forma {
    private double radio;
    
    public Circulo(double radio) {
        this.radio = radio;
    }
    
    @Override
    public double calcularArea() {
        return Math.PI * radio * radio;
    }
}

// 2. SEALED - Controla sus propias extensiones  
public sealed class Rectangulo extends Forma 
    permits Cuadrado {
    
    protected double ancho, alto;
    
    public Rectangulo(double ancho, double alto) {
        this.ancho = ancho;
        this.alto = alto;
    }
    
    @Override
    public double calcularArea() {
        return ancho * alto;
    }
}

// 3. NON-SEALED - Abre la herencia
public non-sealed class Triangulo extends Forma {
    private double base, altura;
    
    public Triangulo(double base, double altura) {
        this.base = base;
        this.altura = altura;
    }
    
    @Override
    public double calcularArea() {
        return (base * altura) / 2;
    }
}

// Especialización de Rectangulo
public final class Cuadrado extends Rectangulo {
    public Cuadrado(double lado) {
        super(lado, lado);
    }
}

// Esto es posible porque Triangulo es non-sealed
class TrianguloEspecial extends Triangulo {
    public TrianguloEspecial(double base, double altura) {
        super(base, altura);
    }
}
```

### Práctica: Sistema de formas

**Objetivo:** Crear una jerarquía de formas geométricas usando clases selladas.

<details>
<summary>💻 Solución</summary>

```java
// Clase sellada base para formas geométricas
public sealed class Forma 
    permits Circulo, Rectangulo, Triangulo {
    
    protected String color;
    
    public Forma(String color) {
        this.color = color;
    }
    
    public abstract double calcularArea();
    public abstract double calcularPerimetro();
    
    public String getColor() {
        return color;
    }
    
    public void mostrarInfo() {
        System.out.printf("Forma: %s, Color: %s, Área: %.2f, Perímetro: %.2f%n",
                         getClass().getSimpleName(), color, 
                         calcularArea(), calcularPerimetro());
    }
}

// Círculo - final (no puede extenderse más)
public final class Circulo extends Forma {
    private double radio;
    
    public Circulo(String color, double radio) {
        super(color);
        if (radio <= 0) {
            throw new IllegalArgumentException("El radio debe ser positivo");
        }
        this.radio = radio;
    }
    
    @Override
    public double calcularArea() {
        return Math.PI * radio * radio;
    }
    
    @Override
    public double calcularPerimetro() {
        return 2 * Math.PI * radio;
    }
    
    public double getRadio() {
        return radio;
    }
}

// Rectángulo - sealed (permite especializaciones)
public sealed class Rectangulo extends Forma 
    permits Cuadrado {
    
    protected double ancho;
    protected double alto;
    
    public Rectangulo(String color, double ancho, double alto) {
        super(color);
        if (ancho <= 0 || alto <= 0) {
            throw new IllegalArgumentException("Las dimensiones deben ser positivas");
        }
        this.ancho = ancho;
        this.alto = alto;
    }
    
    @Override
    public double calcularArea() {
        return ancho * alto;
    }
    
    @Override
    public double calcularPerimetro() {
        return 2 * (ancho + alto);
    }
    
    public double getAncho() { return ancho; }
    public double getAlto() { return alto; }
}

// Cuadrado - especialización de rectángulo
public final class Cuadrado extends Rectangulo {
    public Cuadrado(String color, double lado) {
        super(color, lado, lado);
    }
    
    public double getLado() {
        return ancho; // ancho == alto en un cuadrado
    }
    
    @Override
    public void mostrarInfo() {
        System.out.printf("Cuadrado: Color: %s, Lado: %.2f, Área: %.2f, Perímetro: %.2f%n",
                         color, getLado(), calcularArea(), calcularPerimetro());
    }
}

// Triángulo - non-sealed (permite extensiones abiertas)
public non-sealed class Triangulo extends Forma {
    protected double lado1;
    protected double lado2;
    protected double lado3;
    
    public Triangulo(String color, double lado1, double lado2, double lado3) {
        super(color);
        if (lado1 <= 0 || lado2 <= 0 || lado3 <= 0) {
            throw new IllegalArgumentException("Los lados deben ser positivos");
        }
        if (!esTrianguloValido(lado1, lado2, lado3)) {
            throw new IllegalArgumentException("Los lados no forman un triángulo válido");
        }
        this.lado1 = lado1;
        this.lado2 = lado2;
        this.lado3 = lado3;
    }
    
    private boolean esTrianguloValido(double a, double b, double c) {
        return (a + b > c) && (a + c > b) && (b + c > a);
    }
    
    @Override
    public double calcularArea() {
        // Fórmula de Herón
        double s = calcularPerimetro() / 2;
        return Math.sqrt(s * (s - lado1) * (s - lado2) * (s - lado3));
    }
    
    @Override
    public double calcularPerimetro() {
        return lado1 + lado2 + lado3;
    }
}

// Ejemplo de extensión del triángulo non-sealed
class TrianguloEquilatero extends Triangulo {
    public TrianguloEquilatero(String color, double lado) {
        super(color, lado, lado, lado);
    }
    
    @Override
    public void mostrarInfo() {
        System.out.printf("Triángulo Equilátero: Color: %s, Lado: %.2f, Área: %.2f%n",
                         color, lado1, calcularArea());
    }
}

// Clase para demostrar el uso
public class PracticaClasesSelladasFormas {
    public static void main(String[] args) {
        PracticaClasesSelladasFormas demo = new PracticaClasesSelladasFormas();
        demo.demostrarFormas();
    }
    
    public void demostrarFormas() {
        System.out.println("=== DEMOSTRACIÓN DE CLASES SELLADAS ===");
        
        // Crear diferentes formas
        var formas = new Forma[] {
            new Circulo("Rojo", 5.0),
            new Rectangulo("Azul", 4.0, 6.0),
            new Cuadrado("Verde", 4.0),
            new Triangulo("Amarillo", 3.0, 4.0, 5.0),
            new TrianguloEquilatero("Naranja", 6.0)
        };
        
        // Mostrar información de todas las formas
        for (var forma : formas) {
            forma.mostrarInfo();
        }
        
        // Demostrar control de herencia
        System.out.println("\n=== CONTROL DE HERENCIA ===");
        
        // Esto funciona - tipos permitidos
        Forma circulo = new Circulo("Negro", 3.0);
        Rectangulo cuadrado = new Cuadrado("Blanco", 5.0);
        
        // Esto funciona - triángulo es non-sealed
        Triangulo trianguloEspecial = new TrianguloEquilatero("Púrpura", 4.0);
        
        System.out.println("Todas las formas creadas correctamente");
        System.out.println("Control de herencia funcionando como se esperaba");
        
        // Demostrar cálculos
        System.out.println("\n=== CÁLCULOS ESPECÍFICOS ===");
        calcularTotalArea(formas);
    }
    
    private void calcularTotalArea(Forma[] formas) {
        double areaTotal = 0;
        
        for (var forma : formas) {
            double area = forma.calcularArea();
            areaTotal += area;
            
            // Ejemplo de tratamiento específico por tipo (PATTERN MATCHING)
            switch (forma) {
                case Circulo c -> 
                    System.out.printf("Círculo con radio %.1f: área = %.2f%n", 
                                     c.getRadio(), area);
                case Cuadrado c -> 
                    System.out.printf("Cuadrado con lado %.1f: área = %.2f%n", 
                                     c.getLado(), area);
                case Rectangulo r -> 
                    System.out.printf("Rectángulo %.1fx%.1f: área = %.2f%n", 
                                     r.getAncho(), r.getAlto(), area);
                case Triangulo t -> 
                    System.out.printf("Triángulo: área = %.2f%n", area);
            }
        }
        
        System.out.printf("Área total: %.2f%n", areaTotal);
    }
}
```

</details>

## 5. Ejemplo práctico combinado

```java
// Record para datos del usuario
record Usuario(String nombre, String email) {
    public Usuario {
        if (nombre == null || nombre.trim().isEmpty()) {
            throw new IllegalArgumentException("Nombre requerido");
        }
    }
}

// Clase sellada para tipos de notificación
public sealed class Notificacion 
    permits Email, SMS {
    
    protected String mensaje;
    protected Usuario destinatario;
    
    public Notificacion(String mensaje, Usuario destinatario) {
        this.mensaje = mensaje;
        this.destinatario = destinatario;
    }
    
    public abstract void enviar();
}

public final class Email extends Notificacion {
    private String asunto;
    
    public Email(String mensaje, Usuario destinatario, String asunto) {
        super(mensaje, destinatario);
        this.asunto = asunto;
    }
    
    @Override
    public void enviar() {
        System.out.printf("📧 Email a %s: %s%n", 
                         destinatario.nombre(), asunto);
    }
}

public final class SMS extends Notificacion {
    public SMS(String mensaje, Usuario destinatario) {
        super(mensaje, destinatario);
    }
    
    @Override
    public void enviar() {
        System.out.printf("📱 SMS a %s: %s%n", 
                         destinatario.nombre(), mensaje);
    }
}

public class SistemaNotificaciones {
    public static void main(String[] args) {
        // Usar var para tipos complejos
        var usuario = new Usuario("Ana García", "ana@email.com");
        
        var notificaciones = new Notificacion[] {
            new Email("Bienvenido", usuario, "¡Hola!"),
            new SMS("Código: 123456", usuario)
        };
        
        // Procesar con pattern matching
        for (var notif : notificaciones) {
            switch (notif) {
                case Email e -> {
                    System.out.println("Procesando email...");
                    e.enviar();
                }
                case SMS s -> {
                    System.out.println("Procesando SMS...");
                    s.enviar();
                }
            }
        }
    }
}
```

> [!NOTE]
> Has completado la introducción a las características modernas de Java. Estos conceptos (var, records y clases selladas) te serán muy útiles para escribir código más limpio, expresivo y mantenible. En el próximo tema de Programación Funcional, verás cómo estas características se integran perfectamente con el paradigma funcional.

<p align="center">📚 <em>Fin del Anexo I - Inferencia de tipos, records y clases selladas</em></p>