JSON Web Token, o JWT ("jot") para abreviar, es un estándar para pasar peticiones de forma segura en entornos de espacio restringido. Se ha introducido en todos los frameworks web principales. Simplicidad, compacidad y facilidad de uso son características clave de su arquitectura. Aunque todavía se utilizan sistemas mucho más complejos, los JWT tienen un amplio abanico de aplicaciones.

# ¿Qué es JWT?

Un token web JSON tiene el siguiente aspecto (se han insertado nuevas líneas para facilitar la lectura):

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9. eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9. TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ
```

Aunque parezca una disparate, en realidad es una representación imprimible y muy compacta de una serie de peticiones, junto con una firma para verificar su autenticidad.

```json
{
	"alg": "HS256",
	"typ": "JWT"
}
{
	"sub": "1234567890",
	"name": "John Doe",
	"admin": true
}
```

Las peticiones son definiciones o afirmaciones que se hacen sobre una determinada parte u objeto. Algunas de estas peticiones y su significado se definen como parte de la especificación JWT. Otras son definidas por el usuario. 
La magia detrás de JWT es que estandarizan ciertas peticiones que son útiles en el contexto de algunas operaciones comunes.
Por ejemplo, una de estas operaciones comunes es establecer la identidad de determinadas partes.