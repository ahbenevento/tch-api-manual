# Tu Carta Hoy - REST API

**Versión 1**

## Gestión de cuentas cliente

1.  [Alta](#alta)
2.  [Modificación](#modificación)
3.  [Borrado](#borrado)

### Alta

**Descripción**

Permite crear una nueva cuenta cliente.

**Endpoint**

**POST** `/customer`

*Header*

```http
Authorization: *****
Content-Type: application/json
```

*Body*

```json
{
    "name": "",
    "email": "",
    "alias": "",
    "slogan": "",
    "logo_url": "https://...",
    "whatsapp": "",
    "options": {
        "sortCategories": false,
        "sortProducts": true
    },
    "ui": {
        "firstMessageChat": "",
        "showProductos": true,
        "titlesRounded": true,
        "colors": {
            "categories": "#000",
            "titleBackground": "#000",
            "products": "#000",
            "productDetails": "#000",
            "background": "#000",
            "elements": "#000",
            "price": "#000"
        }
    }
}
```

**Valores aceptados en la solicitud**

| Nombre | Requerido | Descripción |
|--------|:---------:|-------------|
|`name`|Si|El nombre de la cuenta accesible desde la Web. Puede ser utilizado com subdominio o carpeta, por lo que los espacios y otros caracteres especiales como los acentos no están permitidos.|
|`email`|Si|El correo electrónico utilizado.|
|`alias`|Si|Razón social o nombre de fantasía.|
|`logo_url`|Si|Una URL donde localizar la imagen utilizada como logo de la forma. Los formatos soportados son: `jpg`, `png`, `gif` y `webp`.|
|`logo_url`|Si|Una URL donde localizar la imagen utilizada como logo de la forma. Los formatos soportados son: `jpg`, `png`, `gif` y `webp`.|
|`whatsapp`| |El nro. de teléfono utilizado para WhatsApp.|
|`options`| |Un objeto con las opciones sobre cómo se generará el menú de la carta.|
|`ui`|Si|Un objeto con la configuración de la interfaz Web.|

**Opciones sobre el menú de la carta**

La siguiente tabla describe las propiedades utilizadas en `options`.

| Nombre | Requerido | Predeterminado | Descripción |
|--------|:---------:|:--------------:|-------------|
|`sortCategories`| |`false`|Ordenar alfabéticamente las categorías del menú.|
|`sortProducts`| |`true`|Ordenar alfabéticamente los productos de cada categoría del menú.|

**Configuración de la interfaz Web**

La siguiente tabla describe las propiedades utilizadas en `ui`.

| Nombre | Requerido | Predeterminado | Descripción |
|--------|:---------:|:--------------:|-------------|
|`firstMessageChat`|Si| |El mensaje inicial con el que una nueva conversación se inicia al enviar un pedido por parte del usuario.|
|`showProductos`| |`true`|Indica si inicialmente se debe mostrar la lista de productos desplegada.|
|`titlesRounded`| |`true`|Mostrar titulos con bordes redondeados.|
|`colors`|Si | |La configuración de colores.|

**Configuración de colores para la interfaz Web**

La siguiente tabla describe las propiedades utilizadas en `ui.colors`.

| Nombre | Requerido | Descripción |
|--------|:---------:|-------------|
|`categories`|Si|Color para las categorías.|
|`titleBackground`|Si|Color del fondo de los títulos y categorías.|
|`products`|Si|Color para los productos.|
|`productDetails`|Si|Color para las descripciones de los productos.|
|`background`|Si|Color del fondo de la página Web.|
|`elements`|Si|Color de fondo para los elementos del menú tales como los botones.|
|`price`|Si|Color para todos los importes.|

**Retorna**

Si la operación ha sido realizada con éxito retorna un objeto con la información completa del nuevo cliente, incluyendo su ID único.

### Modificación

**Descripción**

Permite modificar cualquier valor registrado inicialmente al registrar una cuenta cliente.

**Endpoint**

**PUT** `/customer/{customerId}`

`{customerId}` es el ID único obtenido al registrar la cuenta cliente.

*Header*

```http
Authorization: *****
Content-Type: application/json
```

*Body*

```json
{
    "email": "veremos@servidor.com",
    "ui": {
        "colors": {
            "categories": "#fff",
        }
    }
}
```

**Valores aceptados en la solicitud**

Con la excepción de la propiedad `name` la cual no puede modificarse, cualquier otra propiedad puede modificarse mediante esta solicitud. Consulte el [alta de cuenta cliente](#alta).

**Retorna**

Un objeto con la información actualizada del cliente.

### Borrado

**Descripción**

Marca una cuenta cliente como eliminada. Los administradores de la misma ya no podrán acceder ni efectuar ningún tipo de cambio.

**Endpoint**

**DELETE** `/customer/{customerId}`

`{customerId}` es el ID único obtenido al registrar la cuenta cliente.

*Header*

```http
Authorization: *****
```

**Retorna**

Un objeto con la información completa del cliente eliminado.
