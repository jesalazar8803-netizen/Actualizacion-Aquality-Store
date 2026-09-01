# 🛒 Aquality Store

Sistema de comercio electrónico desarrollado como **proyecto personal de portafolio**, orientado a demostrar conocimientos en desarrollo backend, APIs REST, persistencia de datos, seguridad, gestión de usuarios, procesamiento de pedidos e integración con servicios externos.

El proyecto nace a partir de la modernización conceptual de una aplicación web desarrollada originalmente en 2015 con tecnologías tradicionales como PHP, JavaScript, HTML, CSS y MySQL.

La nueva versión es completamente independiente y se desarrolla utilizando tecnologías modernas del ecosistema **Java / Spring Boot**, manteniendo las funcionalidades principales del sistema original y aplicando buenas prácticas actuales de arquitectura y desarrollo de software.

> **Nota:** Este proyecto es exclusivamente personal y académico/profesional. No representa el sitio web actual de AqualityPlast ni utiliza información privada de dicha empresa.

---

## 📋 Descripción

**Aquality Store** es una plataforma de comercio electrónico en la que los usuarios pueden consultar productos, registrarse, administrar un carrito de compras, realizar pedidos y efectuar pagos mediante diferentes métodos.

El sistema implementa dos perfiles principales:

* **Cliente**
* **Administrador**

Los visitantes pueden consultar los productos disponibles y utilizar el formulario de contacto, mientras que los usuarios autenticados tienen acceso al catálogo y a las funcionalidades relacionadas con compras.

El administrador dispone de herramientas para gestionar usuarios, productos, categorías, pedidos, pagos y mensajes recibidos mediante el formulario de contacto.

---

# 🎯 Objetivos del proyecto

* Modernizar conceptualmente una aplicación web legacy.
* Implementar una arquitectura basada en **Spring Boot y REST API**.
* Aplicar principios de **programación orientada a objetos**.
* Implementar persistencia utilizando **JPA/Hibernate**.
* Diseñar una base de datos relacional normalizada.
* Implementar autenticación y autorización.
* Aplicar buenas prácticas de seguridad.
* Implementar gestión de carrito y pedidos.
* Integrar diferentes métodos de pago.
* Generar documentos PDF relacionados con las compras.
* Implementar recuperación de contraseña mediante correo electrónico.
* Implementar pruebas automatizadas.
* Documentar el proyecto mediante UML.
* Aplicar control de versiones con Git.
* Preparar el proyecto para despliegue mediante Docker.

---

# 👥 Roles del sistema

## 👤 Visitante

Usuario que accede al sitio sin autenticarse.

Puede:

* Consultar productos.
* Consultar información de los productos.
* Consultar categorías.
* Utilizar el formulario de contacto.
* Registrarse.
* Iniciar sesión.

El visitante no puede realizar compras.

---

## 🛍️ Cliente

Usuario registrado y autenticado.

Puede:

* Iniciar sesión.
* Consultar el catálogo.
* Consultar productos.
* Consultar detalles de productos.
* Agregar productos al carrito.
* Modificar cantidades.
* Eliminar productos del carrito.
* Consultar el carrito.
* Crear pedidos.
* Seleccionar método de pago.
* Consultar sus pedidos.
* Consultar el detalle de sus pedidos.
* Consultar el estado de sus pedidos.
* Generar comprobantes PDF.
* Solicitar recuperación de contraseña.
* Contactar con la administración.

---

## 🔐 Administrador

Usuario con permisos administrativos.

Puede:

* Gestionar productos.
* Crear productos.
* Actualizar productos.
* Desactivar productos.
* Eliminar productos según las reglas del sistema.
* Gestionar categorías.
* Gestionar clientes.
* Consultar pedidos.
* Actualizar estados de pedidos.
* Consultar pagos.
* Gestionar mensajes de contacto.
* Generar comprobantes PDF.
* Generar reportes.
* Administrar la información general del sistema.

---

# ⚙️ Funcionalidades principales

## 🔑 Autenticación y usuarios

* Registro de clientes.
* Inicio de sesión.
* Cierre de sesión.
* Autenticación mediante JWT.
* Control de acceso basado en roles.
* Roles `CUSTOMER` y `ADMIN`.
* Hash seguro de contraseñas.
* Recuperación de contraseña mediante correo electrónico.
* Tokens de recuperación con fecha de expiración.
* Activación/desactivación de usuarios.

---

## 📦 Catálogo de productos

Los productos pertenecen a categorías y contienen información como:

* Nombre.
* Descripción.
* Precio.
* Stock.
* Imagen.
* Estado.
* Fecha de creación.
* Fecha de actualización.

Los visitantes podrán consultar la sección:

```text
Productos
```

mientras que los clientes autenticados accederán a:

```text
Catálogo
```

