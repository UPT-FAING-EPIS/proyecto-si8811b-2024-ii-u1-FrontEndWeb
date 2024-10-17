![./media/media/image1.png](./media/logo-upt.png)

**UNIVERSIDAD PRIVADA DE TACNA**

**FACULTAD DE INGENIERIA**

**Escuela Profesional de Ingeniería de Sistemas**

**Proyecto _{Nombre de Proyecto}_**

Curso: _Topicos de Base de Datos Avanzados I_

Docente: _Patrick Cuadros Quiroga_

Integrantes:

- **Rodrigo Samael Adonai Lira Alvarez (2019063331)**
- **Angelira Beatriz Romero Roque (2019063331)**

**Tacna – Perú**

***2024***

## Vistas de la Aplicación

### 1. Login Page (Página de inicio de sesión)
- **Descripción**: Esta es la primera vista que el usuario encuentra. En ella, el usuario ingresa su correo electrónico y contraseña para acceder a la aplicación.
- **Funcionalidad**:
  - Valida las credenciales del usuario contra el endpoint `/api/v1/auth/login`.
  - En caso de credenciales correctas, redirige a la vista de cursos del estudiante.
  - Si el login falla, muestra un mensaje de error.
- **Componentes**:
  - `input`: Para ingresar correo y contraseña.
  - `button`: Botón de envío de formulario.
- **Interacción con la API**:
  - POST a `/api/v1/auth/login` para validar las credenciales.

---

### 2. Student Courses (Cursos del Estudiante)
- **Descripción**: Vista donde se listan todos los cursos a los que está inscrito el estudiante.
- **Funcionalidad**:
  - Muestra una lista de cursos recuperados desde la API (`/api/v1/attendance`).
  - Cada curso está representado por una tarjeta que al hacer clic redirige a los detalles de asistencia del curso.
- **Componentes**:
  - `Tarjetas de curso`: Cada tarjeta representa un curso con el nombre del curso.
- **Interacción con la API**:
  - GET a `/api/v1/attendance` para obtener la lista de asistencias del usuario.

---

### 3. Attendance Details (Detalles de Asistencia)
- **Descripción**: Vista que muestra los detalles de la asistencia para un curso específico.
- **Funcionalidad**:
  - Muestra la lista de asistencias y su estado (presente, ausente, justificado, etc.) para el curso seleccionado.
  - Botón para justificar una inasistencia, que redirige a la vista de justificación.
- **Componentes**:
  - `Lista de asistencias`: Muestra el historial de asistencias por fecha.
  - `Botón Justificar Inasistencia`: Permite al estudiante justificar una falta.
- **Interacción con la API**:
  - GET a `/api/v1/sync/attendance` para obtener los detalles de asistencia del curso seleccionado.

---

### 4. No Attendance (Justificar Inasistencia)
- **Descripción**: Vista donde el estudiante puede justificar una inasistencia.
- **Funcionalidad**:
  - El estudiante puede ingresar los detalles de la justificación.
  - Envía la justificación a la API y regresa a los detalles de asistencia del curso.
- **Componentes**:
  - `Formulario`: Con campos para ingresar el asunto y los detalles de la justificación.
  - `Botón Enviar`: Envía la justificación a la API.
- **Interacción con la API**:
  - POST a `/api/v1/sync/justify-absence` para justificar la inasistencia.

---

## Descripción de las Vistas y Flujo de la Aplicación

- **Login Page**: Permite que el usuario ingrese sus credenciales y acceda a la aplicación. La autenticación se realiza a través de la API, y al autenticar correctamente, el usuario es redirigido a la página de cursos.
  
- **Student Courses**: Una vez autenticado, el estudiante verá una lista de los cursos a los que está inscrito. Cada curso está representado por una tarjeta que, al hacer clic, llevará al estudiante a la vista de detalles de asistencia de ese curso.

- **Attendance Details**: En esta página, el estudiante puede ver el historial de asistencias para el curso seleccionado, incluidas las fechas y el estado de cada asistencia (presente, ausente, justificado). Además, hay un botón para justificar una ausencia, lo que llevará al estudiante a la vista "No Attendance".

- **No Attendance**: Aquí, el estudiante puede llenar un formulario para justificar una inasistencia en un curso. Después de enviar el formulario, la justificación es enviada al servidor a través de la API y el estudiante es redirigido de vuelta a los detalles de asistencia del curso.

## Diagrama de Secuencia: Autenticación, Sincronización y Asistencia

```mermaid
sequenceDiagram
    participant Usuario
    participant Frontend
    participant API

    Usuario->>Frontend: Ingresa credenciales (email, contraseña)
    Frontend->>API: POST /api/v1/auth/login
    API-->>Frontend: Token de autenticación
    Frontend-->>Usuario: Redirige a StudentCourses

    Usuario->>Frontend: Ve cursos
    Frontend->>API: GET /api/v1/attendance
    API-->>Frontend: Lista de cursos y asistencias
    Frontend-->>Usuario: Muestra cursos como tarjetas

    Usuario->>Frontend: Selecciona un curso
    Frontend->>API: GET /api/v1/attendance (curso específico)
    API-->>Frontend: Detalles de asistencia del curso
    Frontend-->>Usuario: Muestra detalles de asistencia

## Diagrama de Componentes
graph TB
    subgraph Frontend [Frontend (React)]
        component1[Login Page]
        component2[Student Courses]
        component3[Attendance Details]
        component4[No Attendance Justification]
    end

    subgraph Backend [Backend (API)]
        api1[/api/v1/auth/login]
        api2[/api/v1/attendance]
        api3[/api/v1/sync/data]
        api4[/api/v1/sync/schedule]
        api5[/api/v1/sync/attendance]
        api6[/api/v1/auth/create-account]
    end

    subgraph Database [Base de Datos]
        db1[(Usuarios)]
        db2[(Cursos)]
        db3[(Asistencias)]
    end

    component1 --> api1
    component2 --> api2
    component3 --> api5
    component4 --> api5
    api1 --> db1
    api2 --> db3
    api5 --> db3
