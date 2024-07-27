# Explicación del script AutomaticGeneratingConnections.cs para EPLAN P8

## ¿Qué hace este script?

Este script de C# para EPLAN P8 realiza las siguientes funciones:

1. Crea manejadores de eventos para actualizar los enchufes (Plugs) en EPLAN.
2. Actualiza automáticamente los datos de conexión cuando el usuario ejecuta el comando de impresión o de exportación a PDF.
3. Asegura que los datos de conexión estén actualizados antes de generar salidas importantes del proyecto.

## Cómo funciona técnicamente

Vamos a desglosar el script en partes más pequeñas para entenderlo mejor:

### 1. Importación de bibliotecas

```csharp
using Eplan.EplApi.ApplicationFramework;
using Eplan.EplApi.Scripting;
```

Estas líneas importan las bibliotecas necesarias de EPLAN para que el script pueda interactuar con el software.

### 2. Definición de la clase

```csharp
public class AutomaticGeneratingConnections
{
    // ... (contenido de la clase)
}
```

Esta es la definición de la clase principal del script. Todo el código estará dentro de esta clase.

### 3. Manejadores de eventos

```csharp
[DeclareEventHandler("onActionStart.String.PrnPrintDialogShow")]
public void ehPrint()
{
    GenerateConnections();
}

[DeclareEventHandler("onActionStart.String.XPdfExportAction")]
public void ehPdf()
{
    GenerateConnections();
}
```

Estos son dos manejadores de eventos:
- `ehPrint()`: Se activa cuando se inicia la acción de mostrar el diálogo de impresión.
- `ehPdf()`: Se activa cuando se inicia la acción de exportar a PDF.

Ambos manejadores llaman a la función `GenerateConnections()`.

### 4. Método para generar conexiones

```csharp
private static void GenerateConnections()
{
    ActionCallingContext acc = new ActionCallingContext();
    acc.AddParameter("TYPE", "CONNECTIONS");
    new CommandLineInterpreter().Execute("generate",acc);
}
```

Este método es el que realmente hace el trabajo de generar las conexiones:
1. Crea un contexto de llamada de acción (`ActionCallingContext`).
2. Agrega un parámetro para especificar que queremos generar conexiones.
3. Utiliza un intérprete de línea de comandos para ejecutar la acción "generate" con el contexto que hemos creado.

## Cómo usar el script

1. Guarda el script como un archivo con extensión `.cs` (por ejemplo, `AutomaticGeneratingConnections.cs`).
2. En EPLAN, ve a [Utilidades] > [Scripts] > [Cargar].
3. Selecciona el archivo del script que acabas de guardar.
4. El script se cargará y estará activo en EPLAN.

Una vez cargado, el script funcionará automáticamente:
- Cuando intentes imprimir (mostrando el diálogo de impresión), se actualizarán las conexiones.
- Cuando intentes exportar a PDF, también se actualizarán las conexiones.

No necesitas hacer nada más; el script se encargará de mantener actualizados los datos de conexión antes de estas acciones importantes.
