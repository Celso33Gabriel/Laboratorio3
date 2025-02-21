# **Análisis del Programa**

### 1. Tareas Repetitivas o que pueden encapsularse en funciones

En el programa proporcionado, se identifican varias tareas repetitivas que podrían encapsularse en funciones para mejorar la modularidad y reutilización del código. Algunas de estas tareas son:

- **Agregar estudiante**: Actualmente, la adición de un estudiante y su calificación se hace directamente en la estructura del `if`. Esto puede encapsularse en una función independiente.
- **Mostrar la lista de estudiantes**: Se usa un bucle para recorrer la lista de estudiantes y calificaciones, lo cual podría ser una función separada.
- **Calcular promedio de calificaciones**: La sumatoria y división de las calificaciones podría estar en una función para mejorar la claridad del código.
- **Encontrar al estudiante con la calificación más alta**: Actualmente, el código recorre la lista en una estructura `if`, pero podría implementarse como una función independiente.

### 2. Variables Locales vs Variables Globales

#### Variables Globales:

El programa usa las siguientes variables globales:

- `List<string> estudiantes`
- `List<double> calificaciones`

Estas variables deben ser accesibles en todo el programa porque contienen la información clave sobre los estudiantes y sus calificaciones.

#### Variables Locales:

Las variables locales se usan dentro del `Main`, como:

- `opcion` (para capturar la elección del usuario).
- `nombre` y `calificacion` (usadas dentro de la opción 1).
- `suma` y `promedio` (en la opción 3).
- `maxCalificacion` y `estudianteMax` (en la opción 4).

Para mejorar la claridad y evitar el uso excesivo de variables globales, se recomienda que estas variables sean locales dentro de funciones específicas.

---

**Modularización**

### 1. Convertir el Programa en Funciones

Se recomienda dividir el código en funciones como las siguientes:

```csharp
static void AgregarEstudiante()
{
    Console.Write("Ingrese el nombre del estudiante: ");
    string nombre = Console.ReadLine();
    Console.Write("Ingrese la calificación del estudiante: ");
    if (double.TryParse(Console.ReadLine(), out double calificacion))
    {
        estudiantes.Add(nombre);
        calificaciones.Add(calificacion);
        Console.WriteLine("Estudiante agregado correctamente.");
    }
    else
    {
        Console.WriteLine("Entrada inválida. Ingrese una calificación válida.");
    }
}
```

```csharp
static void MostrarEstudiantes()
{
    if (estudiantes.Count == 0)
    {
        Console.WriteLine("No hay estudiantes registrados.");
    }
    else
    {
        Console.WriteLine("\nLista de estudiantes:");
        for (int i = 0; i < estudiantes.Count; i++)
        {
            Console.WriteLine($"{estudiantes[i]} - Calificación: {calificaciones[i]}");
        }
    }
}
```

```csharp
static void CalcularPromedio()
{
    if (calificaciones.Count == 0)
    {
        Console.WriteLine("No hay calificaciones registradas.");
    }
    else
    {
        double suma = 0;
        foreach (double calificacion in calificaciones)
        {
            suma += calificacion;
        }
        double promedio = suma / calificaciones.Count;
        Console.WriteLine($"El promedio de calificaciones es: {promedio}");
    }
}
```

```csharp
static void MostrarEstudianteConMaxCalificacion()
{
    if (calificaciones.Count == 0)
    {
        Console.WriteLine("No hay calificaciones registradas.");
    }
    else
    {
        double maxCalificacion = calificaciones[0];
        string estudianteMax = estudiantes[0];
        for (int i = 1; i < calificaciones.Count; i++)
        {
            if (calificaciones[i] > maxCalificacion)
            {
                maxCalificacion = calificaciones[i];
                estudianteMax = estudiantes[i];
            }
        }
        Console.WriteLine($"El estudiante con la calificación más alta es: {estudianteMax} con {maxCalificacion}");
    }
}
```

Estas funciones modularizan el código, haciéndolo más limpio y fácil de mantener.

---

**Preguntas Guía**

1. **¿Qué ventajas tiene dividir el código en funciones?**

   - Mejora la organización y claridad.
   - Permite reutilizar el código en diferentes partes del programa.
   - Facilita la depuración y prueba de componentes individuales.
   - Reduce la repetición de código.

2. **¿Por qué es importante limitar el uso de variables globales?**

   - Evita errores inesperados debido a modificaciones en diferentes partes del programa.
   - Facilita la depuración y mantenimiento del código.
   - Permite que las funciones sean más independientes y reutilizables.

3. **¿Cómo se puede mejorar la legibilidad del código?**

   - Usar nombres de variables y funciones descriptivos.
   - Agregar comentarios para explicar la lógica del código.
   - Usar indentación y espacios adecuados.
   - Evitar estructuras demasiado anidadas.

---

**Mejoras Adicionales**

### Validación de Entradas del Usuario

Actualmente, el programa no maneja errores si el usuario ingresa texto en lugar de un número. Se puede mejorar con:

```csharp
Console.Write("Ingrese la calificación del estudiante: ");
if (double.TryParse(Console.ReadLine(), out double calificacion))
{
    calificaciones.Add(calificacion);
}
else
{
    Console.WriteLine("Entrada inválida. Ingrese un número.");
}
```

Esto evita que el programa se bloquee si el usuario ingresa un valor incorrecto.

---

### **Conclusión**
La modularización del programa ayuda a mejorar su estructura, mantenimiento y reutilización. Además, al limitar el uso de variables globales y mejorar la validación de datos, se consigue un código más robusto y menos propenso a errores.





