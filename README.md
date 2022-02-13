
# Configuración y despliegue de servidores

## Implementaciones realizadas en la práctica
 - Desplegada en el servidor la práctica de Backend Avanzado
    http://ec2-100-26-58-79.compute-1.amazonaws.com/

 - Protegida la conexión a la BD de mongo con usuario:contraseña

 - Para las peticiones a la API necesario token generado en:
    http://ec2-100-26-58-79.compute-1.amazonaws.com/apiv1/authenticate
    email: user@example.com, password: 1234

 - Las peticiones a la API por nginx en (necesario header Authorization: token):
    http://ec2-100-26-58-79.compute-1.amazonaws.com/apiv1/anuncios  

 - Campos necesarios para añadir anuncios: nombre, venta, precio, imagen, tags
 - Sirven ficheros estaticos por nginx 
 - aplicacion node y el servicio de este implementados con supervisor

 - Desplegada práctica de react en http://100.26.58.79/



### GET /anuncios

**Input Query**:

start: {int} skip records
limit: {int} limit to records
sort: {string} field name to sort by
includeTotal: {bool} whether to include the count of total records without filters
tag: {string} tag name to filter
venta: {bool} filter by venta or not
precio: {range} filter by price range, examples 10-90, -90, 10-
nombre: {string} filter names beginning with the string

Input query example: ?start=0&limit=2&sort=precio&includeTotal=true&tag=mobile&venta=true&precio=-90&nombre=bi

**Result:** 

    {
      "ok": true,
      "result": {
        "rows": [
          {
            "_id": "55fd9abda8cd1d9a240c8230",
            "nombre": "iPhone 3GS",
            "venta": false,
            "precio": 50,
            "foto": "/images/anuncios/iphone.png",
            "__v": 0,
            "tags": [
              "lifestyle",
              "mobile"
            ]
          }
        ],
        "total": 1
      }
    }


### GET /anuncios/tags

Return the list of available tags for the resource anuncios.

**Result:** 

    {
      "ok": true,
      "allowed_tags": [
        "work",
        "lifestyle",
        "motor",
        "mobile"
      ]
    }
