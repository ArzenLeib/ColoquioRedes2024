esto es un proyecto next.js
quiero que lo mejores un poco la documentación, quiero que además de que esten explicados los endpoints quiero que aparezcan en una tabla y quiero que expliques tambien los comandos básicos que se utilizan en una tipica aplicacion de next.js
hacelo en markdown

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

Darle permiso de Editor y no enviar notificaciones.

Ejemplo de como se debería de ver el modal de Compartir antes de aceptar.

![imagen 1](https://github.com/user-attachments/assets/058af95b-4ef0-4eac-b15d-92d271f22c46)

Tener el SpreadSheetID del sheet a mano (está entre /d/ y /edit/)

![imagen](https://github.com/user-attachments/assets/194b67ca-58de-4901-900f-aaa31f3dc7cc)

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

json
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



---

### **POST api/ai-consulta**

- **Descripción**: Genera el contenido deseado usando Google Gemini.
- **Autenticación**: Requerida.
- **Body**:
    - prompt: Prompt para generar contenido.
    - spreadsheetId: ID de la hoja de cálculo de Google Sheets.
- **Respuesta**: JSON con el contenido generado (text) o un mensaje de error.

---

### **POST api/cargar-sheet**

- **Descripción**: Obtiene datos de una hoja específica en una hoja de cálculo y sus nombres de hojas.
- **Autenticación**: Requerida.
- **Body**:
    - spreadsheetId: ID de la hoja de cálculo.
    - range: Rango de celdas, en formato A1 (opcional).
- **Respuesta**:
    - sheetData: Datos de la hoja.
    - fileName: Nombre de la hoja de cálculo.
    - sheetNames: Lista de todas las hojas en la hoja de cálculo.
    
    O un mensaje de error.
    

---

### **POST api/generar-dataset**

- **Descripción**: Crea una nueva hoja dentro de una hoja de cálculo y añade datos provenientes de un formulario.
- **Autenticación**: Requerida.
- **Body**:
    - spreadsheetId: ID de la hoja de cálculo.
    - sheetTitle: Título para la nueva hoja.
    - data: Set de datos en formato json que se envía a una hoja nueva del Google Sheets.
- **Respuesta**: Texto de confirmación si los datos fueron añadidos correctamente o un mensaje de error.

### **POST api/agregar-fila**

- **Descripción**: Crea una nueva fila con los datos insertados.
- **Autenticación**: Requerida.
- **Body**:
    - spreadsheetId: ID de la hoja de cálculo.
    - sheetTitle: Título de la hoja.
    - range: El espacio que los datos nuevos van a ocupar.
    - data: Set de datos en formato json que se envía a una nueva fila del Google Sheets.
- **Respuesta**: Texto de confirmación si los datos fueron añadidos correctamente o un mensaje de error.

### **POST api/modificar-fila**

- **Descripción**: Modifica una fila con los datos insertados.
- **Autenticación**: Requerida.
- **Body**:
    - spreadsheetId: ID de la hoja de cálculo.
    - sheetTitle: Título de la hoja.
    - range: El espacio que los datos nuevos van a ocupar.
    - data: Set de datos en formato json que se que modifica una fila del Google Sheets.
- **Respuesta**: Texto de confirmación si los datos fueron modificados correctamente o un mensaje de error.

### **POST api/eliminar-fila**

- **Descripción**: Deja los campos vacíos de la fila deseada.
- **Autenticación**: Requerida.
- **Body**:
    - spreadsheetId: ID de la hoja de cálculo.
    - sheetTitle: Título de la hoja.
    - range: El espacio que los datos nuevos van a ocupar.
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
