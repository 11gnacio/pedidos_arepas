# 🫓 Pedidos de Arepas — Flask + MySQL + MVC + Validación

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-3.0%2B-000000?logo=flask&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-8.0%2B-4479A1?logo=mysql&logoColor=white)
![Bootstrap](https://img.shields.io/badge/Bootstrap-5.3-7952B3?logo=bootstrap&logoColor=white)

Aplicación web desarrollada con **Flask** y **MySQL** siguiendo la arquitectura **MVC (Modelo-Vista-Controlador)**. La aplicación gestiona y valida pedidos de arepas en tiempo real, aplicando reglas de negocio estrictas en el backend antes de guardar en la base de datos.

---

##  Función de la Aplicación

La aplicación permite administrar el ciclo de vida completo del registro de pedidos de arepas mediante un flujo seguro de lectura y creación:

1. **Listado de Pedidos (`/pedidos`):** Muestra todos los pedidos registrados recuperados desde MySQL en una tabla interactiva.
2. **Formulario de Registro (`/pedidos/nuevo`):** Permite ingresar el nombre del cliente, tipo de arepa y la cantidad deseada.
3. **Validación Backend (`/pedidos/crear`):** Antes de interactuar con la base de datos, el servidor evalúa los datos recibidos mediante las siguientes reglas:
   - **Campos obligatorios:** Todos los campos deben estar completos.
   - **Longitud del nombre:** Debe tener al menos 2 caracteres.
   - **Cantidad válida:** Debe ser un valor entero estrictamente mayor a 0.
4. **Retroalimentación Dinámica:**
   - Si la información es **inválida**, se generan mensajes de alerta con `flash()` y se redirige al usuario al formulario sin alterar la base de datos.
   - Si la información es **válida**, se realiza el `INSERT` en MySQL y se redirige a la vista principal con una confirmación de éxito.

---

##  Descripción Detallada de Carpetas y Archivos

```text
pedidos_arepas/
│
├── flask_app/                        # Paquete principal de la aplicación Flask
│   ├── __init__.py                   # Inicializa la app Flask y configura la secret_key desde el .env
│   │
│   ├── bd/                           # Contenedor de scripts SQL
│   │   └── esquema_arepas.sql        # Script DDL/DML para crear la base de datos y datos de prueba
│   │
│   ├── config/                       # Módulo de configuración e infraestructura
│   │   └── mysqlconnection.py        # Conector a MySQL mediante PyMySQL con soporte para variables de entorno
│   │
│   ├── controllers/                  # Capa Controlador (Manejo de rutas y solicitudes HTTP)
│   │   └── pedidos.py                 # Define las rutas GET/POST, recibe datos del formulario y gestiona el flujo
│   │
│   ├── models/                       # Capa Modelo (Lógica de negocio y consultas SQL)
│   │   └── pedido.py                  # Clase Pedido, métodos de consulta (get_all, save) y @staticmethod de validación
│   │
│   ├── static/                       # Archivos estáticos
│   │   └── css/
│   │       └── style.css             # Hojas de estilo personalizadas para la interfaz
│   │
│   └── templates/                    # Capa Vista (Plantillas HTML renderizadas con Jinja2)
│       ├── nuevo_pedido.html         # Formulario de registro con captura de errores flash
│       └── pedidos.html              # Vista principal para listar la tabla de pedidos
│
├── resources/                        # Diagramas y recursos de diseño
│   └── esquema_arepas_erd.mwb        # Archivo de modelo Entidad-Relación de MySQL Workbench
│
├── .env                              # Archivo local de variables de entorno (claves secretas y credenciales)
├── .gitignore                        # Define los archivos y carpetas que Git debe ignorar (p. ej., .env, __pycache__)
├── Pipfile                           # Lista de dependencias del proyecto para Pipenv
├── Pipfile.lock                      # Registro exacto con hashes de las versiones de dependencias instaladas
├── README.md                         # Documentación general del proyecto
└── server.py                         # Punto de entrada principal para arrancar el servidor de desarrollo