
Desglosado:
1. JSON: javaScript Object Notation, un formato de intercambio de datos entendible para multiples lenguajes de programación y humanos.
2. Web:   sistema interconectado de páginas web públicas accesibles a través de Internet
3. Token: referencia (un identificador) que regresa a los datos sensibles a través de un sistema de tokenización
Ahora entendiendo de forma desglosada podemos decir que JWT es un estandar abierto, que representa un objeto tokenizado de forma compacta y autónoma(debe ser corto, y puede usarse en la web, apps, etc).
#### ESTRUCTURA:
xxxx.yyyy.zzzz
1. Encabezado(xxxx): contiene información como tipo de token y algoritmo de firma 
2. Carga útil(yyyy): reclamaciones, que son datos que incluimos, pueden ser registradas, públicas y privadas
![[Pasted image 20250606095928.png]]
3. Firma(zzzz): Se genera con el algoritmo de encriptación del encabezado definido en el encabezado, hace uso del encabezado + carga útil y el secreto(conjunto de caracteres privados), retorna el la 3ra parte del token que asegura la legitimidad del token.

* El token firmado implica la integridad de afirmaciónes encapsuladas.
* El token cifrado implica ocultar estas afirmaciones y tener que pasar un proceso de decifrado para leer contenido.
* El token firmado por clave pública/privada garantiza que cav.priv firmó token
* En la carga útil, las reclamaciones privadas no debn tener muchos datos o datos confidenciales
#### Cuándo uso:
El caso más común, cuando desea acceder a un recurso protegido, se enviará el JWT en el encabezado de autorización, si es válido accederá. Esto se hace en cada solicitud o consulta.

Al intercambiár info es seguro dado que usa claves pública(privada, asegurando que el remitente sea quien dice ser y no haa alteración en la carga útil

#### Validar y Verificar JWT

**Validar:** Token con sentido semántico, estructurado y sin expirar
**Verificar:** Token de fuente confiable, sin modificación

#### Codificación y Decodificación

**Codificar:** Pasar de json a base64 tanto el header como la carga útil. Con el secreto y el algoritmo elegido la firma puede pasar a base64
**Decodificar: ** Pasar de base64 a Json,  anque pueda ver la carga útil, no podré validar la info sin la firma que necesita tanto del algoritmo como del secreto. Por ende no será validado en caso de uso.

Nota: Una desventaja de los JWT es que no son fácilmente anulables, a diferencia de los tokens de sesión. Si un JWT se filtra a un actor malicioso, este podrá canjearlo en cualquier lugar hasta que se cumpla la fecha de vencimiento, a menos que el propietario del sistema lo actualice `jwt_secret`(lo que, por supuesto, invalidará los tokens existentes _de todos )._

#### CONEXIONES
[[Autenticación y Autorización]]
[[Infraestructura]]

#### REFERENCIAS

>https://www.oracle.com/ar/database/what-is-json/
>https://developer.mozilla.org/es/docs/Glossary/World_Wide_Web
>https://es.wikipedia.org/wiki/Token_(inform%C3%A1tica)
>https://www.youtube.com/watch?v=bVgmy5osPsY
>https://jwt.io/introduction
>https://datatracker.ietf.org/doc/html/rfc7519#section-4.1
>https://supabase.com/docs/guides/auth/jwts 