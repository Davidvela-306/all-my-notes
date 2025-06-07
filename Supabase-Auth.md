Primero debemos conocer los conceptos detallados en [[Autenticación y Autorización]]

#### Arq supabase

- **Capa cliente**, puede ser un SDK de supabase o un cliente REST que permita solicitudes HTTP
- Utiliza API de kong como puerta de enlace que conecta a los servicios supabase
- Go true, desarrollado por Netlify y Bifurcado por supabase para admitir servicio autenticación, valida, emite, acutaliza  [[Json Web Token (JWT)]] y comunicación servicios OAuth (google, facebook, etc)
- PostgresSQL como db. Datos de autenticación se guardan en la db pero este equema no se expone al generar automáticamente la API por temas de seguridad.
- Es posible usar auth con objetos propios usando triggers y claves foraneas, si se hace eso asegurarse cumplir con medidas seguridad (RLS o revoking grants).

#### USO DE JWT
Supabase hace uso de [[Json Web Token (JWT)]] como normalmente se especifica.

En Supabase se emite JWT para tres propósitos diferentes
### 🔑 **1. `anon key` (clave anónima)**

- **Qué es:** Una clave pública que permite a los usuarios **acceder al proyecto sin autenticarse**.
    
- **Uso:** Se usa **en el frontend** para que usuarios no logueados puedan interactuar con Supabase (por ejemplo: leer una tabla pública).
    
- **Por qué:** Esta clave **omite la API Gateway** y se conecta directamente al backend de Supabase, pero **con acceso muy limitado**.
    

> 🧠 **Piensa en ella como una llave pública con acceso restringido.**

---

### 🔐 **2. `service_role key` (clave de rol de servicio)**

- **Qué es:** Una clave **privada** con **todos los permisos posibles**.
    
- **Uso:** Solo se debe usar **en el backend** (por ejemplo, funciones de servidor o cron jobs).
    
- **Por qué:** Puede **ignorar la seguridad de nivel de fila (RLS)**, lo que significa que puede leer o escribir cualquier cosa en cualquier tabla.
    

> ⚠️ **NUNCA** la pongas en el frontend. Si alguien la obtiene, puede manipular toda tu base de datos.

---

### 👤 **3. `user specific JWTs` (tokens de usuario)**

- **Qué son:** JWTs **generados automáticamente por Supabase** cuando un usuario inicia sesión (email, Google, etc.).
    
- **Uso:** El usuario los usa para **acceder a datos protegidos** según su rol, permisos o reglas de RLS.
    
- **Por qué:** Representan **la sesión del usuario**, como lo hacían los _session cookies_ antes.
    

> 🧠 Piensa en esto como **el carnet de identidad del usuario logueado**: lo identifica y define qué puede o no puede hacer.