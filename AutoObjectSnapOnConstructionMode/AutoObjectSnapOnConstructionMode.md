# Explicación del script AutoObjectSnapOnConstructionMode.vb para EPLAN P8

## ¿Qué hace este script?

Este script de Visual Basic para EPLAN P8 realiza la siguiente función:

1. Activa automáticamente la función de "Object Snap" (ajuste de objetos) cuando se entra en el modo de construcción en EPLAN.

## Cómo funciona técnicamente

Vamos a desglosar el script en partes más pequeñas para entenderlo mejor:

### 1. Definición de la clase

```vb
Public Class GedToggleObjectAction_Class
    ' ... (contenido de la clase)
End Class
```

Esta es la definición de la clase principal del script. Todo el código estará dentro de esta clase.

### 2. Manejador de eventos

```vb
<DeclareEventHandler("onActionStart.String.XGedActionToggleConstructionMode")> _
Public Function GedActionToggleConstructionMode(ByVal iEventParameter As IEventParameter) As Long
    ' ... (contenido de la función)
End Function
```

Este es un manejador de eventos que se activa cuando se inicia la acción de cambiar al modo de construcción en EPLAN. El atributo `DeclareEventHandler` especifica qué acción desencadena este manejador.

### 3. Ejecución de la acción

```vb
Dim CLI As New CommandLineInterpreter()
CLI.Execute("XGedToggleObjectSnapAction") 'Object Snap
```

Dentro del manejador de eventos:
1. Se crea un nuevo objeto `CommandLineInterpreter` llamado `CLI`.
2. Se utiliza este intérprete para ejecutar la acción "XGedToggleObjectSnapAction", que activa la función de ajuste de objetos (Object Snap).

## Cómo usar el script

1. Guarda el script como un archivo con extensión `.vb` (por ejemplo, `AutoObjectSnapOnConstructionMode.vb`).
2. En EPLAN, ve a [Utilidades] > [Scripts] > [Cargar].
3. Selecciona el archivo del script que acabas de guardar.
4. El script se cargará y estará activo en EPLAN.

Una vez cargado, el script funcionará automáticamente:
- Cada vez que entres en el modo de construcción en EPLAN, la función de ajuste de objetos (Object Snap) se activará automáticamente.

No necesitas hacer nada más; el script se encargará de activar el Object Snap cada vez que entres en el modo de construcción.

## Nota técnica

Este script está escrito en Visual Basic, a diferencia de los scripts anteriores que estaban en C#. Sin embargo, ambos lenguajes son compatibles con EPLAN P8 para la creación de scripts.