Ambas secciones utilizan la misma información de productos, pero presentan diferentes experiencias dependiendo del estado de autenticación.

---

## 🛒 Carrito de compras

Cada cliente puede disponer de un carrito asociado a su cuenta.

Funcionalidades:

* Agregar productos.
* Modificar cantidades.
* Eliminar productos.
* Consultar productos agregados.
* Calcular subtotales.
* Validar stock.
* Mantener el precio correspondiente al producto dentro del carrito.

Modelo:

```text
User
  │
  │ 1
  ▼
Cart
  │
  │ 1
  ▼
CartItem
  │
  │ N
  ▼
Product
```

---

# 🧾 Pedidos

Cuando el cliente confirma su carrito, el sistema genera un pedido.

Cada pedido almacena:

* Número de pedido.
* Cliente.
* Fecha.
* Estado.
* Subtotal.
* Impuestos.
* Total.
* Productos adquiridos.

Estados contemplados:

```text
PENDING
CONFIRMED
PROCESSING
SHIPPED
DELIVERED
CANCELLED
```

---

# 💳 Pagos

El sistema está diseñado para soportar diferentes métodos de pago.

Métodos contemplados:

```text
ONLINE
BANK_TRANSFER
CASH_ON_DELIVERY
```

Los pagos mantienen información como:

* Identificador de transacción.
* Método de pago.
* Estado.
* Valor.
* Fecha.
* Fecha de confirmación.

Estados:

```text
PENDING
AUTHORIZED
PAID
FAILED
CANCELLED
REFUNDED
```

Para pagos online se contempla la integración con una **pasarela de pago externa**.

La arquitectura permite reemplazar o incorporar proveedores de pago sin modificar la lógica principal de pedidos.

---

# 📄 Comprobantes y PDF

El sistema permitirá generar documentos PDF asociados a las compras.

Los comprobantes podrán ser generados por:

* Cliente.
* Administrador.

El documento podrá incluir:

```text
Información del pedido
Información del cliente
Productos
Cantidad
Precio unitario
Subtotal
Impuestos
Total
Método de pago
Estado del pedido
Fecha
```

---

# 📧 Recuperación de contraseña

Los clientes podrán solicitar la recuperación de su contraseña mediante el correo electrónico registrado.

Flujo:

```text
Usuario
   │
   ▼
Solicitar recuperación
   │
   ▼
Sistema genera token
   │
   ▼
Correo electrónico
   │
   ▼
Enlace de recuperación
   │
   ▼
Nueva contraseña
```

Los tokens tendrán:

* Fecha de creación.
* Fecha de expiración.
* Estado de utilización.

Por razones de seguridad, el sistema no revelará si una dirección de correo está registrada.

---

# 📩 Formulario de contacto

El sistema utilizará un formulario de contacto para visitantes y clientes.

Los mensajes serán:

1. Validados.
2. Almacenados en la base de datos.
3. Notificados al administrador mediante correo electrónico.

Flujo:

```text
Usuario
   │
   ▼
Formulario de contacto
   │
   ├──────────────► Base de datos
   │
   └──────────────► Correo administrador
```

El administrador podrá consultar y gestionar los mensajes recibidos.

Estados:

```text
NEW
READ
REPLIED
ARCHIVED
```

Esta estrategia permite conservar un historial de comunicaciones y, al mismo tiempo, recibir una notificación inmediata.

---

# 🗄️ Base de datos

El proyecto utiliza **MySQL** como sistema gestor de base de datos.

Entidades principales:

```text
roles
users
categories
products
carts
cart_items
orders
order_items
payments
invoices
contact_messages
password_reset_tokens
```

Modelo simplificado:

```text
Role
 │
 └── User
      │
      ├── Cart
      │    └── CartItem
      │          └── Product
      │
      ├── Order
      │    ├── OrderItem
      │    │     └── Product
      │    │
      │    ├── Payment
      │    │
      │    └── Invoice
      │
      └── PasswordResetToken

Category
    │
    └── Product

ContactMessage
```

---

# 💡 Manejo del precio histórico

Una característica importante del diseño es que los productos comprados conservan el precio que tenían en el momento de realizar la compra.

Por ejemplo:

```text
Producto
Precio actual: $900.000

Pedido #1001
Precio de compra: $750.000
```

Aunque posteriormente el producto cambie a:

```text
$900.000
```

el pedido histórico seguirá conservando:

```text
$750.000
```

Esto se implementa mediante:

```text
OrderItem
 ├── quantity
 ├── unitPrice
 └── subtotal
```

---

# 🏗️ Arquitectura

El backend utiliza una arquitectura por capas:

