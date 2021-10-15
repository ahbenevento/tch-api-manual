# Tu Carta Hoy - REST API

**Versión 1**

## Autenticación y acceso

Es necesario contar con un *access token* para poder utilizar esta API. Estos *access token* expiran luego de **24 hs**. Pasado este tiempo será necesario realizar un nuevo *login*.

### Login

**Descripción**

Permite obtener un *access token*.

**Endpoint**

**GET** `/login`

*Header*

```
Content-Type: application/json
```

*Body*

```json
{
    "username": "ck_...",
    "password": "cs_..."
}
```

**Retorna**

Un objeto con el *access token* generado.

```json
{
    "error": null,
    "messages": [],
    "result": {
        "expiresAt": {
            "date": "2021-10-15 16:44:07.210631",
            "timezone_type": 3,
            "timezone": "America\/Argentina\/Buenos_Aires"
        },
        "accessToken": "...",
        "createdAt": {
            "date": "2021-10-14 16:44:07.210631",
            "timezone_type": 3,
            "timezone": "America\/Argentina\/Buenos_Aires"
        },
        "accountId": 10
    }
}
```

**Endpoint alternativo**

**GET** `/login`

*Header*

```
Authorization: Basic {base64-credentials}
```

Donde `{base64-credentials}` es la concatenación del nombre de usuario y la contraseña separados por el caracter dos puntos (`:`) y codificado en *Base64*.
