layout: true

---
class: middle, center, general
# JWT y Node.js
## Tokeniza tus web apps
Una pequeña charla por [Carlos González](http://caal-15.github.io)

Síguela en [caal-15.github.io/jwt-node-talk](http://caal-15.github.io/jwt-node-talk)
.footnote[.alt-link[[Sitio JWT](https://jwt.io/)]]

---
class: left, middle

# ¿Qué Son?

.big[JSON Web Tokens, son un estándar abierto que define una forma _compacta_ y
_segura_ de transmitir información entre distintos interesados como objetos
JSON.]
.footnote[.alt-link[[El estándar](https://tools.ietf.org/html/rfc7519)]]

---
class: center, middle

# ¿Para qué Sirven?

.big[
* Autenticación
* Intercambio de Información
]

---
class: left middle

# Ventajas

.big[
* __Seguros:__  Los datos siempre viajan con una firma (con un secreto
  usando _HMAC_, o con llave pública y privada usando _RSA_).

* __Compactos:__ Los JWT son lo suficientemente pequeños para viajar en una
  _URL_, en una _cabecera HTTP_, o como un _campo de un POST_.

* __Autocontenidos:__ Los JWT cargan toda la información necesaria para
  identificar al usuario, además son _Sessionless!_.
]

---
class: center, middle

# Composición

---
class: left, middle

# Cabecera (header)

.big[Contiene el tipo del token y algoritmo usado para la firma, se codifica
usando _Base64Url_.]

```javascript
const meta = {
  "alg": "HS256",
  "typ": "JWT"
}
const header = myCoolEnc.base64Url(meta)
```

---
class: left, middle

# Cuerpo (payload)

.big[Contiene la información _deseada_ del usuario, se codifica también usando
_Base64Url_.]

```javascript
const data = {
  "_id": "507f191e810c19729de860ea",
  "email": "caal@caal.caal",
  "admin": true
}
const payload = myCoolEnc.base64Url(data)
```
---
class: left, middle

# Firma (signature)

.big[Contiene una firma generada a partir de un algoritmo de encripción (_RSA_,
_HMAC_), y la cabecera y el cuerpo _codificados_.]

```javascript
const signature = myCoolCrypt.HMACSHA256(
  header + '.' + payload,
  secret
)
```

---
class: left, middle

# Poniéndolo todo Junto

.big[Simplemente juntamos la _cabecera_, el _cuerpo_ y la _firma_ separándolos
por puntos:]

```javascript
const token = (
  header + '.' + payload + '.' + signature
)
```

---
class: center, middle

# Implementando en Node.js

## ¿Qué vamos a usar?

.big[
* Framework con soporte para middleware ([restify](http://restify.com/), [express](http://expressjs.com/), etc.).
* Librería para firma y verificación de JWT: [jsonwebtoken](https://github.com/auth0/node-jsonwebtoken).
* Middleware de manejo de seguridad: [passport.js](http://passportjs.org/).
* Estrategia para passport: [passport-jwt](https://github.com/themikenicholson/passport-jwt).
* Base de Datos: [MongoDB](https://www.mongodb.com/).
* ODM: [mongoose](http://mongoosejs.com/).
]

.footnote[.alt-link[[Repositorio](https://github.com/caal-15/jwt-fiddle)]]

---
class: center, middle

# Gracias por su atención!
