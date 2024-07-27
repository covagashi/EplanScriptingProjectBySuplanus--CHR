# Explicación intermedia del script ExecuteEplanAction.cs para EPLAN P8

## Propósito del script

Este script crea una interfaz de usuario que permite al usuario ejecutar acciones de EPLAN introduciendo comandos en un cuadro de texto. Proporciona retroalimentación visual sobre la validez del comando y permite su ejecución.

## Estructura y componentes principales

### 1. Importaciones y declaración de clase

```csharp
using System.Drawing;
using System.Windows.Forms;
using Eplan.EplApi.ApplicationFramework;
using Eplan.EplApi.Scripting;

public partial class frmExecuteEplanAction : Form
{
    // ... (contenido de la clase)
}
```

El script utiliza Windows Forms para la interfaz de usuario y las bibliotecas de EPLAN para la ejecución de acciones.

### 2. Componentes de la interfaz de usuario

```csharp
private Button btnCancel;
private Button btnOk;
private TextBox txtAction;
private CommandLineInterpreter oCLI = new CommandLineInterpreter();
```

Define los controles principales de la interfaz y un intérprete de línea de comandos de EPLAN.

### 3. Inicialización de componentes

El método `InitializeComponent()` (generado por el diseñador de Windows Forms) configura la disposición y propiedades de los controles en la interfaz.

### 4. Métodos para integración con EPLAN

```csharp
[DeclareMenu]
public void MenuFunction()
{
    // ... (código para añadir elemento de menú)
}

[DeclareAction("ExecuteEplanAction")]
public void Function()
{
    // ... (código para mostrar el formulario)
}
```

Estos métodos utilizan atributos específicos de EPLAN para integrar el script en la interfaz de EPLAN.

### 5. Manejo de eventos

```csharp
private void btnCancel_Click(object sender, System.EventArgs e)
{
    this.Close();
}

private void btnOk_Click(object sender, System.EventArgs e)
{
    oCLI.Execute(txtAction.Text);
    this.Close();
}

private void txtAction_TextChanged(object sender, System.EventArgs e)
{
    // ... (código para validar la acción)
}
```

Estos métodos manejan los eventos de la interfaz de usuario, como clics en botones y cambios en el texto.

## Funcionalidad clave

### Validación de comandos en tiempo real

```csharp
private void txtAction_TextChanged(object sender, System.EventArgs e)
{
    bool bRet = oCLI.IsExecutable(txtAction.Text);
    if (bRet)
    {
        txtAction.BackColor = Color.LightGreen;
        btnOk.Enabled = true;
    }
    else
    {
        txtAction.BackColor = Color.LightSalmon;
        btnOk.Enabled = false;
    }
}
```

Este método verifica en tiempo real si el comando ingresado es ejecutable en EPLAN. Proporciona retroalimentación visual cambiando el color de fondo del cuadro de texto y habilitando/deshabilitando el botón OK.

### Ejecución de comandos

```csharp
private void btnOk_Click(object sender, System.EventArgs e)
{
    oCLI.Execute(txtAction.Text);
    this.Close();
}
```

Cuando se hace clic en OK, el comando ingresado se ejecuta utilizando el intérprete de línea de comandos de EPLAN.

## Aspectos técnicos destacables

1. **Uso de Windows Forms**: El script crea una interfaz de usuario utilizando Windows Forms, lo que permite una interacción más rica con el usuario.

2. **Integración con EPLAN**: Utiliza atributos como `[DeclareMenu]` y `[DeclareAction]` para integrar el script en la interfaz de EPLAN.

3. **Validación en tiempo real**: Implementa una validación de comandos en tiempo real, proporcionando retroalimentación visual inmediata al usuario.

4. **Manejo de eventos**: Demuestra cómo manejar diferentes eventos de la interfaz de usuario, como clics de botón y cambios de texto.

5. **Uso del CommandLineInterpreter**: Utiliza la clase `CommandLineInterpreter` de EPLAN para validar y ejecutar comandos.

## Uso del script

1. Al cargar el script en EPLAN, se añadirá un nuevo elemento de menú "EPLAN Action To Run...".
2. Al seleccionar este elemento, se abrirá una ventana donde el usuario puede ingresar comandos de EPLAN.
3. La interfaz proporciona retroalimentación visual sobre la validez del comando ingresado.
4. El usuario puede ejecutar el comando válido haciendo clic en OK o cancelar la operación.

Este script es un ejemplo avanzado de cómo crear herramientas personalizadas para EPLAN que combinan una interfaz de usuario intuitiva con la potencia de la API de scripting de EPLAN.
