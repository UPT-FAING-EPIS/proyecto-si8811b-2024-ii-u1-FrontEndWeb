![./media/media/image1.png](./media/logo-upt.png)

**UNIVERSIDAD PRIVADA DE TACNA**

**FACULTAD DE INGENIERIA**

**Escuela Profesional de Ingeniería de Sistemas**

**Proyecto _Asistencia UPT_**

Curso: _Topicos de Base de Datos Avanzados I_

Docente: _Patrick Cuadros Quiroga_

Integrantes:

- **Rodrigo Samael Adonai Lira Alvarez (2019063331)**
- **Angelira Beatriz Romero Roque (2019063327)**

**Tacna – Perú**

***2024***

## Descripción General del Proyecto

El software desarrollado es una plataforma integral de gestión de **asistencia**, **sincronización de datos** y **autenticación de usuarios**, diseñada para optimizar y automatizar el control de personal en organizaciones. La solución está compuesta por varios componentes interconectados que permiten a los usuarios realizar tareas clave como el registro de asistencia, la validación de identidad y la sincronización de información entre sistemas remotos y locales.

### Funcionalidades Principales

1. **Autenticación de Usuarios**: El sistema implementa un mecanismo de autenticación robusto, utilizando tokens JWT (JSON Web Token) para gestionar el acceso a las diferentes áreas del sistema. Cada usuario puede registrarse e iniciar sesión utilizando credenciales verificadas, garantizando la seguridad de la plataforma.

2. **Gestión de Asistencia**: La aplicación permite a los usuarios (administradores y empleados) registrar y consultar asistencia en tiempo real. Los administradores pueden visualizar informes detallados de asistencia, verificar ausencias y controlar entradas y salidas en función de las horas trabajadas.

3. **Sincronización de Datos**: La plataforma incluye una funcionalidad de sincronización para gestionar eficientemente la transferencia de datos entre servidores locales y en la nube. Esto asegura que los registros de asistencia y autenticación se mantengan actualizados en tiempo real, incluso en entornos distribuidos.

4. **Interfaz de Usuario Intuitiva**: El frontend de la aplicación está diseñado con una interfaz amigable y fácil de usar, lo que permite a los usuarios acceder a las funciones de la plataforma de manera rápida y eficiente. Se ha utilizado un enfoque responsivo para que la interfaz se adapte a diferentes dispositivos.

5. **API RESTful**: La aplicación expone un conjunto de servicios a través de una API REST, lo que permite a otros sistemas interactuar con la plataforma para obtener y enviar datos. Estos servicios facilitan la integración con sistemas de terceros, como sistemas de nómina o ERPs, para automatizar procesos empresariales clave.

### Componentes Técnicos
- **Frontend**: La interfaz está desarrollada utilizando React (u otro framework JavaScript de preferencia), ofreciendo una experiencia interactiva y dinámica para los usuarios finales.
  
### Objetivos del Proyecto

El objetivo principal del software es ofrecer una solución eficiente y confiable para el manejo de personal en empresas de distintos tamaños, permitiendo:
- Automatizar el proceso de control de asistencia.
- Reducir errores manuales en el registro y validación de información.
- Facilitar la integración de sistemas de información a través de servicios REST.
- Ofrecer un entorno seguro para la gestión de usuarios y datos sensibles.

Este sistema está diseñado para ser escalable y adaptable a diversas necesidades empresariales, mejorando la eficiencia en la gestión de recursos humanos y optimizando los procesos internos.

## Instalación

Sigue los pasos a continuación para instalar las dependencias del proyecto y correr la aplicación correctamente en tu entorno local.

1. **Clonar el Repositorio**

   Primero, clona este repositorio en tu máquina local usando git:

   ```bash
   git clone https://github.com/usuario/nombre-del-repositorio.git](https://github.com/UPT-FAING-EPIS/proyecto-si8811b-2024-ii-u1-FrontEndWeb.git
   
2. **Instalación de Dependencias**

Este proyecto utiliza varias dependencias que deben instalarse antes de ejecutar la aplicación. 

### El Frontend (React):

Instala Node.js: Si aún no tienes Node.js instalado en tu sistema, descárgalo e instálalo desde el sitio oficial de Node.js.

Una vez que tengas Node.js instalado, navega al directorio del frontend (si tu proyecto está separado en un subdirectorio)

```bash
cd sistema-asistencia
```
Instala las dependencias del proyecto usando el siguiente comando:

```bash
npm install
```
Esto instalará todas las dependencias listadas en el archivo package.json.

3. **Ejecutar el Proyecto**

Una vez instaladas las dependencias, puedes ejecutar  el frontend de la siguiente manera.
###Ejecutar el FrontEnd
Navega al directorio del frontend (si está separado):

```bash
cd sistema-asistencia
```
Ejecuta el siguiente comando para iniciar la aplicación frontend:

```bash
npm start
```
4. **Acceder a la aplicacion**
Una vez que el frontend estén en ejecución, puedes acceder a la aplicación desde tu navegador.

-**Interfaz del usuario (Frontend)**: Visita http://localhost:3000 para interactuar con la aplicación.

Esto iniciará la aplicación en modo de desarrollo, y podrás acceder a la interfaz en http://localhost:3000.

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
 ```

### Diagrama de Componentes

```mermaid
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

```
