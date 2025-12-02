# 🧶 Sistema de Presupuestos de Alfombras

Aplicación web desarrollada con **Spring Boot** para gestionar presupuestos de alfombras personalizadas.  
Permite registrar clientes, tamaños de alfombras, materiales utilizados (telas, hilados, pegamentos, etc.) y calcular el precio final del presupuesto. Incluye una interfaz web hecha con **Thymeleaf** y **Bootstrap**.

> 💡 Pensado como parte de la cursada de Programación Web / Desarrollo de Apliclicaciones Web y también como proyecto real para un emprendimiento de alfombras.

---

## 🚀 Tecnologías utilizadas

### Backend
- **Java** (versión 17+)
- **Spring Boot**
  - Spring Web (controladores MVC)
  - Spring Data JPA (repositorios y acceso a datos)
  - Spring Validation (validaciones de formularios)
  - Spring Security (protección de endpoints y login básico) ← _si no lo usaste, podés borrar esta línea_
- **Hibernate** (implementación JPA)
- **Maven** (gestor de dependencias y build)

### Frontend
- **Thymeleaf** (motor de plantillas HTML)
- **HTML5 / CSS3**
- **Bootstrap 5** (diseño responsivo y componentes visuales)
- **JavaScript** (para pequeñas interacciones en la vista, por ejemplo botones, tablas, confirmaciones, etc.)

### Base de datos
- **MySQL / MariaDB**
  - Tablas para: `presupuestos`, `telas`, `hilados`, `pegamentos` y otras entidades relacionadas
- Script SQL para carga inicial de datos de prueba (insert de presupuestos y materiales)

### Herramientas de desarrollo
- **Git & GitHub** (control de versiones)
- **IDE:** IntelliJ IDEA / STS / Eclipse (lo que estés usando)
- **Postman** (para probar endpoints REST, especialmente métodos `DELETE` y filtros)

---

## 🎯 Objetivo del proyecto

El objetivo de la aplicación es gestionar de forma sencilla los **presupuestos de alfombras**:

- Registrar datos del cliente
- Cargar el tamaño de la alfombra (ancho x largo)
- Seleccionar las telas y materiales usados
- Calcular el precio total según los materiales y el tamaño
- Listar, editar y eliminar presupuestos existentes

---

## ✨ Funcionalidades principales

### 🧾 Módulo de Presupuestos
- Alta de presupuestos desde un formulario web
- Listado de todos los presupuestos
- Edición y eliminación de presupuestos
- Búsqueda por nombre de cliente  
  (por ejemplo usando un método de repositorio tipo `findByNombreClienteContainingIgnoreCase`)
- Filtro por rango de precio total (mínimo y máximo) usando **Query Methods**

### 🎨 Módulo de Materiales (Telas, Hilados, Pegamentos)
- CRUD completo para:
  - Telas base
  - Telas de fondo
  - Hilados
  - Pegamentos
- Relación entre `Presupuesto` y los materiales a través de claves foráneas  
  (por ejemplo: `id_tela_base`, `id_tela_fondo`, `id_hilado`, `id_pegamento`)

### 🔐 Seguridad (si lo estás usando)
- Configuración de **Spring Security** para:
  - Proteger rutas específicas
  - Permitir usar Postman para probar endpoints `DELETE`/`PUT` sin romper la app
- Usuarios en memoria / configuración básica según la cursada

### 🖼️ Interfaz
- Vistas en Thymeleaf:
  - Listado de presupuestos
  - Formulario de creación/edición
  - Listado y formularios de materiales
- Botones con íconos (editar / eliminar) usando `<img th:src="@{imagenes/...}">`
- Estilos con **Bootstrap 5**:
  - Tablas responsive
  - Botones de acción
  - Layout con contenedores y columnas

---

## 🧱 Modelo de datos (resumen)

> Los nombres pueden variar según tu proyecto; ajustalos como los tengas en tus entidades.

**Entidad `Presupuesto` (ejemplo):**
- `idPresupuesto` (PK)
- `nombreCliente`
- `anchoAlfombra`
- `largoAlfombra`
- `precioTotal`
- Relaciones:
  - `telaBase` → `TelaBase`
  - `telaFondo` → `TelaFondo`
  - `hilado` → `Hilado`
  - `pegamento` → `Pegamento`

**Otras entidades:**
- `TelaBase`  
- `TelaFondo`  
- `Hilado`  
- `Pegamento`  

Cada una con su `id` propio y campos como `nombre`, `descripcion`, `precioUnitario`, etc.

---

## 🗂️ Organización del proyecto (paquetes)

Ejemplo de estructura en `src/main/java`:

- `controller`  
  Controladores Spring MVC para presupuestos y materiales.

- `service`  
  Lógica de negocio, clases de servicio que usan los repositorios.

- `repository`  
  Interfaces que extienden `JpaRepository` y definen **Query Methods**  
  (por ejemplo `findByNombreClienteContainingIgnoreCase`, `findByPrecioTotalBetween`, etc.)

- `model` / `entity`  
  Entidades JPA anotadas con `@Entity`.

- `dto`  
  Objetos de transferencia de datos para separar entidad ↔ formulario/vista  
  (si los estás usando en este proyecto).

- `config`  
  Clases de configuración (por ejemplo, `SecurityConfig`).

---

## ⚙️ Configuración y ejecución

### Prerrequisitos
- Java 17+
- Maven
- MySQL / MariaDB en ejecución

### 1. Clonar el repositorio

```bash
git clone https://github.com/tu-usuario/tu-repo-presupuestos-alfombras.git
cd tu-repo-presupuestos-alfombras
