# Coloquio Redes y Comunicaciones

### Por Arzeno Eugenio

**Despliegue en Vercel**

[https://coloquio-redes2024.vercel.app/](https://coloquio-redes2024.vercel.app/)

[https://coloquio-redes2024.vercel.app/crear-prompt](https://coloquio-redes2024.vercel.app/crear-prompt)

## Documentación

### Proyecto

Es una aplicación React con Next.js, usando los componentes que ofrece Shadcn para el Front.
Esto mejora drásticamente como se ve visualmente la aplicación y Next.js optimizó las llamadas a las API.

### Antes de comenzar

Teniedo un Sheet de Google ya creado, compartir el documento con la siguiente cuenta de mail
[tp4coloquioredes@tp4-coloquio-redes.iam.gserviceaccount.com](mailto:tp4coloquioredes@tp4-coloquio-redes.iam.gserviceaccount.com)

Darle permiso de Editor y no enviar notificaciones.

Ejemplo de como se debería de ver el modal de Compartir antes de aceptar.

![imagen.png](imagen.png)

Tener el SpreadSheetID del sheet a mano (está entre /d/ y /edit/)

![imagen.png](imagen%201.png)

### BackEnd

### **GET api/auth/login**

- **Descripción**: Muestra la página de inicio de sesión si el usuario no está autenticado. Si ya está autenticado, redirige al inicio.
- **Autenticación**: No requerida para mostrar la página de inicio de sesión, pero el acceso completo al sistema requiere autenticación.

### **GET api/auth/logout**

- **Descripción**: Cierra la sesión del usuario utilizando Auth0.
- **Autenticación**: Requerida.

### **GET api/auth/me**

- **Descripción**: Cierra la sesión del usuario utilizando Auth0.
- **Autenticación**: Requerida.

**Ejemplo de la información que trae:**

```json
{
  "sub": "auth0|5f8d4b3cfc13b740c7ed9e77",
  "name": "John Doe",
  "given_name": "John",
  "family_name": "Doe",
  "nickname": "johnny",
  "picture": "https://example.com/john-doe-picture.jpg",
  "email": "johndoe@example.com",
  "email_verified": true,
  "identities": [
    {
      "provider": "google-oauth2",
      "user_id": "1234567890",
      "connection": "google-oauth2",
      "isSocial": true
    }
  ],
  "roles": ["admin", "user"],
  "user_metadata": {
    "preferred_language": "en",
    "location": "USA"
  },
  "app_metadata": {
    "organization": "ExampleCorp"
  },
  "created_at": "2021-01-01T12:00:00.000Z",
  "updated_at": "2023-01-01T12:00:00.000Z"
}
```

---

### **POST api/ai-consulta**

- **Descripción**: Genera el contenido deseado usando Google Gemini.
- **Autenticación**: Requerida.
- **Body**:
    - `prompt`: Prompt para generar contenido.
    - `spreadsheetId`: ID de la hoja de cálculo de Google Sheets.
- **Respuesta**: JSON con el contenido generado (`text`) o un mensaje de error.

---

### **POST api/cargar-sheet**

- **Descripción**: Obtiene datos de una hoja específica en una hoja de cálculo y sus nombres de hojas.
- **Autenticación**: Requerida.
- **Body**:
    - `spreadsheetId`: ID de la hoja de cálculo.
    - `range`: Rango de celdas, en formato A1 (opcional).
- **Respuesta**:
    - `sheetData`: Datos de la hoja.
    - `fileName`: Nombre de la hoja de cálculo.
    - `sheetNames`: Lista de todas las hojas en la hoja de cálculo.
    
    O un mensaje de error.
    

---

### **POST api/generar-dataset**

- **Descripción**: Crea una nueva hoja dentro de una hoja de cálculo y añade datos provenientes de un formulario.
- **Autenticación**: Requerida.
- **Body**:
    - `spreadsheetId`: ID de la hoja de cálculo.
    - `sheetTitle`: Título para la nueva hoja.
    - `data`: Set de datos en formato json que se envía a una hoja nueva del Google Sheets.
- **Respuesta**: Texto de confirmación si los datos fueron añadidos correctamente o un mensaje de error.

### **POST api/agregar-fila**

- **Descripción**: Crea una nueva fila con los datos insertados.
- **Autenticación**: Requerida.
- **Body**:
    - `spreadsheetId`: ID de la hoja de cálculo.
    - `sheetTitle`: Título de la hoja.
    - `range`: El espacio que los datos nuevos van a ocupar.
    - `data`: Set de datos en formato json que se envía a una nueva fila del Google Sheets.
- **Respuesta**: Texto de confirmación si los datos fueron añadidos correctamente o un mensaje de error.

### **POST api/modificar-fila**

- **Descripción**: Modifica una fila con los datos insertados.
- **Autenticación**: Requerida.
- **Body**:
    - `spreadsheetId`: ID de la hoja de cálculo.
    - `sheetTitle`: Título de la hoja.
    - `range`: El espacio que los datos nuevos van a ocupar.
    - `data`: Set de datos en formato json que se que modifica una fila del Google Sheets.
- **Respuesta**: Texto de confirmación si los datos fueron modificados correctamente o un mensaje de error.

### **POST api/eliminar-fila**

- **Descripción**: Deja los campos vacíos de la fila deseada.
- **Autenticación**: Requerida.
- **Body**:
    - `spreadsheetId`: ID de la hoja de cálculo.
    - `sheetTitle`: Título de la hoja.
    - `range`: El espacio que los datos nuevos van a ocupar.
- **Respuesta**: Texto de confirmación si los datos fueron eliminados correctamente o un mensaje de error.

---

### FrontEnd

- **NavBar:**
Permite al usuario navegar, abrir y cerrar sesión.
- **Campo ID SpreadSheet:**
    
    El usuario ingresa el ID del SpreadSheet de Google Sheets que desea cargar y luego presiona el botón **Cargar**.
    
- **Campo de Texto para Prompt:**
    
    Área donde el usuario ingresa el prompt que se envía a Gemini con los datos de la hoja de cálculo seleccionada.
    
- **Botón para Enviar Prompt:**
    
    Envía al Backend una petición al Endpoint /generate.
    
- **Selector de Hojas:**
    
    Combo box que permite al usuario elegir una hoja dentro del SpreadSheet cargado. Este control está oculto y se muestra al cargar la hoja.
    
- **CRUD:**
    
    Permite agregar y modificar datos al Sheet deseado, permite utilizar la hoja de calculo como una base de datos.
    

### Trabajo Viejo

**Repositorio GitHub**

[GitHub - ArzenLeib/TP4Redes](https://github.com/ArzenLeib/TP4Redes)

**Despliegue en Vercel**

[https://tp-4-redes.vercel.app/](https://tp-4-redes.vercel.app/)

## Documentación

### Proyecto

Es una aplicación regular usando Node.Js con Express, para el Front renderizo archivos ejs para que me permita trabajar con variables tendro del html.

La elección de hacerlo así fue porque quería aprender como funcionaba ejs en un proyecto enfocado al BackEnd porque leí que ahí es donde su fuerte estaba, además al renderizarse dentro del servidor me permite tener Front y Back dentro de un repositorio y así facilitar el despliegue hecho en Vercel.

### Antes de comenzar

Teniedo un Sheet de Google ya creado, compartir el documento con la siguiente cuenta de mail
[tp4coloquioredes@tp4-coloquio-redes.iam.gserviceaccount.com](mailto:tp4coloquioredes@tp4-coloquio-redes.iam.gserviceaccount.com)

Darle permiso de Editor y no enviar notificaciones.

Ejemplo de como se debería de ver el modal de Compartir antes de aceptar.

![imagen.png](imagen.png)

Tener el SpreadSheetID del sheet a mano (está entre /d/ y /edit/)

![imagen.png](imagen%201.png)

### BackEnd

### **GET /login**

- **Descripción**: Muestra la página de inicio de sesión si el usuario no está autenticado. Si ya está autenticado, redirige al inicio.
- **Autenticación**: No requerida para mostrar la página de inicio de sesión, pero el acceso completo al sistema requiere autenticación.

### **GET /logout**

- **Descripción**: Cierra la sesión del usuario utilizando Auth0.
- **Autenticación**: Requerida.

---

### **GET /**

- **Descripción**: Muestra la página principal con datos de la hoja de cálculo.
- **Autenticación**: Requerida.
- **Respuesta**: Renderiza la vista `index.ejs` con:
    - `sheetNames`: Array de nombres de hojas de cálculo.
    - `fileName`: Nombre del archivo.
    - `sheetData`: Datos de la hoja seleccionada.

---

### **POST /generate**

- **Descripción**: Genera contenido usando Google Gemini y lo añade a una nueva hoja en una hoja de cálculo específica.
- **Autenticación**: Requerida.
- **Body**:
    - `prompt`: Prompt para generar contenido.
    - `spreadsheetId`: ID de la hoja de cálculo de Google Sheets.
- **Respuesta**: JSON con el contenido generado (`text`) o un mensaje de error.

---

### **GET /cargar-sheet**

- **Descripción**: Obtiene datos de una hoja específica en una hoja de cálculo y sus nombres de hojas.
- **Autenticación**: Requerida.
- **Query Params**:
    - `spreadsheetId`: ID de la hoja de cálculo.
    - `range`: Rango de celdas, en formato A1 (opcional).
- **Respuesta**: JSON con:
    - `sheetData`: Datos de la hoja.
    - `fileName`: Nombre de la hoja de cálculo.
    - `sheetNames`: Lista de todas las hojas en la hoja de cálculo.

---

### **POST /submit**

- **Descripción**: Crea una nueva hoja dentro de una hoja de cálculo y añade datos provenientes de un formulario.
- **Autenticación**: Requerida.
- **Body**:
    - `spreadsheetId`: ID de la hoja de cálculo.
    - `request`: Valor para la primera columna.
    - `name`: Valor para la segunda columna.
- **Respuesta**: Texto de confirmación si los datos fueron añadidos correctamente o un mensaje de error.

---

### **POST /**

- **Descripción**: Añade nuevos datos a una hoja existente en la hoja de cálculo y recarga la página principal con los datos actualizados.
- **Autenticación**: Requerida.
- **Body**:
    - `request`: Valor para la primera columna.
    - `name`: Valor para la segunda columna.
    - `spreadsheetId`: ID de la hoja de cálculo.
    - `range`: Rango de celdas, en formato A1.
- **Respuesta**: Renderiza la vista `index.ejs` con los datos actualizados.

---

### FrontEnd

- **Logout:**
Permite al usuario cerrar sesión llevandolo a la ruta `/logout`.
- **Campo ID SpreadSheet:**
    
    el usuario ingresa el ID del SpreadSheet de Google Sheets que desea cargar y luego presiona el botón **Cargar**.
    
- **Campo de Texto para Prompt:**
    
    Área donde el usuario ingresa el prompt que se envía a Gemini con los datos de la hoja de cálculo seleccionada.
    
- **Botón para Enviar Prompt:**
    
    Envía al Backend una petición al Endpoint /generate.
    
- **Selector de Hojas:**
    
    Combo box que permite al usuario elegir una hoja dentro del SpreadSheet cargado. Este control está oculto y se muestra al cargar la hoja.