```text
                    CLIENTE
                       │
                       ▼
                 REST API
                       │
              ┌────────┴────────┐
              │                 │
              ▼                 ▼
        Controllers         Security
              │
              ▼
           Services
              │
              ▼
         Repositories
              │
              ▼
        JPA / Hibernate
              │
              ▼
             MySQL
```

Servicios externos:

```text
Spring Boot
    │
    ├── Email Service ─────► SMTP
    │
    ├── PDF Service
    │
    └── Payment Service ───► Payment Gateway
```

---

# 🧱 Estructura del backend

```text
src/
└── main/
    ├── java/
    │   └── com/
    │       └── aquality/
    │           └── store/
    │
    │               ├── config/
    │               ├── controller/
    │               ├── service/
    │               ├── repository/
    │               ├── entity/
    │               ├── dto/
    │               │   ├── request/
    │               │   └── response/
    │               ├── mapper/
    │               ├── security/
    │               ├── exception/
    │               ├── enums/
    │               ├── payment/
    │               ├── email/
    │               └── pdf/
    │
    └── resources/
        ├── application.properties
        └── db/
            └── migration/
```

---

# 🔌 API REST

La aplicación expondrá servicios REST organizados por dominio.

```text
/api/auth
/api/products
/api/categories
/api/cart
/api/orders
/api/payments
/api/contact
/api/admin
```

Ejemplos:

```http
POST /api/auth/register
POST /api/auth/login
POST /api/auth/password-reset

GET /api/products
GET /api/products/{id}

GET /api/cart
POST /api/cart/items
PUT /api/cart/items/{id}
DELETE /api/cart/items/{id}

POST /api/orders
GET /api/orders
GET /api/orders/{id}

POST /api/payments

POST /api/contact
```

---

# 🔐 Seguridad

La seguridad del backend estará basada en:

* Spring Security.
* JWT.
* Password hashing.
* Control de acceso por roles.
* Validación de solicitudes.
* Protección de endpoints.
* Tokens de recuperación con expiración.
* Manejo global de excepciones.
* Variables de entorno para información sensible.

Las contraseñas nunca serán almacenadas en texto plano.

---

# 🧪 Pruebas

Se implementarán diferentes niveles de pruebas:

### Unitarias

```text
JUnit 5
Mockito
```

### Integración

```text
Spring Boot Test
```

### API

```text
Postman
Insomnia
```

### Documentación API

```text
OpenAPI
Swagger UI
```

Se realizarán pruebas sobre:

* Registro.
* Login.
* Autorización.
* Productos.
* Carrito.
* Pedidos.
* Pagos.
* Recuperación de contraseña.
* Contacto.
* Administración.

---

# 📐 UML

El proyecto incluye documentación UML desarrollada mediante PlantUML.

Diagramas:

```text
docs/
└── 06-uml/
    │
    ├── use-case-diagram.puml
    ├── class-diagram.puml
    ├── architecture-diagram.puml
    │
    ├── sequence-diagrams/
    │   ├── register.puml
    │   ├── login.puml
    │   ├── add-to-cart.puml
    │   ├── purchase.puml
    │   ├── password-recovery.puml
    │   └── contact.puml
    │
    ├── activity-diagrams/
    │   └── purchase.puml
    │
    └── state-diagrams/
        ├── order-status.puml
        └── payment-status.puml
```

---

# 🛠️ Tecnologías utilizadas

## Backend

* Java 25
* Spring Boot
* Spring Web
* Spring Data JPA
* Hibernate
* Spring Security
* JWT
* Bean Validation
* Maven

## Base de datos

* MySQL 8
* Flyway

## Frontend

* HTML5
* CSS3
* JavaScript

## Testing

* JUnit 5
* Mockito
* Spring Boot Test
* Postman
* Insomnia

## Documentación

* PlantUML
* OpenAPI
* Swagger UI
* Markdown

## DevOps

* Git
* GitHub
* Docker
* Docker Compose

## Servicios externos

* SMTP / servicio de correo electrónico
* Pasarela de pago

---

# 🔄 Migración tecnológica

El proyecto representa la evolución conceptual de:

```text
        APLICACIÓN LEGACY
              │
              ▼
     PHP + JavaScript
       HTML + CSS
          MySQL
              │
              ▼
       REINGENIERÍA
              │
              ▼
       AQUALITY STORE
              │
       ┌──────┴───────┐
       ▼              ▼
    Frontend        Backend
       │              │
 HTML/CSS/JS      Java/Spring
                      │
             ┌────────┼─────────┐
             ▼        ▼         ▼
           JPA     Security    REST
             │
             ▼
           MySQL
```

El objetivo no es realizar una traducción literal de PHP a Java, sino **rediseñar la aplicación aplicando una arquitectura moderna y mantenible**.

---

# 🗂️ Gestión de versiones de base de datos

Las modificaciones de la base de datos serán administradas mediante Flyway.

Ejemplo:

