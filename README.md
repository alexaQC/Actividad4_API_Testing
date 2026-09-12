# Actividad4_API_Testing
Pruebas de API, Newman, JMeter y CI/CD - Actividad 4


## Seguridad y principios DevSecOps aplicados

### 1. Pruebas automatizadas en CI/CD y calidad

Las pruebas automatizadas ayudan a mejorar la calidad porque permiten comprobar de manera constante que la API sigue funcionando correctamente después de realizar cambios. Se creó una colección de Postman con pruebas para los métodos GET, POST, PUT y DELETE, además de validaciones de status code, body y headers, posteriormente la colección se ejecutó con Newman y se integró en un pipeline de GitHub Actions. El pipeline ejecutó 6 peticiones y 30 validaciones sin errores, permitiendo detectar automáticamente si alguna funcionalidad deja de responder como se espera.

### 2. Autenticación con tokens y seguridad de APIs

La autenticación mediante tokens permite controlar el acceso a recursos que no deberían estar disponibles para cualquier usuario. Se realizó un login mediante una petición POST que generó un access token, Este token se guardó automáticamente en una variable de entorno de Postman y después se utilizó como Bearer Token en una petición GET autenticada, De esta forma no fue necesario escribir manualmente el token en cada solicitud y se comprobó que el endpoint protegido solamente pudiera consultarse utilizando una credencial válida.

### 3. Riesgos detectados mediante pruebas automatizadas

Las pruebas automatizadas pueden detectar problemas como códigos de respuesta incorrectos, respuestas que no contienen las propiedades esperadas, headers faltantes, errores en operaciones CRUD, fallas de autenticación y tokens inválidos o vencidos. Durante las pruebas realizadas se validaron automáticamente los status code, las propiedades del body y el header Content-Type. También se comprobó el funcionamiento del login y de una petición autenticada, además con JMeter se realizó una prueba de carga de 20 usuarios sobre el endpoint GET de MockAPI, obteniendo 20 muestras y 0.00% de errores.

### 4. Integración de DevSecOps en el pipeline

La filosofía DevSecOps busca integrar calidad y seguridad durante el proceso de desarrollo y no solamente al final. Aquí se aplicó al incluir las pruebas de API dentro de GitHub Actions. Cada vez que se ejecuta el pipeline, GitHub descarga el repositorio, configura Node.js, instala Newman y ejecuta automáticamente la colección de Postman, esto permite verificar las funciones principales de la API, sus validaciones y la autenticación dentro del mismo proceso de CI/CD. Si alguna prueba falla, el pipeline también falla, permitiendo detectar el problema antes de considerar correcta una nueva versión del proyecto.
