# Tu Carta Hoy - REST API

**Versión 1**

## Generalidades

Para poder utilizar la API será necesario contar con una cuenta activa, que consta de un usuario y una contraseña.

Al acceder con las credenciales correctas se obtendrá un *access token* con el cual se podrá consumir cualquiera de los *endpoint* disponibles.

Estos *access token* expiran luego de **24 hs**. Pasado este tiempo será necesario realizar un nuevo *login*.

### Ambientes

-   Desarrollo: `http://pragmatica.com.ar/tch/api/v1`
-   Producción: `falta`

### Valores retornados por la API

Si la solicitud enviada no existe o no puede realizarse sobre una entidad existente en la base de datos retornará un error `HTTP 404`.

Mientras que si las credenciales no son las correctas o bien el *access token* ha expirado el error retornado será `HTTP 401`.

Por el contrario si se produjera un fallo durante la operación el error retornado será `HTTP 500`.

En cualquier otro caso la API siempre retornará un objeto JSON informando el resultado de la operación realizada. Dicho objeto tendrá la siguiente estructura base:

```json
{
    "error": null,
    "messages": [],
    "result": null
}
```

La propiedad `error` será `null` si la solicitud se realiza correctamente. De lo contrario contendrá una cadena con el identificador del error producido. Consulte las siguientes tablas con los errores retornados por la API.

`messages` puede tener una o más línas informando el resultado de una operación. Por lo general se utiliza para describir un error disparado durante la solicitud.

Por último `result` tendrá el valor retornado por la solicitud. En caso de error su valor será siempre `null`.

### Errores retronados por la API

**Generales**

| Error | Descripción |
|-------|-------------|
|`APIERRORID_WRONGDATA`|Los datos esperados no pasaron la validación.|
|`INVALIDACCESSTOKEN`|El *access token* no es válido o ha expirado.|

**Acceso a la API**

| Error | Descripción |
|-------|-------------|
|`ACCOUNTEXISTS`|La cuenta que intenta registrar ya existe.|
|`ACCOUNTNOTEXISTS`|La cuenta no fue encontrada.|
|`OPERATIONNOTALLOWED`|Se está intentando realizar una operación que la cuenta no tiene permitido.|

**Gestión de cuentas cliente**

| Error | Descripción |
|-------|-------------|
|`CUSTOMERNOTEXISTS`|La cuenta cliente no existe.|
|`CUSTOMERALREADYEXISTS`|La cuenta cliente que se intenta registrar ya existe. Recuerde que el nombre y correo electrónico no pueden repetirse.|
|`CUSTOMERDISABLED`|La cuenta cliente ha sido deshabilitada. No podrá actualizar la carta ni su interfaz Web.|

**Actualización de la carta**

| Error | Descripción |
|-------|-------------|
|`WRONGFORMATFILE`|Se intentó actualizar un menú con una planilla con un formato incompatible. Por el momento el único formato aceptado es **Microsoft Excel** a partir de la versión 2003 (extensiones `.xls` y `.xlsx`).|
|`SPREADSHEETEMPTY`|Se intentó actualizar un menú con una planilla vacía. Si posee más de una hoja el proceso solo funciona sobre la primera.|
|`FAILEDTOCREATEJSONMENU`|Se produjo un error al internar crear los archivos necesarios para acceder al menú desde la Web. Lo ideal sería reintentar la operación y comprobar si el error persiste.|
|`UPDATEERROR`|Se produjo un error al internar actualizar el menú de la carta. Lo ideal sería reintentar la operación y comprobar si el error persiste.|
