# RESUMEN ENTRADA/SALIDA EN FICHEROS DE TEXTO PLANO Y BINARIOS

## 📄 Ficheros de Texto (Caracteres)

Estas clases trabajan con secuencias de caracteres legibles por humanos y derivan principalmente de las clases abstractas `Writer` y `Reader`.

**1. ESCRITURA DE TEXTO (Derivadas de `Writer`)**

| Clase | Propósito y características | Métodos principales | Iteración / Cierre |
| --- | --- | --- | --- |
| **`PrintWriter`** | Es la clase más cómoda para escribir con formato. Puede escribir cualquier tipo de dato convirtiéndolo a texto. Por defecto, sobreescribe el fichero. | `print()`, `println()`, `printf()`, `flush()`, `close()`. | Se recomienda usar `try-with-resources` para asegurar el cierre automático. |
| **`FileWriter`** | Escribe caracteres en un fichero. Su mayor utilidad es permitir el **modo append** (añadir al final sin borrar) pasándole `true` al constructor: `new FileWriter("f.txt", true)`. | Se suele usar envolviéndola en otras clases (`BufferedWriter` o `PrintWriter`). | N/A |
| **`BufferedWriter`** | Añade un buffer en memoria para mejorar el rendimiento, reduciendo las operaciones de disco. Ideal para escribir muchas líneas. | `write(String)`, `newLine()` (salto de línea del SO), `flush()`, `close()`. | Volcar a disco con `flush()` o al cerrar con `close()`. |

---

**2. LECTURA DE TEXTO (Derivadas de `Reader` y `Scanner`)**

| Clase | Propósito y características | Métodos principales | Iteración para leer todo |
| --- | --- | --- | --- |
| **`Scanner`** | Muy versátil para leer datos estructurados por tokens (separados por espacios, saltos de línea o delimitadores personalizados con `useDelimiter()`). Se instancia pasando un objeto `File`. | `next()`, `nextInt()`, `nextDouble()`, `nextLine()`, `hasNext()`, `hasNextLine()`. | Bucle condicional: `while(scanner.hasNextLine()) { ... }`. *Ojo: si usas `nextInt()`, debes usar un `nextLine()` extra para consumir el salto de línea residual*. |
| **`FileReader`** | Lectura básica a bajo nivel. Lee carácter a carácter. | `read()` (devuelve un `int`), `close()`. | Bucle hasta -1: `while((caracter = fr.read()) != -1)`. Se debe castear el `int` a `char`. |
| **`BufferedReader`** | Añade buffer a un `Reader` (como `FileReader`), mejorando enormemente el rendimiento. Es la mejor opción para leer un fichero línea a línea. | `readLine()` (lee la línea entera sin el salto), `close()`. | Bucle hasta null: `while((linea = br.readLine()) != null) { ... }`. |

---

## 📦 Ficheros Binarios (Bytes)

Estas clases trabajan con el formato binario nativo (más eficiente pero no legible directamente) y derivan de `OutputStream` e `InputStream`.

**3. ESCRITURA BINARIA (Derivadas de `OutputStream`)**

| Clase | Propósito y características | Métodos principales |
| --- | --- | --- |
| **`FileOutputStream`** | Escritura directa byte a byte en disco. Permite modo append igual que `FileWriter`. | `write(int b)`, `write(byte[] b)`, `flush()`, `close()`. |
| **`DataOutputStream`** | Permite escribir tipos de datos primitivos (`int`, `double`, etc.) y `String` directamente. Es una envoltura sobre `FileOutputStream`. | `writeInt()`, `writeDouble()`, `writeBoolean()`, `writeUTF()` (para Strings), `size()`. |
| **`ObjectOutputStream`** | Permite la **serialización**: guardar objetos Java completos en disco. | `writeObject(Object obj)`. |

---

**4. LECTURA BINARIA (Derivadas de `InputStream`)**

| Clase | Propósito y características | Métodos principales | Iteración para leer todo |
| --- | --- | --- | --- |
| **`FileInputStream`** | Lectura directa byte a byte desde disco. | `read()` (devuelve `int` de 0 a 255), `close()`. | Bucle hasta -1: `while((byteLeido = fis.read()) != -1)`. |
| **`DataInputStream`** | Lee datos primitivos escritos por `DataOutputStream`. **Deben leerse en el mismo orden estricto** en el que se escribieron. | `readInt()`, `readDouble()`, `readBoolean()`, `readUTF()`. | Opción 1: `while(dis.available() > 0)` (estimación de bytes). <br>

<br>Opción 2 (más robusta): Bucle infinito `while(true)` atrapando la excepción `EOFException` para detectar el fin de fichero. |
| **`ObjectInputStream`** | Permite la **deserialización**: reconstruir objetos Java desde bytes. | `readObject()` (devuelve un `Object` genérico que requiere casting). | Similar a `DataInputStream`, requiere atrapar `ClassNotFoundException` por si la clase no existe en el proyecto. |

---

### ⚠️ Requisito fundamental: La interfaz `Serializable`

Para poder usar los métodos `writeObject()` y `readObject()`, es **estrictamente necesario** que las clases de los objetos implicados implementen la interfaz `java.io.Serializable`.

* Es una interfaz "marcador" (no requiere implementar ningún método) que avisa a Java de que la clase puede ser convertida a bytes.
* Si intentas serializar un objeto de una clase que no lo implementa, Java lanzará una `NotSerializableException`.
* Además, es una buena práctica declarar explícitamente el atributo `private static final long serialVersionUID = 1L;` para controlar la compatibilidad de versiones de la clase en el futuro.
* Si hay algún campo sensible (como una contraseña) que no quieres guardar en el fichero, debes marcarlo con el modificador `transient`.