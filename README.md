# MapAPELL — Visor Geoespacial APELL Bahía Blanca

[![Proceso APELL](https://img.shields.io/badge/APELL-Bahía%20Blanca-2e7d32)](index.html)

**MapAPELL** es un visor cartográfico interactivo desarrollado para el **Proceso APELL Bahía Blanca** (Awareness and Preparedness for Emergencies at Local Level). Permite consultar, visualizar y descargar capas geoespaciales relacionadas con la gestión del riesgo y la respuesta ante emergencias en el área del Polo Petroquímico de Bahía Blanca.

## 🗺️ Funcionalidades

- Visualización de capas GeoJSON sobre mapa interactivo (Leaflet.js)
- Área de influencia del Proceso APELL (barrios de Ingeniero White y alrededores)
- Capas temáticas:

  **Información del Proceso APELL**
  - **Edificios institucionales** — Delegación Ingeniero White, CTE y APELL
  - **Mangas de viento** — Con simulación de la dirección del viento en tiempo real
  - **Sirenas comunitarias**
  - **Puntos de encuentro**
  - **Empresas de 3era categoría** — Polígonos, rubro y contacto
  - **Handies Proceso APELL** — Ubicación y responsables
  - **Lugares de confinamiento**

  **Información complementaria**
  - **Barrios Proceso APELL** — Polígonos de los barrios del área de influencia
  - **Delegaciones municipales**
  - **Establecimientos educativos**
  - **Centros de Salud** — Hospitales, Unidades Sanitarias, CAPS, Salas Médicas
  - **Comedores Comunitarios** — Puntos de asistencia alimentaria
  - **Establecimientos Deportivos** — Clubes e instalaciones como zonas de concentración masiva
  - **Respuesta Primaria** — Bomberos, policía, defensa civil y atención médica
- Búsqueda global por nombre de ubicación y por dirección
- Filtro de capas en el panel lateral
- Cómo llegar / cálculo de rutas desde la ubicación del usuario o un origen personalizado
- Selector de mapa base (OpenStreetMap como mapa principal y Esri World Imagery satelital)
- Portal de descargas en formato GeoJSON

## 📁 Estructura

```
/
├── index.html          # Visor principal del mapa
├── descargas.html      # Portal de descargas de capas
├── vercel.json         # Configuración de despliegue en Vercel
├── package.json        # Scripts y dependencias del proyecto
├── api/                # Funciones serverless de Vercel (echo, geo, info, time)
├── img/                # Íconos de capas (mangas, sirenas, puntos de encuentro)
└── data/
    ├── *.js            # Datos GeoJSON embebidos como constantes JS (los usa el visor)
    └── *.json/*.geojson # Archivos GeoJSON originales para descarga
```

Cada capa tiene dos archivos en `data/`: el `.js` que lee el visor (por ejemplo `mangas.js` → `mangasData`) y el `.geojson`/`.json` que se ofrece en el portal de descargas.
Al actualizar una capa hay que actualizar ambos y, si se modifica un `.js`, subir el número de versión (`?v=`) en `index.html` y `descargas.html` para evitar la caché.

| Capa | Datos del visor | Archivo de descarga |
|------|-----------------|---------------------|
| Barrios | `barrios.js` | `BARRIOS_BAHIA_BLANCA.geojson` |
| Centros de salud | `centros_salud.js` | `CENTRO_SALUD.geojson` |
| Comedores | `comedores.js` | `comedores_com.json` |
| Deportivos | `deportivos.js` | `Estab_deportivos.json` |
| Respuesta primaria | `respuesta.js` | `Sistema de respuesta primaria - Digitalización.json` |
| Delegaciones | `delegaciones.js` | `Delegaciones_municipales_partido_Bahia_Blanca.geojson` |
| Escuelas | `escuelas.js` | `escuelas_ult.geojson` |
| Empresas del polo | `empresas.js` | `empresas_polo.geojson` |
| Mangas de viento | `mangas.js` | `MANGAS_VIENTO_APELL.geojson` |
| Sirenas | `sirenas.js` | `SIRENA_APELL.geojson` |
| Puntos de encuentro | `puntos_encuentro.js` | `PUNTOS_ENCUENTRO_APELL.json` |
| Handies | `handies.js` | `handies_procesoapell.geojson` |
| Confinamiento | `confinamiento.js` | `confinamiento_act.geojson` |
| Edificios institucionales | `instituciones.js` | `Instituciones.geojson` |

> Visor y descargas contienen exactamente los mismos datos: todos están en WGS84 (EPSG:4326) y con los mismos campos.

## 🚀 Uso

El proyecto es completamente estático (HTML + JS + CSS). Para ejecutarlo localmente:

```bash
# Con Node.js
npm start          # equivale a: npx serve .

# Con Python
python -m http.server 8080

# O simplemente abrí index.html en tu navegador
```

Para publicarlo en la web, basta con subir la carpeta del proyecto a cualquier servicio de hosting estático (GitHub Pages, Netlify, Vercel, etc.). Actualmente se despliega en Vercel (ver `vercel.json`).

## 🛠️ Tecnologías
- [Leaflet.js](https://leafletjs.com/) v1.9.4 — Librería de mapas interactivos
- [Font Awesome](https://fontawesome.com/) 6.4.0 — Iconografía
- [Google Fonts](https://fonts.google.com/) — Tipografía (Roboto)
- [Open-Meteo](https://open-meteo.com/) — Viento en tiempo real
- [OSRM](https://project-osrm.org/) — Cálculo de rutas
- [Nominatim](https://nominatim.org/) — Búsqueda de direcciones
- [Proj4js](https://proj4js.org/) — Solo como herramienta de desarrollo para convertir coordenadas UTM a WGS84 al preparar datos (no se usa en el visor)

## 📦 Datos

Los datos geoespaciales son producidos y mantenidos por el **Laboratorio de Geotecnologías (LabGeot)** — Mateo Asensi y colaboradores.

Las capas se proveen en formato GeoJSON y pueden descargarse libremente desde el [Portal de Descargas](descargas.html).

## 📄 Licencia

Datos y código © Proceso APELL Bahía Blanca / LabGeot. Uso libre con atribución.
