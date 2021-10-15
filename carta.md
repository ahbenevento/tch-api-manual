# Tu Carta Hoy - REST API

**Versión 1**

## Preparación y actualización de una carta

1.  [Renderizar interfaz Web](#renderizar-interfaz-web)
2.  [Actualizar carta desde archivo](#actualizar-carta-desde-archivo)

### Renderizar interfaz Web

**Descripción**

El renderizado de la interfaz Web crea en el espacio de trabajo de la cuenta cliente todos los archivos necesarios para poder acceder al menú de la carta desde un enlace.

Este proceso debe lanzarse luego de registrar la cuenta y cada vez que se modifique alguno de sus datos.

**Endpoint**

**GET** `/carte/prepare_ui/{customerId}`

`{customerId}` es el ID único obtenido al registrar la cuenta cliente.

*Header*

```
Authorization: *****
Content-Type: application/json
```

**Retorna**

Un objeto con las direcciones Web de acceso a la carta.

```json
{
    "error": null,
    "messages": [],
    "result": {
        "url": "https:\/\/...\/cartas\/cuenta-cliente",
        "adminUrl": "https:\/\/...\/cartas\/cuenta-cliente\/gestion\/carta"
    }
}
```

### Actualizar carta desde archivo

**Descripción**

Permite actualizar la carta mendiante una planilla de cálculo **Microsoft Excel**. Los formatos soportados son los publicados en las versiones 2003 en adelante (archivos con extesión `.xls` y `.xlsx`).

**Endpoint**

**POST** `/carte/update_from_xls/{customerId}`

`{customerId}` es el ID único obtenido al registrar la cuenta cliente.

*Header*

```
Authorization: *****
Content-Type: application/vnd.ms-excel | vnd.openxmlformats-officedocument.spreadsheetml.sheet
```

*Body*

El contenido del archivo.

**Retorna**

Un objeto con la dirección Web a la última planilla procesada.

```json
{
    "error": null,
    "messages": [],
    "result": {
        "urlLastSpreadsheet": "https:\/\/...\/cartas\/cuenta-cliente/carta/archivo.xlsx"
    }
}
```

### Actualizar carta desde URL

**Descripción**

Permite actualizar la carta desde una URL a una planilla de cálculo **Microsoft Excel**. Los formatos soportados son los publicados en las versiones 2003 en adelante (archivos con extesión `.xls` y `.xlsx`).

**Endpoint**

**POST** `/carte/update_from_url/{customerId}`

`{customerId}` es el ID único obtenido al registrar la cuenta cliente.

*Header*

```
Authorization: *****
Content-Type: application/json
```

*Body*

```json
{
    "spreadsheetUrl": "https://...",
}
```

**Retorna**

Un objeto con la dirección Web a la última planilla procesada.

```json
{
    "error": null,
    "messages": [],
    "result": {
        "urlLastSpreadsheet": "https:\/\/...\/cartas\/cuenta-cliente/carta/archivo.xlsx"
    }
}
```