```text
db/
└── migration/
    ├── V1__create_tables.sql
    ├── V2__insert_initial_roles.sql
    ├── V3__insert_initial_categories.sql
    └── V4__...
```

Esto permite mantener un historial reproducible de las modificaciones realizadas sobre la base de datos.

---

# 🐳 Docker

El proyecto estará preparado para ejecutarse mediante Docker.

Componentes previstos:

```text
Docker Compose
│
├── Spring Boot
│
├── MySQL
│
└── Servicios auxiliares
```

El objetivo es facilitar la instalación y ejecución del proyecto en diferentes entornos.

---

# 🚀 Ejecución local

## Requisitos

Instalar:

```text
Java 25
Maven
MySQL 8
Git
Docker (opcional)
```

## Clonar

```bash
git clone <URL_DEL_REPOSITORIO>
cd aquality-store
```

## Configurar base de datos

Crear:

```sql
CREATE DATABASE aquality_store
CHARACTER SET utf8mb4
COLLATE utf8mb4_unicode_ci;
```

Configurar las credenciales mediante variables de entorno.

## Ejecutar

En Windows:

```powershell
.\mvnw.cmd spring-boot:run
```

En Linux/macOS:

```bash
./mvnw spring-boot:run
```

La aplicación estará disponible normalmente en:

```text
http://localhost:8080
```

---

# 📌 Estado del proyecto

> 🚧 **En desarrollo**

### Completado

* [x] Análisis de aplicación legacy.
* [x] Definición del alcance.
* [x] Identificación de funcionalidades.
* [x] Definición de roles.
* [x] Reglas de negocio.
* [x] Historias de usuario.
* [x] Requerimientos funcionales.
* [x] Requerimientos no funcionales.
* [x] MER definitivo.
* [x] Diseño UML.
* [x] Arquitectura inicial.
* [x] Definición de entidades.
* [x] Definición de relaciones JPA.

### En desarrollo

* [ ] Configuración Spring Boot.
* [ ] Migración Flyway V1.
* [ ] Entidades JPA.
* [ ] Repositories.
* [ ] Services.
* [ ] REST Controllers.
* [ ] DTOs.
* [ ] Manejo global de excepciones.
* [ ] Spring Security.
* [ ] JWT.
* [ ] Carrito.
* [ ] Pedidos.
* [ ] Integración de pagos.
* [ ] Generación de PDF.
* [ ] Servicio de correo.
* [ ] Frontend.
* [ ] Tests.
* [ ] Docker.
* [ ] Deploy.

---

# 🗺️ Roadmap

```text
FASE 1
Análisis y diseño
       │
       ▼
FASE 2
Base de datos + Flyway
       │
       ▼
FASE 3
Entidades JPA
       │
       ▼
FASE 4
Repositories + Services
       │
       ▼
FASE 5
REST API
       │
       ▼
FASE 6
Spring Security + JWT
       │
       ▼
FASE 7
Carrito + Pedidos
       │
       ▼
FASE 8
Pagos
       │
       ▼
FASE 9
PDF + Email
       │
       ▼
FASE 10
Frontend
       │
       ▼
FASE 11
Testing
       │
       ▼
FASE 12
Docker + Deploy
```

---

# 📚 Documentación

La documentación del proyecto se encuentra organizada dentro de:

```text
docs/
├── requirements/
├── business-rules/
├── user-stories/
├── database/
├── 06-uml/
├── api/
├── testing/
└── manuals/
```

En estas carpetas se documentan:

* Requerimientos.
* Historias de usuario.
* Reglas de negocio.
* Diccionario de datos.
* Modelo entidad-relación.
* Diagramas UML.
* Arquitectura.
* API REST.
* Casos de prueba.
* Manual técnico.
* Manual de usuario.

---

# 🎓 Propósito como proyecto de portafolio

Este proyecto está diseñado para demostrar conocimientos prácticos en:

```text
Java
Spring Boot
REST API
Spring Security
JWT
JPA
Hibernate
MySQL
SQL
Flyway
HTML
CSS
JavaScript
Git
GitHub
Docker
Testing
UML
Arquitectura de software
```

Además, busca demostrar el proceso completo de desarrollo de software:

```text
Análisis
   ↓
Requerimientos
   ↓
Diseño
   ↓
UML
   ↓
Base de datos
   ↓
Backend
   ↓
API REST
   ↓
Seguridad
   ↓
Frontend
   ↓
Testing
   ↓
Docker
   ↓
Deploy
```

---

# 👨‍💻 Autor

**OSLO**

Proyecto desarrollado con fines educativos, profesionales y de portafolio.

---

## 📄 Licencia

Este proyecto se desarrolla como proyecto personal de portafolio.

La licencia definitiva será definida durante la preparación del repositorio público.
