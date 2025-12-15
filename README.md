# Aplicación Evaluación Unidad 1

Esta es una aplicación móvil desarrollada con [Expo](https://expo.dev) y React Native que permite gestionar tareas personales con un sistema completo de autenticación.

## Desarrollado por

Este proyecto fue realizado por los estudiantes:
- **Daniela Baeza**
- **Yogerson López**
- **Fabián Torres**

## Características Implementadas

### Sistema de Autenticación
- **Registro de usuarios**: Los usuarios pueden crear una cuenta nueva con correo electrónico y contraseña
- **Inicio de sesión**: Autenticación con credenciales guardadas
- **Recuperación de contraseña**: Permite cambiar la contraseña usando el correo electrónico
- **Persistencia de sesión**: La sesión del usuario se mantiene incluso después de cerrar la aplicación usando AsyncStorage
- **Cerrar sesión**: Funcionalidad para desloguearse de forma segura

### Gestión de Tareas
- **Agregar tareas**: Crear nuevas tareas con título y descripción opcional
- **Visualizar tareas**: Lista de todas las tareas del usuario con información completa
- **Eliminar tareas**: Capacidad de eliminar tareas que ya no se necesiten
- **Interfaz intuitiva**: Diseño moderno con tema oscuro para una mejor experiencia visual

### Interfaz de Usuario
- Diseño moderno con tema oscuro
- Navegación fluida entre pantallas
- Validación de formularios con mensajes de error claros
- Experiencia de usuario optimizada

## Tecnologías Utilizadas

- **Expo** ~54.0.20
- **React Native** 0.81.5
- **TypeScript** ~5.9.2
- **React Navigation** - Para navegación entre pantallas
- **AsyncStorage** - Para almacenamiento local de datos
- **Expo Router** - Sistema de routing basado en archivos
- **Axios** - Cliente HTTP para comunicación con APIs
- **expo-image-picker** - Captura de imágenes desde cámara y galería
- **expo-location** - Servicio de geolocalización GPS

## APIs Utilizadas

### API Principal Backend
- **URL Base**: `https://basic-hono-api.borisbelmarm.workers.dev`
- **Framework**: Hono (API REST)
- **Endpoints**:
  - `POST /auth/register` - Registro de nuevos usuarios
  - `POST /auth/login` - Autenticación de usuarios
  - `POST /images` - Carga de imágenes
  - `GET /todos` - Obtener lista de tareas
  - `POST /todos` - Crear nueva tarea
  - `PUT /todos/:id` - Actualizar tarea
  - `DELETE /todos/:id` - Eliminar tarea

### APIs Externas
- **OpenStreetMap Nominatim** - Reverse geocoding para obtener direcciones legibles a partir de coordenadas GPS
- **Expo Location API** - Geolocalización nativa (móvil)

## Sistema de Autenticación

### Mecanismo de Autenticación
- **Tipo**: Bearer Token (JWT)
- **Flujo**:
  1. El usuario se registra o inicia sesión a través del endpoint `/auth/login` o `/auth/register`
  2. El servidor devuelve un token JWT que se almacena localmente con **AsyncStorage**
  3. Todas las peticiones posteriores incluyen el token en el header `Authorization: Bearer {token}`
  4. El token se persiste para mantener la sesión activa entre recargas de la aplicación

### Seguridad
- Los tokens se almacenan de forma segura en AsyncStorage (almacenamiento local del dispositivo)
- Las contraseñas se envían encriptadas en la primera solicitud y no se almacenan localmente
- Cada endpoint protegido requiere validación del token en el servidor
- Soporte para recuperación de contraseña con validación por correo electrónico

### Contexto de Autenticación
- Archivo: `components/context/AuthContext.tsx`
- Maneja: login, registro, cambio de contraseña, estado de autenticación global
- Provee: acceso al token, datos del usuario y funciones de autenticación a toda la aplicación

## Cómo ejecutar el proyecto

1. Instalar dependencias

   ```bash
   npm install
   ```

2. Iniciar la aplicación

   ```bash
   npx expo start
   ```

En la salida, encontrarás opciones para abrir la app en:

- [Development build](https://docs.expo.dev/develop/development-builds/introduction/)
- [Android emulator](https://docs.expo.dev/workflow/android-studio-emulator/)
- [iOS simulator](https://docs.expo.dev/workflow/ios-simulator/)
- [Expo Go](https://expo.dev/go), un sandbox limitado para probar el desarrollo con Expo

## Estructura del Proyecto

```
pizerria/
├── app/                    # Pantallas con routing basado en archivos
│   ├── login.tsx          # Pantalla de inicio de sesión
│   ├── register.tsx       # Pantalla de registro
│   ├── reset-password.tsx # Pantalla de recuperación de contraseña
│   └── home.tsx           # Pantalla principal con tareas
├── src/
│   ├── context/
│   │   └── AuthContext.tsx    # Contexto de autenticación global
│   ├── navigation/
│   │   └── RootNavigator.tsx  # Configuración de navegación
│   └── screens/
│       ├── LoginScreen.tsx    # Componente de login
│       ├── RegisterScreen.tsx # Componente de registro
│       └── HomeScreen.tsx     # Componente principal
└── assets/                # Recursos e imágenes

```

## Funcionalidades Clave

### Autenticación
- Los usuarios se almacenan localmente usando AsyncStorage
- Validación de correos existentes al registrarse
- Verificación de credenciales al iniciar sesión
- Cambio de contraseña con validación

### Gestión de Estado
- Context API para manejo global del estado de autenticación
- Estado local para las tareas en la pantalla principal
- Persistencia automática de datos de usuario

## Resumen de Desarrollo

Este proyecto es una aplicación móvil completa de gestión de tareas desarrollada con Expo y React Native. Combina autenticación robusta, almacenamiento en la nube y características avanzadas de captura multimedia y geolocalización.

### Logros Principales

1. **Sistema de Autenticación Completo**
   - Registro de usuarios con validación de correo
   - Login seguro con tokens JWT
   - Recuperación de contraseña
   - Sesiones persistentes

2. **Gestión de Tareas con Sincronización**
   - CRUD completo (Crear, Leer, Actualizar, Eliminar) de tareas
   - Sincronización con servidor backend
   - Almacenamiento local como respaldo

3. **Características Multimedia**
   - Captura de fotos desde cámara
   - Selección de imágenes desde galería
   - Carga de imágenes al servidor
   - Previsualización de imágenes antes de guardar

4. **Geolocalización e Integración de Mapas**
   - Captura de ubicación GPS en tiempo real
   - Conversión de coordenadas a direcciones legibles (reverse geocoding)
   - Almacenamiento y visualización de ubicaciones con tareas

5. **Experiencia de Usuario Optimizada**
   - Diseño moderno con tema oscuro
   - Interfaz intuitiva y responsiva
   - Validación de formularios con feedback claro
   - Navegación fluida entre pantallas

## Novedades Recientes

- **Captura y adjunto de imágenes (móvil y web):**
   - Se añadió la posibilidad de tomar fotos con la cámara o seleccionar imágenes desde la galería para adjuntarlas a cada tarea.
   - Implementación móvil: usamos `expo-image-picker` para `launchCameraAsync` y `launchImageLibraryAsync`.
   - Compatibilidad Web: se añadió un *fallback* que crea dinámicamente un `input type="file"` con `capture` cuando el navegador lo soporta, de modo que el botón "Tomar foto" en web abra la cámara o permita seleccionar un archivo.
   - La imagen se guarda en la propiedad `imageUri` de cada `Task` y se muestra como previsualización antes de guardar.
   - Archivos relevantes:
      - `components/ui/camera-button.tsx` — botón que unifica la acción de cámara/galería (full-width).
      - `components/ui/new-task.tsx` y `app/todos.tsx` — formularios que permiten tomar/seleccionar imagen y mostrar la previsualización.
      - `components/ui/task-item.tsx` — modal de edición que también permite cambiar la foto de la tarea.
   - Nota: en web `URL.createObjectURL(file)` se usa para previsualizar; estas URLs son temporales y no persisten entre recargas. Para persistencia entre sesiones se necesita subir la imagen a un servidor o serializarla (ej. base64) y guardar el resultado.

- **Integración de GPS y direcciones legibles:**
   - Se añadió captura de ubicación con `expo-location`: solicitud de permisos, obtención de coordenadas (`getCurrentPositionAsync`) y reverse geocoding.
   - Para obtener una dirección humana legible (calle, comuna, región, país) se utiliza `Location.reverseGeocodeAsync` en móvil.
   - Fallback web / robustez: se añadió una estrategia recomendada (o implementada en helpers) que consulta un servicio de geocodificación inversa (por ejemplo Nominatim / OpenStreetMap) cuando `reverseGeocodeAsync` no devuelve una dirección completa en web.
   - La dirección resultante se guarda en la propiedad `address` de la `Task` y se muestra en la lista de tareas y en el modal de edición.
   - Archivos relevantes:
      - `components/ui/new-task.tsx` — obtiene ubicación y muestra dirección en la UI antes de guardar.
      - `app/todos.tsx` — formulario alternativo que también captura ubicación y la persiste.
      - `components/ui/task-item.tsx` — permite capturar ubicación desde el modal de edición y guardarla con `updateTask`.
      - `components/context/TodosContext.tsx` — el tipo `Task` ahora incluye `address?: string | null`, `addTask` y `updateTask` persisten `address` en AsyncStorage (`@app_todos`).
   - Nota sobre Nominatim: si se usa Nominatim para fallback en web, es recomendable cachear resultados y respetar los límites de uso (rate limits). Para producción se recomienda un backend intermedio o servicio comercial.

## Cómo probar las nuevas funcionalidades

- Iniciar la app (PowerShell):
```powershell
npx expo start --clear
```
- Probar en móvil (Expo Go / dispositivo físico recomendado):
   - Crear una nueva tarea, usar "Tomar foto" para abrir la cámara, permitir permisos y tomar la foto.
   - Usar "Obtener ubicación" para aceptar permisos de localización y ver la dirección resuelta antes de guardar.

- Probar en web (navegador):
   - Abir la app con la opción web de Expo en el navegador.
   - El botón "Tomar foto" intentará abrir la cámara si el navegador lo soporta; en caso contrario mostrará el selector de archivos.
   - La dirección puede ser resuelta por el helper de geocodificación; si el navegador no devuelve una dirección legible se utilizará el fallback a Nominatim (si está habilitado).

# Nota: Este README fue realizado con el apoyo de IA 

