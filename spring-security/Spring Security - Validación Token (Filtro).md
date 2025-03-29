La clase `BasicAuthenticationFilter` en **Spring Security** se encarga de manejar la autenticación basada en **HTTP Basic Authentication**.


📌 **¿Cuándo se usa?**  
✅ Si en la configuración de Spring Security usas `.httpBasic()`, Spring aplicará este filtro automáticamente.  
✅ Si necesitas procesar autenticaciones en cada petición (por ejemplo, en APIs protegidas).

## Método `doFilterInternal`

El método `doFilterInternal` se ejecuta en cada petición para procesar la autenticación. Es el **núcleo de los filtros en Spring Security**, ya que permite **interceptar y procesar cada petición HTTP** antes de que llegue al controlador.

✅ Podemos obtener el token y quitarle el prefijo "Bearer " 
	 `String token = header.replace(PREFIX_TOKEN, "");` 

✅ Podemos verificar un JWT  y obtener los claims del mismo
`Jwts.parser().verifyWith(SECRET_KEY).build().parseSignedClaims(token).getPayload()`

✅ Se puede obtener información como **username, roles y email** si están en el JWT.

###   Componentes clave
#### **`SecurityContextHolder`**, ¿Qué hace esta clase?

🔹 `SecurityContextHolder` es una clase central en **Spring Security** que **almacena el usuario autenticado** y sus permisos en un objeto `SecurityContext`.  
🔹 Este contexto **está disponible durante toda la petición HTTP**.

Ejemplo de uso
```Java
Authentication authentication = new UsernamePasswordAuthenticationToken("usuario", null, Collections.emptyList());

SecurityContextHolder.getContext().setAuthentication(authentication);
```

✔ Se crea un `UsernamePasswordAuthenticationToken`, que representa al usuario autenticado.  
✔ Se almacena en `SecurityContextHolder`, haciendo que el usuario quede autenticado **para la duración de la petición actual**.

#### `chain.doFilter()`, ¿Qué hace este método?

🔹 `chain.doFilter(request, response)` permite que la petición continúe su recorrido a través de los demás filtros en la cadena de Spring Security.  
🔹 Si omites esta línea, la petición **no avanzará** y se interrumpirá en el filtro actual.

Ejemplo

```Java
     protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain chain) throws IOException, ServletException {
   String header = request.getHeader(HEADER_AUTHORIZATION); 
        if(header == null || !header.startsWith(PREFIX_TOKEN)){
            chain.doFilter(request, response);
            return;
        }
        String token = header.replace(PREFIX_TOKEN, "");
        try {
            Claims claims = Jwts.parser().verifyWith(SECRET_KEY).build().parseSignedClaims(token).getPayload();
            String username = claims.getSubject();
            
            UsernamePasswordAuthenticationToken authToken = new UsernamePasswordAuthenticationToken(username, null, Collections.emptyList());

            SecurityContextHolder.getContext().setAuthentication(authToken);
            chain.doFilter(request, response);


        } catch (JwtException e) {

            Map<String, String> body = new HashMap<>();
            body.put("error", e.getMessage());
            body.put("message", "El token JWT no es válido");
  
            response.getWriter().write(new ObjectMapper().writeValueAsString(body));

            response.setStatus(HttpStatus.UNAUTHORIZED.value());
            response.setContentType(CONTENT_TYPE);

        }}
```