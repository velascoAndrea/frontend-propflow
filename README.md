# PropFlow — Frontend

Interfaz web construida con Vue.js 3 y TailwindCSS para buscar propiedades inmobiliarias en lenguaje natural.

## Stack
- Vue.js 3 
- TailwindCSS
- Axios
- Vite
- Docker

## Componentes

| Componente | Descripción |
|------------|-------------|
| `SearchBar.vue` | Campo de búsqueda con ejemplos rápidos |
| `SQLDisplay.vue` | Muestra el SQL generado por el LLM |
| `ResultsPanel.vue` | Maneja estados: cargando, error, sin resultados |
| `PropertyCard.vue` | Tarjeta individual de propiedad |

## Instalación local

### Con Docker
```bash
docker-compose up --build
```
Abrir: http://localhost:8080

### Sin Docker
```bash
npm install
npm run dev
```

## Variables de entorno
El frontend se conecta al backend en `http://localhost:8000` por defecto.

## Ejemplos de búsquedas
- `Casas con 3 habitaciones en zona 10`
- `Apartamentos menos de Q150,000`
- `Propiedades con más de 2 baños`
- `Terrenos en zona 15`