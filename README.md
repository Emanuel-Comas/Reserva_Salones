# App de Reservas – API REST.

Aplicación backend para la gestión de reservas, turnos, usuarios, servicios y salones, desarrollada en Node.js + Express, con autenticación JWT, base de datos MySQL, generación de reportes y documentación Swagger.


## Archivos principales.

    reservas.js

    Archivo donde se configura toda la aplicación Express.

    -- Qué hace:

        Crea la app con Express

        Habilita JSON (express.json())

        Configura Passport (login y JWT)

        Configura logs con Morgan (consola y access.log)

        Registra Swagger

        -- Monta las rutas de la API (/api/v1/*):

            salones

            servicios

            reservas

            auth

            reportes

            usuarios

            turnos

            logs (admin)

            notificaciones

    En resumen:

        reservas.js arma la aplicación completa; servidor.js solo la levanta.



    servidor.js

        Archivo mínimo de arranque de la aplicación.

        -- Responsabilidades:

            Carga variables de entorno con dotenv

            Importa la aplicación Express ya configurada desde reservas.js

            Inicia el servidor HTTP escuchando en el puerto definido por entorno

            Muestra mensajes informativos en consola (estado y Swagger)

        -- No contiene:

            lógica de negocio

            middlewares

            definición de rutas

            configuración de Express

    En resumen:

        Solo arranca el servidor. Toda la configuración real vive en reservas.js.



## Características principales.

-- API REST versionada (/v1)

-- Autenticación y autorización con JWT + Passport

-- Gestión de:

    Usuarios

    Reservas

    Turnos

    Servicios

    Salones

-- Roles de usuario:

    1 - Admin
    2 - Empleado
    3 - Cliente


-- Generación de reportes (PDF / CSV)

-- Envío de correos con Nodemailer

-- Templates con Handlebars

-- Cacheo de respuestas con Apicache

-- Logs de acceso con Morgan

-- Documentación automática con Swagger

-- Arquitectura por capas (controladores, db, middlewares, servicios, rutas)


## Tecnologías usadas.

    Node.js

    Express 5 –> Framework backend

    MySQL –> Base de datos relacional

    mysql2 –> Driver de conexión a MySQL

    Passport:

        passport-local –> Autenticación por usuario/contraseña

        passport-jwt –> Autenticación mediante JWT

    jsonwebtoken –> Generación y validación de tokens

    express-validator –> Validación de datos

    cors –> Manejo de CORS

    dotenv –> Variables de entorno

    Morgan –> Logging HTTP

    Apicache –> Cacheo de respuestas

    Swagger:

        -- La documentación se genera automáticamente a partir de la configuración y anotaciones del proyecto.

        swagger-jsdoc -> Genera la especificación Swagger a partir del código.

        swagger-ui-express -> Expone la documentación en una interfaz web (/api-docs).

    Nodemailer –> Envío de correos

    Handlebars –> Templates HTML

    Puppeteer –> Generación de reportes PDF

    csv-writer –> Exportación de reportes CSV


## Instalación.

    -- Clonar el repositorio:

        git clone <url-del-repo>
        cd Reserva_Salones

    -- Requisitos previos.

        - Node.js (v18 o superior)
        - MySQL en ejecución, en este caso se uso Xampp.

    -- Instalar dependencias:

        npm install

    -- Variables de entorno:

        Crear un archivo .env en la raíz del proyecto:

            PORT=3000

            DB_HOST=localhost
            DB_USER=usuario
            DB_PASSWORD=password
            DB_NAME=reservas_db

            JWT_SECRET=clave_secreta

            EMAIL_HOST=smtp.example.com
            EMAIL_PORT=587
            EMAIL_USER=correo@example.com
            EMAIL_PASS=password


## Ejecución.

    -- Modo desarrollo:

        npm run des

    -- El servidor se levanta por defecto en::

        http://localhost:3000

## Documentación API (Swagger).

    -- Una vez iniciado el servidor, acceder a:

        http://localhost:3000/api-docs


    -- Incluye:

        Endpoints

        Métodos

        Validaciones

        Autenticación JWT


## Autenticación.

    Login mediante Passport Local

    Autorización mediante JWT

    El token debe enviarse en el header:

        Authorization: Bearer <token>

    -- Algunas rutas requieren rol admin.


## Arquitectura/Estructura.

    -- El proyecto sigue una estructura por capas:

        Rutas: definición de endpoints

        Controladores: validación y control de flujo

        Servicios: lógica de negocio

        DB: acceso a base de datos

        Middlewares: auth, validaciones, errores

        Utiles: helpers, templates, reportes

    -- Esto facilita:

        Escalabilidad

        Testeo

        Mantenimiento


    -- Estructura del proyecto:

        ```
        └── 📁Reserva_Salones
            └── 📁src
                └── 📁config
                    ├── passport.js
                    ├── swagger.js
                └── 📁controladores
                    ├── authControlador.js
                    ├── informeControlador.js
                    ├── logController.js
                    ├── notificacionControlador.js
                    ├── reservasControlador.js
                    ├── salonesControlador.js
                    ├── serviciosControlador.js
                    ├── turnosControlador.js
                    ├── usuariosControlador.js
                └── 📁db
                    ├── conexion.js
                    ├── reservas.js
                    ├── reservaServicios.js
                    ├── salones.js
                    ├── servicios.js
                    ├── turnos.js
                    ├── usuarios.js
                └── 📁middlewares
                    ├── apicache.js
                    ├── autorizarUsuario.js
                    ├── validarCampos.js
                └── 📁servicios
                    ├── informesServicio.js
                    ├── notificacionServicio.js
                    ├── reservasServicios.js
                    ├── salonesServicio.js
                    ├── serviciosServicio.js
                    ├── turnosServicio.js
                    ├── usuarioServicio.js
                └── 📁utiles
                    └── 📁handlebars
                        ├── informe.hbs
                        ├── plantilla.hbs
                └── 📁v1
                    └── 📁rutas
                        ├── adminRouters.js
                        ├── authRutas.js
                        ├── notificacionRuta.js
                        ├── reporteRoutes.js
                        ├── reservasRutas.js
                        ├── salonesRutas.js
                        ├── serviciosRutas.js
                        ├── turnosRoutes.js
                        ├── usuariosRutas.js
                ├── reservas.js
                ├── servidor.js
            ├── .env
            ├── .gitignore
            ├── access.log
            ├── package-lock.json
            ├── package.json
            ├── README.md
            └── requirements.txt
        ```

    
## Reportes.

    Generación de reportes en PDF usando Puppeteer

    Templates HTML con Handlebars

    Exportación a CSV

-- Ideal para informes administrativos.


## Emails.

    Envío de notificaciones por correo

    Configurable vía .env

    Útil para confirmaciones de reservas y avisos


## Logs y monitoreo.

    Registro de accesos en 'access.log', que se creara solo si no esta en el proyecto raiz.

    Logging HTTP con Morgan


## Notas.

    -- Asegurate de tener MySQL corriendo antes de iniciar la app.
    -- En este caso use 'Xampp'.


## Autor.

    Emanuel Comas
    -- Proyecto backend - Aplicación de Reservas.


## Licencia.

    ISC