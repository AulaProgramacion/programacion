# RESUMEN JAVA NIO

## 🗺️ Representación y manejo de rutas

El núcleo de NIO.2 no trabaja con `String` ni `File`, sino con la interfaz `Path`.

| Interfaz / Clase | Propósito y características | Métodos principales |
| --- | --- | --- |
| **`Path`** | Interfaz que representa una ruta (absoluta o relativa) en el sistema de ficheros. Puede apuntar a un fichero, directorio o symlink (exista físicamente o no). | `toString()`, `getFileName()`, `getParent()`, `toAbsolutePath()`.<br>

<br>`normalize()`: Elimina redundancias como `.` o `..`.<br>

<br>`resolve(Path)`: Une dos rutas (añade la 2ª al final de la 1ª).<br>

<br>`relativize(Path)`: Calcula la ruta relativa entre dos paths. |
| **`Paths` / `Path` (Java 11+)** | Factorías (clases con métodos estáticos) para instanciar objetos `Path`. | `Paths.get("ruta", "al", "fichero")` o la versión más moderna `Path.of("ruta", "al", "fichero")`. |
| **Conversión** | Interoperabilidad con código legado de `java.io.File`. | `miPath.toFile()` y `miFile.toPath()`. |

---

## 🛠️ Operaciones sobre el sistema de ficheros (`Files`)

La clase utilitaria **`Files`** proporciona métodos estáticos para casi cualquier operación. A diferencia de la antigua API, estos métodos lanzan excepciones claras (como `IOException`, `NoSuchFileException`, `FileAlreadyExistsException`) si algo falla.

**1. COMPROBACIONES Y METADATOS** (No suelen lanzar excepción al comprobar)

| Acción | Métodos principales |
| --- | --- |
| **Existencia y Tipo** | `Files.exists(path)`, `Files.notExists(path)`, `Files.isRegularFile(path)`, `Files.isDirectory(path)`. *(Devuelven booleanos)*. |
| **Permisos básicos** | `Files.isReadable(path)`, `Files.isWritable(path)`, `Files.isExecutable(path)`. |
| **Metadatos** *(Estos sí lanzan IOException)* | `Files.size(path)`, `Files.getLastModifiedTime(path)`, `Files.getOwner(path)`, `Files.probeContentType(path)` (ej. "text/plain"). |

**2. GESTIÓN DE FICHEROS Y DIRECTORIOS**

| Acción | Métodos principales y consideraciones |
| --- | --- |
| **Crear** | `Files.createFile(path)`: Falla si ya existe.<br>

<br>`Files.createDirectory(path)`: Falla si el padre no existe.<br>

<br>`Files.createDirectories(path)`: **Muy útil.** Crea toda la jerarquía necesaria de forma idempotente (no falla si ya existen). |
| **Eliminar** | `Files.delete(path)`: Falla si no existe o si es un directorio con contenido.<br>

<br>`Files.deleteIfExists(path)`: Más segura, no lanza excepción si no existe. |
| **Copiar** | `Files.copy(origen, destino, opciones)`. Opciones comunes: `StandardCopyOption.REPLACE_EXISTING` o `COPY_ATTRIBUTES`. *Nota: si es un directorio, solo copia la carpeta vacía, no su contenido*. |
| **Mover / Renombrar** | `Files.move(origen, destino, opciones)`. Sirve para cambiar de ruta o cambiar el nombre. Es mucho más fiable que el antiguo `File.renameTo()`. |

---

## 📂 Exploración de directorios

NIO ofrece formas mucho más potentes de listar contenidos que el antiguo `File.list()`.

| Acción | Métodos principales | Iteración |
| --- | --- | --- |
| **Listar nivel actual** (Superficial) | `Files.newDirectoryStream(dir)` o filtrando `Files.newDirectoryStream(dir, "*.txt")`. | Devuelve un `DirectoryStream<Path>` que implementa `Iterable`. Se usa en un `try-with-resources` iterando con un `for(Path p : stream)`. |
| **Recorrido Recursivo** (Profundo) | `Files.walk(raiz)`: Devuelve todo el árbol.<br>

<br>`Files.find(...)`: Recorre aplicando un filtro basado en los atributos del fichero. | Devuelven un `Stream<Path>` (API de Streams de Java), lo que permite concatenar `.filter()`, `.map()`, `.forEach()`, etc. |

---

## 📖 Integración con streams de texto (lectura / escritura)

La clase `Files` también incluye métodos de conveniencia para leer/escribir texto rápidamente, soportando la especificación de la codificación (ej. `StandardCharsets.UTF_8`).

| Enfoque | Métodos de `Files` para Lectura / Escritura |
| --- | --- |
| **Alta nivel (Todo en memoria)**<br>

<br>*(Solo para ficheros pequeños/medianos)* | `Files.readAllLines()`: Devuelve `List<String>`.<br>

<br>`Files.readString()` (Java 11+): Devuelve el texto completo.<br>

<br>`Files.write()` (con `List<String>`) o `Files.writeString()`. Soportan `StandardOpenOption.APPEND`. |
| **Bajo nivel (Con buffer)**<br>

<br>*(Para ficheros grandes o rendimiento)* | `Files.newBufferedReader(path, StandardCharsets.UTF_8)`.<br>

<br>`Files.newBufferedWriter(path, StandardCharsets.UTF_8, StandardOpenOption...)`. (Esta es la forma recomendada de integrar NIO con la E/S tradicional de caracteres). |