# Dashboard Ejecutivo SG-SST — IMA Company SAS

Aplicación en Streamlit para visualizar de forma ejecutiva e interactiva los 14 instrumentos digitales del SG-SST del MVP de IMA Company SAS.

## Versión 3.0

Esta versión elimina el módulo **Carga y calidad de datos** y no incluye la página narrativa académica. El enfoque queda centrado en operación, gerencia y toma de decisiones.

### Mejoras incluidas

- Conexión preferente a Google Sheets desde la carpeta compartida del proyecto.
- Respaldo automático con archivos Excel locales incluidos en la carpeta `data/`.
- Centro de alertas SG-SST para priorizar vencimientos, acciones críticas y desviaciones.
- Diseño visual más ejecutivo con tarjetas KPI, semáforos y paleta institucional.
- Gráficos interactivos Plotly: barras, líneas, donuts, heatmaps, dispersión y tablas descargables.
- Filtros interactivos por año, sede, mes, estado, proceso, categoría, responsable, riesgo, prioridad y otros campos según el módulo.
- Botón **Actualizar datos** para limpiar caché y volver a consultar Google Sheets.
- Lectura robusta de hojas con encabezados desplazados, filas vacías o títulos superiores.

## Estructura

```text
streamlit_sgsst_dashboard_v3/
├── app.py
├── requirements.txt
├── README.md
├── .streamlit/
│   ├── config.toml
│   └── secrets.toml.example
└── data/
    └── archivos Excel de respaldo
```

## Origen de datos

La aplicación permite elegir en la barra lateral entre:

1. **Google Sheets**: lee los 14 instrumentos desde los IDs configurados en `GOOGLE_SHEETS` dentro de `app.py`.
2. **Archivos Excel locales**: usa los archivos `.xlsx` guardados en `data/`.

Si se selecciona Google Sheets y una hoja no carga por permisos, la app intenta usar automáticamente el Excel local de respaldo.

## Conexión pública por enlace

Para usar la conexión simple sin credenciales, asegúrese de que la carpeta o cada Google Sheet tenga permiso:

**Cualquier persona con el enlace → Lector**

Esta opción es práctica para demo académica, pero no se recomienda con datos sensibles reales de trabajadores.

## Conexión privada con cuenta de servicio

Para datos privados, use una cuenta de servicio de Google Cloud:

1. Cree una cuenta de servicio en Google Cloud.
2. Genere una clave JSON.
3. Comparta cada Google Sheet con el correo `client_email` de la cuenta de servicio como lector.
4. En Streamlit Community Cloud, abra la app > Settings > Secrets.
5. Pegue el contenido siguiendo el formato de `.streamlit/secrets.toml.example`.

No suba `secrets.toml` real al repositorio.

## Despliegue en Streamlit Community Cloud

1. Suba esta carpeta a GitHub.
2. Entre a Streamlit Community Cloud.
3. Cree una nueva app desde el repositorio.
4. Configure el archivo principal como:

```text
app.py
```

5. Verifique que `requirements.txt` esté en la raíz del repositorio o en la misma carpeta de `app.py`.
6. Si usará cuenta de servicio, cargue los secrets antes de desplegar o desde Settings.

## Recomendación de privacidad

Los instrumentos SG-SST pueden contener nombres, cargos, diagnósticos, restricciones médicas, accidentes, enfermedades laborales y datos sensibles. Para una demo pública se recomienda usar datos simulados o anonimizados.
