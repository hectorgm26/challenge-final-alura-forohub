# Foro Hub

## Descripción del Proyecto

Foro Hub es una aplicación de foro en línea que permite a los usuarios registrar, ver, actualizar y eliminar tópicos. El sistema permite gestionar los tópicos en función de diferentes cursos, con funcionalidades que incluyen la autenticación de usuarios y la protección de la información sensible.

Este proyecto es parte del **challange final de programación** dentro de la formación de **Spring Boot** del programa **Oracle One** de **Alura LATAM**. Durante este proyecto, he implementado una API REST con las siguientes características y objetivos:

- **Gestión de Tópicos**: Crear, listar, actualizar y eliminar tópicos.
- **Autenticación y autorización**: Seguridad con Spring Security y JWT.
- **Persistencia en base de datos**: Con MySQL para almacenar los datos de usuarios, tópicos y cursos.
- **Migraciones de base de datos**: Uso de Flyway para la gestión de esquemas.

## Funcionalidades

### 1. **Registrar Tópicos**
   - **Método**: `POST /topicos`
   - **Descripción**: Permite registrar un nuevo tópico con un título, mensaje, autor y curso.
   - **Respuesta**: El tópico creado, incluyendo el correo electrónico del autor y el nombre del curso.
   - **Validaciones**: Verificación de que los campos no estén vacíos y que el usuario autor exista.

### 2. **Listar Tópicos**
   - **Método**: `GET /topicos`
   - **Descripción**: Devuelve todos los tópicos registrados en el sistema.
   - **Respuesta**: Lista de tópicos con título, mensaje, fecha de creación, autor (correo) y curso.

### 3. **Obtener Detalles de un Tópico**
   - **Método**: `GET /topicos/{id}`
   - **Descripción**: Muestra los detalles de un tópico específico.
   - **Respuesta**: Detalles del tópico, incluyendo el título, mensaje, autor (correo), y curso.

### 4. **Actualizar Tópico**
   - **Método**: `PUT /topicos/{id}`
   - **Descripción**: Permite actualizar los detalles de un tópico específico.
   - **Respuesta**: El tópico actualizado.

### 5. **Eliminar Tópico**
   - **Método**: `DELETE /topicos/{id}`
   - **Descripción**: Elimina un tópico específico.
   - **Respuesta**: Código de estado `204 No Content` si la operación fue exitosa.

### 6. **Login y Autenticación**
   - **Método**: `POST /login`
   - **Descripción**: Permite iniciar sesión con credenciales de usuario (correo electrónico y contraseña).
   - **Respuesta**: Devuelve un token JWT que debe ser utilizado para autenticar las siguientes solicitudes.

## Requisitos

Para ejecutar este proyecto, necesitas tener instalados los siguientes programas:

- **JDK 17 o superior**: Para compilar y ejecutar el código Java.
- **MySQL**: Base de datos utilizada para almacenar la información.
- **Maven**: Herramienta para la gestión de dependencias y construcción del proyecto.
- **Postman/Insomnia**: Para probar los endpoints de la API.

## Configuración

1. **Base de datos**: Asegúrate de tener MySQL instalado y ejecutándose. Luego, configura la conexión en el archivo `application.properties`:

   ```properties
   spring.datasource.url=jdbc:mysql://localhost:3306/forohub
   spring.datasource.username=root
   spring.datasource.password=tu-contraseña
   ```

2. **Migraciones**: Usa Flyway para crear las tablas necesarias en la base de datos:

   - Los scripts de migración están disponibles en el proyecto.

3. **Autenticación**: Para probar la autenticación y generación del token JWT, debes hacer un `POST` al endpoint `/login` con un cuerpo JSON:

   ```json
   {
       "correoElectronico": "usuario@ejemplo.com",
       "contrasena": "tu-contraseña"
   }
   ```

   La respuesta será un token JWT que podrás usar para autenticarte en los siguientes endpoints.

## Casos de prueba con Insomnia

### 1. **Crear Tópico (POST /topicos)**
   - Método: `POST`
   - URL: `http://localhost:8080/topicos`
   - Body (JSON):
     ```json
     {
       "titulo": "Nuevo Tópico",
       "mensaje": "Este es un mensaje sobre un nuevo tópico.",
       "autor": "usuario@ejemplo.com", 
       "curso": "Curso de Java"
     }
     ```

### 2. **Obtener Tópicos (GET /topicos)**
   - Método: `GET`
   - URL: `http://localhost:8080/topicos`

### 3. **Obtener Detalles de un Tópico (GET /topicos/{id})**
   - Método: `GET`
   - URL: `http://localhost:8080/topicos/{id}` (Reemplaza `{id}` por el ID del tópico)

### 4. **Actualizar Tópico (PUT /topicos/{id})**
   - Método: `PUT`
   - URL: `http://localhost:8080/topicos/{id}` (Reemplaza `{id}` por el ID del tópico)
   - Body (JSON):
     ```json
     {
       "titulo": "Tópico Actualizado",
       "mensaje": "Este es un mensaje actualizado sobre el tópico.",
       "autor": "usuario@ejemplo.com", 
       "curso": "Curso de Java"
     }
     ```

### 5. **Eliminar Tópico (DELETE /topicos/{id})**
   - Método: `DELETE`
   - URL: `http://localhost:8080/topicos/{id}` (Reemplaza `{id}` por el ID del tópico)

### 6. **Login (POST /login)**
   - Método: `POST`
   - URL: `http://localhost:8080/login`
   - Body (JSON):
     ```json
     {
       "correoElectronico": "usuario@ejemplo.com",
       "contrasena": "tu-contraseña"
     }
     ```

   - Respuesta: Devuelve un JWT para autenticación.

## Consideraciones de Seguridad

- Todos los endpoints de **modificación de datos** (POST, PUT, DELETE) están protegidos por autenticación JWT.
- Asegúrate de incluir el token en el encabezado `Authorization` de las solicitudes.

## Contribuciones

Este proyecto es parte de la formación de Spring Boot de Alura LATAM y está diseñado para aplicar lo aprendido en la creación de una API REST segura y funcional.

Si deseas contribuir o hacer mejoras, siéntete libre de hacer un fork y enviar un pull request.

## Licencia

Este proyecto está bajo la Licencia MIT. Puedes usarlo, modificarlo y distribuirlo con fines comerciales o no comerciales.

