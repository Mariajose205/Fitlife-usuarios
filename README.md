# Fitlife MS-usuarios

Microservicio de gestión de usuarios para FitLife. Este servicio maneja la autenticación, registro y gestión de usuarios con diferentes roles (ADMIN, TRAINER, USER).

## Características

- **Factory Method Pattern**: Implementación del patrón Factory Method para crear usuarios según su rol
- **BCrypt Encryption**: Encriptación de contraseñas usando BCrypt
- **Role-based Access Control**: Soporte para roles de ADMIN, TRAINER y USER
- **REST API**: Endpoints completos para gestión de usuarios
- **Unit Testing**: Pruebas unitarias con JUnit y Mockito

## Tecnologías

- Java 17
- Spring Boot 3.2.0
- Spring Data JPA
- MySQL 8.0
- BCrypt para encriptación
- Maven
- Docker

## Endpoints

### Autenticación
- `POST /usuarios/login` - Login de usuario
- `POST /usuarios/register` - Registro de nuevo usuario

### Gestión de Usuarios
- `GET /usuarios` - Obtener todos los usuarios
- `GET /usuarios/{id}` - Obtener usuario por ID
- `GET /usuarios/email/{email}` - Obtener usuario por email
- `DELETE /usuarios/{id}` - Eliminar usuario

### Estadísticas
- `GET /usuarios/estadisticas/total` - Contar total de usuarios
- `GET /usuarios/estadisticas/rol/{rol}/count` - Contar usuarios por rol
- `GET /usuarios/estadisticas/activos/count` - Contar usuarios activos
- `GET /usuarios/estadisticas/inactivos/count` - Contar usuarios inactivos

## Configuración

### Variables de Entorno

```env
SPRING_DATASOURCE_URL=jdbc:mysql://mysql-usuarios:3306/fitlife_usuarios_db
SPRING_DATASOURCE_USERNAME=root
SPRING_DATASOURCE_PASSWORD=root
SPRING_JPA_HIBERNATE_DDL_AUTO=update
```

## Desarrollo

### Compilar el proyecto
```bash
mvn clean package
```

### Ejecutar pruebas
```bash
mvn test
```

### Ejecutar localmente
```bash
mvn spring-boot:run
```

## Docker

### Construir imagen
```bash
docker build -t fitlife-usuarios:latest .
```

### Ejecutar contenedor
```bash
docker run -p 8085:8085 \
  -e SPRING_DATASOURCE_URL=jdbc:mysql://host.docker.internal:3306/fitlife_usuarios_db \
  -e SPRING_DATASOURCE_USERNAME=root \
  -e SPRING_DATASOURCE_PASSWORD=root \
  fitlife-usuarios:latest
```

## Factory Method

El servicio utiliza el patrón Factory Method para crear usuarios según su rol:

```java
// Crear administrador
Usuario admin = UsuarioFactory.crearAdministrador("Juan", "admin@fitlife.cl", "password");

// Crear entrenador
Usuario trainer = UsuarioFactory.crearEntrenador("Maria", "trainer@fitlife.cl", "password");

// Crear usuario normal
Usuario user = UsuarioFactory.crearUsuarioNormal("Pedro", "user@gmail.com", "password");

// Detección automática por email
Usuario autoUser = UsuarioFactory.crearUsuarioAutoDetect("Ana", "admin@fitlife.cl", "password");
```

## GitHub Actions

Este repositorio utiliza GitHub Actions para CI/CD:

- **Build**: Compila el proyecto con Maven
- **Test**: Ejecuta pruebas unitarias
- **Docker Build**: Construye la imagen Docker
- **Docker Push**: Sube la imagen a Docker Hub

## Contribución

1. Fork el repositorio
2. Crea una rama para tu feature (`git checkout -b feature/nueva-funcionalidad`)
3. Commit tus cambios (`git commit -m 'Agrega nueva funcionalidad'`)
4. Push a la rama (`git push origin feature/nueva-funcionalidad`)
5. Abre un Pull Request

## Licencia

Este proyecto es parte de FitLife Gym Management System.
