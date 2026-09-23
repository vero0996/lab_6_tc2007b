Verónica Paola Zapata Sánchez
A01199193

Ejercicio 0:
La contraseña. La contraseña nunca se guarda, lo que se guarda es el token. 
El token de acceso. Este si se guarda de manera cifrada. 
El token de refresco. Como es un token que se genera después de insertar la contraseña, se debe guardar para no estar pidiendo la contraseña a cada rato.
Usuario y rol. Si, esta no es información sensible ya que da información sobre el usuario y lo que puede hacer dentro de su sesión. 
El código de profesor. Esto no se guarda, nada más se usa para confirmar la diferencia de las vistas alumno - profesor.
La fecha xp. Si.

Ejercicio B3:
El token de acceso puede filtrarse fuera de DataStore a través del Logcat mediante interceptores de log HTTP (lo cual se evita usando redactHeader("Authorization") y no dejando logs detallados en release), las capturas de pantalla tomadas mientras se visualiza el token o su valor en pantalla (prevenido activando el flag FLAG_SECURE en la ventana), la URL si se llega a enviar por error como parámetro de consulta en peticiones GET (evitado pasándolo únicamente mediante el encabezado Authorization: Bearer), y el portapapeles si el usuario o la app copian el valor y otra aplicación maliciosa lo lee (prevenido no ofreciendo la opción de copiarlo o marcando el contenido pegado como sensible).

Ejercicio C2:
1. PublicarScreen llama al PublicarViewModel para enviar el aviso.
2. PublicarViewModel le pide al AvisosRepository que publique.
3. AvisosRepository llama a la API con Retrofit.
4. AuthInterceptor le pega el token de acceso a la petición HTTP.
5. El Servidor lee el token, ve que el rol es de alumno y regresa un error 403 Forbidden.
6. Retrofit recibe el 403 y lanza una excepción (HttpException).
7. PublicarViewModel atrapa esa excepción y guarda el error en su estado (uiState).
8. PublicarScreen lee el nuevo estado y muestra el mensaje en pantalla.

No. Cambiar datos locales en DataStore solo afecta a la app. El servidor decide los permisos leyendo la firma del token JWT; como esa firma no cambió, sigue rechazando la petición con un 403.
