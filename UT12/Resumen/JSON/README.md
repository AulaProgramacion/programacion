# CONCEPTOS ESENCIALES LIBRERÍA GSON

## 🚀 Conceptos clave de Gson

* **Serializar (Java → JSON):** Se usa `gson.toJson(objeto)`.
* **Deserializar (JSON → Java):** Se usa `gson.fromJson(json, Clase.class)`.
* **Requisito de clase:** La clase Java **debe** tener un constructor vacío (sin parámetros).
* **Colecciones genéricas:** Para pasar de JSON a una `List<Clase>`, como Java borra los tipos en ejecución, es **imprescindible** usar `TypeToken`.
* **Opciones útiles:** * Usar `new GsonBuilder().setPrettyPrinting().create()` genera un JSON legible con indentación.
* La anotación `@SerializedName("nombre_en_json")` sobre un atributo permite que se llame distinto en Java y en JSON.
* Si marcas un atributo como `transient`, Gson lo ignorará por completo.



---

## 💻 Código esencial: Lista de objetos ↔ Fichero JSON

Este es el patrón estándar y más eficiente para guardar y recuperar listas usando la API moderna NIO.2 (`Files`) y `Gson`.

```java
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import com.google.gson.reflect.TypeToken;
import java.io.*;
import java.lang.reflect.Type;
import java.nio.charset.StandardCharsets;
import java.nio.file.*;
import java.util.List;

public class EsencialGson {
    public static void main(String[] args) {
        // 1. Crear Gson (con formato legible)
        Gson gson = new GsonBuilder().setPrettyPrinting().create();
        Path fichero = Paths.get("usuarios.json");

        // --- ESCRITURA (Lista Java → Fichero JSON) ---
        List<Usuario> listaEscribir = List.of(
            new Usuario("Ana", 28), 
            new Usuario("Carlos", 35)
        );

        try (BufferedWriter bw = Files.newBufferedWriter(fichero, StandardCharsets.UTF_8)) {
            gson.toJson(listaEscribir, bw);
            System.out.println("✅ Lista guardada correctamente en JSON.");
        } catch (IOException e) {
            e.printStackTrace();
        }

        // --- LECTURA (Fichero JSON → Lista Java) ---
        // ⚠️ Obligatorio el TypeToken para saber qué tipo de lista es
        Type tipoLista = new TypeToken<List<Usuario>>() {}.getType();

        try (BufferedReader br = Files.newBufferedReader(fichero, StandardCharsets.UTF_8)) {
            List<Usuario> listaLeida = gson.fromJson(br, tipoLista);
            
            System.out.println("✅ Lista recuperada:");
            for (Usuario u : listaLeida) {
                System.out.println(u);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

// Clase de ejemplo (Recuerda: ¡Constructor vacío obligatorio!)
class Usuario {
    private String nombre;
    private int edad;

    public Usuario() {} 

    public Usuario(String nombre, int edad) {
        this.nombre = nombre;
        this.edad = edad;
    }

    @Override
    public String toString() { return nombre + " (" + edad + ")"; }
}

```