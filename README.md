# Tablero Ambiental GPM

Tablero web (GitHub Pages) de los contadores ambientales del O&M del GPM. Reúne en un solo lugar los tres sectores que antes se llevaban en Excel separados: **PC Tratayén**, **PC Salliqueló** y **Oficina Administrativa General Acha**.

Cada tema (venteos, gas combustible, agua, residuos, etc.) tiene **un gráfico con una línea de color por sector**. El color de cada sector es fijo en todo el tablero.

## Archivos
- `index.html`: el tablero, en un solo archivo y sin dependencias.
- `Code.gs`: Apps Script que expone el Google Sheets como JSON.
- `BASE_AMBIENTAL_GPM.xlsx`: base para crear el Google Sheets.
  - **DATOS**: una fila por Año + Tema + Sector, con los meses Ene–Dic en columnas. Es la única pestaña de carga.
  - **TEMAS**: catálogo de temas, con ID, nombre, unidad, grupo y N° de contador ambiental.
  - **SECTORES**: nombre y color de cada sector.
  - **GRAFICOS**: un gráfico por tema con una línea por sector, dentro de la misma planilla.
  - **AYUDA**: instrucciones de carga.

## Puesta en marcha
1. Subir `BASE_AMBIENTAL_GPM.xlsx` a Drive y abrirlo como Google Sheets (Archivo > Guardar como Hojas de cálculo de Google).
2. En ese Sheets: Extensiones > Apps Script. Pegar `Code.gs` e implementarlo como aplicación web (Ejecutar como: Yo · Acceso: Cualquier usuario). Copiar la URL `/exec`.
3. En `index.html`, completar `const FUENTE = { appsScriptUrl: "https://script.google.com/macros/s/.../exec", sheetId: "" };`.
4. En GitHub: Settings > Pages > Deploy from branch `main` / root.

## Carga mensual
En **DATOS**, completar la columna del mes en cada fila. Dejar la celda vacía si todavía no hay dato y poner 0 si el valor es cero. Cargar solo números, sin unidades ni texto.
El tablero toma como corte el último mes que tenga algún valor cargado.
Para un tema nuevo, agregarlo en TEMAS y sumar sus filas en DATOS: el tablero lo toma solo. Para un año nuevo, copiar las filas, cambiar el Año y vaciar los meses.
Si la URL de datos falla, el tablero muestra la copia embebida y lo indica en el pie ("Fuente").
