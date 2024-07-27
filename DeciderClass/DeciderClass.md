# Explicación intermedia del script DeciderClass.cs para EPLAN P8

## Propósito del script

Este script de prueba en C# para EPLAN P8 demuestra dos funcionalidades principales:
1. Mostrar un cuadro de diálogo de decisión simple (OK/Cancelar).
2. Abrir un selector de archivos con opciones personalizadas.

## Estructura y funcionamiento del script

### 1. Importaciones y declaración de clase

```csharp
using Eplan.EplApi.Base;
using Eplan.EplApi.Scripting;

class DeciderClass
{
    // ... (contenido de la clase)
}
```

El script importa las bibliotecas necesarias de EPLAN y define la clase `DeciderClass`.

### 2. Método principal

```csharp
[Start]
public void Function()
{
    // ... (código del método)
}
```

Este método, marcado con el atributo `[Start]`, es el punto de entrada del script.

### 3. Cuadro de diálogo de decisión

```csharp
Decider decider = new Decider();
EnumDecisionReturn decision = decider.Decide(
    EnumDecisionType.eOkCancelDecision,
    "This is the text",
    "Title",
    EnumDecisionReturn.eOK,
    EnumDecisionReturn.eOK);

switch (decision)
{
    case EnumDecisionReturn.eOK:
        // OK
        break;
    case EnumDecisionReturn.eCANCEL:
        // Cancel
        break;
}
```

Este bloque de código:
- Crea un objeto `Decider`.
- Llama al método `Decide` con varios parámetros para configurar el cuadro de diálogo.
- Utiliza un `switch` para manejar la respuesta del usuario.

### 4. Selector de archivos

```csharp
FileSelectDecisionContext fileContext = new FileSelectDecisionContext("MySelector", EnumDecisionReturn.eCANCEL);
fileContext.Title = "Title";
fileContext.CustomDefaultPath = @"C:\MyDefaultPath";
fileContext.OpenFileFlag = true;
fileContext.AllowMultiSelect = true;
fileContext.DefaultExtension = "xml";
fileContext.AddFilter("XML files (*.xml)", "*.xml");
fileContext.AddFilter("All files (*.*)", "*.*");

Decider oDecision = new Decider();
EnumDecisionReturn eAnswer = oDecision.Decide(fileContext);
if (eAnswer != EnumDecisionReturn.eOK)
{
    foreach (string file in fileContext.GetFiles())
    {
        // do with file
    }
}
```

Este bloque:
- Crea y configura un objeto `FileSelectDecisionContext` para personalizar el selector de archivos.
- Utiliza otro objeto `Decider` para mostrar el selector de archivos.
- Si el usuario selecciona archivos (OK), itera sobre los archivos seleccionados.

## Aspectos técnicos destacables

1. **Uso de enumeraciones**: El script utiliza enumeraciones como `EnumDecisionType` y `EnumDecisionReturn` para manejar tipos de decisiones y respuestas de manera tipada.

2. **Configuración del selector de archivos**: El script demuestra cómo configurar un selector de archivos personalizado, incluyendo la configuración de filtros, rutas por defecto y opciones de selección múltiple.

3. **Manejo de respuestas del usuario**: Tanto para el cuadro de diálogo simple como para el selector de archivos, el script incluye lógica para manejar las diferentes respuestas posibles del usuario.

## Uso del script

1. Carga el script en EPLAN a través de [Utilidades] > [Scripts] > [Ejecutar].
2. El script mostrará primero un cuadro de diálogo simple.
3. Luego, abrirá un selector de archivos personalizado.

