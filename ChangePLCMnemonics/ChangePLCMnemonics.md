# Explicación avanzada del script ChangePLCMnemonics.cs para EPLAN P8

## Propósito del script

Este script en C# para EPLAN P8 crea una acción que permite cambiar los mnemónicos de E/S de PLC en las "Direcciones / Listas de asignación". Específicamente, permite cambiar entre los formatos "E" y "A" a "I" y "Q", o viceversa.

## Estructura y funcionamiento del script

### 1. Declaraciones e importaciones

```csharp
using System.Windows.Forms;
using Eplan.EplApi.ApplicationFramework;
using Eplan.EplApi.Scripting;
```

Estas líneas importan los espacios de nombres necesarios para trabajar con formularios de Windows y la API de EPLAN.

### 2. Definición de la clase principal

```csharp
public class NAIROLF_ContextMenu_ChangePLCMnemonics
{
    public static string sSourceText = string.Empty;
    // ... (resto del código)
}
```

Esta clase contiene toda la lógica del script. La variable `sSourceText` se usa para almacenar temporalmente el texto que se va a modificar.

### 3. Método principal para cambiar mnemónicos

```csharp
[DeclareAction("NAIROLF_ChangePLCMnemonics")]
public void ChangePLCMnemonik(string DestMnemonik)
{
    // ... (código del método)
}
```

Este método es el núcleo del script. Realiza las siguientes operaciones:
1. Verifica si se ha especificado un mnemónico de destino.
2. Limpia el portapapeles y copia el contenido seleccionado en EPLAN.
3. Reemplaza los mnemónicos en el texto copiado según el destino especificado.
4. Pega el texto modificado de vuelta en EPLAN.

### 4. Lógica de reemplazo de mnemónicos

```csharp
switch (DestMnemonik)
{
    case "IQ":
        sSourceText = sSourceText.Replace("E", "I").Replace("A", "Q");
        break;
    case "EA":
        sSourceText = sSourceText.Replace("I", "E").Replace("Q", "A");
        break;
    default:
        return;
}
```

Este switch determina qué reemplazos hacer basándose en el mnemónico de destino especificado.

### 5. Creación de menús contextuales

```csharp
[DeclareMenu()]
public void CreateContextMenus()
{
    // ... (código para crear menús contextuales)
}
```

Este método crea dos entradas de menú contextual en EPLAN:
1. Para cambiar de E/A a I/Q
2. Para cambiar de I/Q a E/A

Utiliza la API de EPLAN para agregar estos elementos al menú contextual del diálogo "XPlcIoDataDlg".

## Aspectos técnicos destacables

1. **Uso de atributos**: Los atributos `[DeclareAction]` y `[DeclareMenu]` son específicos de EPLAN y se utilizan para registrar acciones y menús en el sistema.

2. **Manejo del portapapeles**: El script utiliza el portapapeles de Windows como un intermediario para modificar el texto seleccionado en EPLAN.

3. **Manejo de errores**: El script utiliza bloques try-catch para manejar posibles errores, mostrando mensajes de error en caso de que ocurran.

4. **Interfaz de usuario**: Aunque es un script de backend, interactúa con el usuario a través de mensajes y menús contextuales.

## Uso del script

1. Carga el script en EPLAN a través de [Utilidades] > [Scripts] > [Cargar].
2. Una vez cargado, aparecerán nuevas opciones en el menú contextual del diálogo de datos de E/S del PLC.
3. Selecciona el texto que deseas modificar y usa una de las opciones del menú contextual para cambiar los mnemónicos.


