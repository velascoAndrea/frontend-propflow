# PropFlow — Frontend

Interfaz web construida con Vue.js 3 y TailwindCSS para buscar propiedades inmobiliarias en lenguaje natural. Se comunica con el backend FastAPI para traducir búsquedas a SQL usando un LLM local.

## Stack Tecnológico

- **Vue.js 3** — Composition API
- **TailwindCSS 3** — Estilos utilitarios
- **Axios** — Comunicación con el backend
- **Vite** — Bundler y servidor de desarrollo
- **Docker** — Contenedor de producción

## Estructura del Proyecto
```
frontend/
├── src/
│   ├── components/
│   │   ├── SearchBar.vue      # Campo de búsqueda con ejemplos rápidos
│   │   ├── SQLDisplay.vue     # Muestra el SQL generado por el LLM
│   │   ├── ResultsPanel.vue   # Maneja estados: cargando, error, sin resultados
│   │   └── PropertyCard.vue   # Tarjeta individual de propiedad
│   ├── App.vue                # Componente raíz y lógica principal
│   ├── main.js                # Punto de entrada
│   └── assets/
│       └── main.css           # Estilos globales con TailwindCSS
├── Dockerfile
├── package.json
├── vite.config.js
└── tailwind.config.js
```

## Componentes

### SearchBar.vue
Campo de texto donde el usuario escribe su búsqueda en lenguaje natural. Incluye ejemplos rápidos clicables y maneja el estado de carga deshabilitando el input mientras se procesa la consulta.

### SQLDisplay.vue
Muestra el SQL generado por el LLM con formato de código. Aparece solo cuando hay una búsqueda activa — sirve como herramienta educativa para ver cómo se traduce el lenguaje natural a SQL.

### ResultsPanel.vue
Maneja cuatro estados:
- **Cargando** — spinner animado mientras el LLM procesa
- **Error** — mensaje descriptivo del error del backend
- **Sin resultados** — mensaje amigable cuando no hay propiedades
- **Resultados** — grid de PropertyCards

### PropertyCard.vue
Tarjeta individual que muestra: tipo de propiedad con badge de color, precio en quetzales, título, descripción, habitaciones, baños, área en m² y ubicación.

## Instalación

### Con Docker Compose (recomendado)

Desde la raíz del repo principal:
```bash
docker-compose up --build
```

Abrir: **http://localhost:8080**

### Sin Docker — desarrollo local
```bash
npm install
npm run dev
```

> El backend debe estar corriendo en `http://localhost:8000`

### Solo el contenedor frontend
```bash
docker build -t propflow-frontend .
docker run -p 8080:8080 propflow-frontend
```

## Variables de Entorno

El frontend se conecta al backend en `http://localhost:8000` por defecto. Si necesitas cambiar la URL del backend modifica esta línea en `App.vue`:
```js
const response = await axios.post('http://localhost:8000/api/search', {
  query: query
})
```

## Buenas Prácticas Aplicadas

- **Componentes reutilizables** — cada responsabilidad en su propio componente
- **Composition API** — uso de `ref`, `defineProps`, `defineEmits` y `onMounted`
- **Manejo de estados** — cargando, error, sin resultados y con resultados
- **Deshabilitación de controles** — el botón y el input se deshabilitan durante la carga
- **Enter para buscar** — el campo responde a `@keyup.enter`
- **Formateo de precios** — usando `toLocaleString('en-US')` 

## Ejemplos de Búsquedas

- `Casas con 3 habitaciones en zona 10`
- `Apartamentos menos de Q150,000`
- `Propiedades con más de 2 baños`
- `Terrenos en zona 15`
- `Departamentos con 2 habitaciones en zona 13`

## Troubleshooting

**El frontend no conecta con el backend**
```bash
# Verificar que el backend está corriendo
curl http://localhost:8000
# Debe responder: {"message": "PropFlow API funcionando"}
```

**TailwindCSS no aplica estilos**
```bash
# Verificar que el archivo main.css tiene las directivas
cat src/assets/main.css
# Debe contener:
# @tailwind base;
# @tailwind components;
# @tailwind utilities;
```
