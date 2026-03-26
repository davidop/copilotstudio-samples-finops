# Conjuntos de pruebas para Evaluacion

Archivo principal:
- conjuntos_pruebas_pmo.csv
- conjuntos_pruebas_pmo.jsonl
- conjuntos_pruebas_pmo_strict.jsonl
- conjuntos_pruebas_pmo_portal_es.csv
- conjuntos_pruebas_pmo_import_input.csv
- conjuntos_pruebas_pmo_import_assertions.csv

## Cobertura
- Happy path: entrada al flujo, deteccion automatica de tipo de servicio y salida con trazabilidad.
- Happy path (extendido): deteccion por sinonimos de dominio (help desk, time and material, scrum, fixed price, advisory) y trazabilidad de confianza.
- Happy path (extendido): deteccion por nombre de archivo con confianza media cuando la evidencia principal proviene del nombre del adjunto.
- Error path: informacion insuficiente, fallo de adjunto, error inesperado, fallback y ambiguedad.
- Regresion: nueva revision, cierre y mejora de propuesta.

## Uso recomendado en Copilot Studio
Si aparece el aviso "Parece que a su archivo le faltaba informacion", usa primero:
- conjuntos_pruebas_pmo_portal_es.csv

Este archivo usa exactamente las columnas que aparecen en el portal:
- `Pregunta`
- `Respuesta esperada`

Si el portal no acepta el CSV original por el esquema de columnas, usa los archivos de importacion:
- conjuntos_pruebas_pmo_import_input.csv (formato enriquecido con `id`, `conjunto`, `input`, `expected_route_or_service`, `must_include`, `expected_output`, `expectedOutput`)
- conjuntos_pruebas_pmo_import_assertions.csv (incluye `must_include` para validacion manual)

1. Abrir apartado Evaluacion del agente.
2. Elegir Importar dataset y cargar primero `conjuntos_pruebas_pmo_import_input.csv`.
3. Si necesitas trazabilidad por caso, usa `conjuntos_pruebas_pmo_import_assertions.csv`.
4. Si el asistente de importacion solicita una columna de respuesta esperada, mapea `expectedOutput` (o `expected_output`).
5. Definir como criterio de exito la presencia de la frase indicada en `must_include`.
6. Ejecutar evaluacion despues de cada cambio en topics.

## Uso en pipelines o validacion automatizada
1. Consumir `conjuntos_pruebas_pmo.jsonl` como dataset de pruebas.
2. Para cada linea, enviar `input` al agente.
3. Validar que la respuesta contenga todos los valores en `expected.must_include`.
4. Si existe `expected.service_type`, validar tambien la trazabilidad del tipo detectado/seleccionado.

## Modo estricto
Usar `conjuntos_pruebas_pmo_strict.jsonl` cuando se requiera mayor control:
- `severity`: critical/high/medium para priorizacion.
- `must_not_include`: textos o errores que NO deben aparecer.

En la version actual se incluyen tambien validaciones de confianza esperada:
- Casos por sinonimo semantico: `confianza Alta`.
- Casos por nombre de archivo: `confianza Media`.

Regla sugerida:
- `critical`: fallo inmediato del pipeline.
- `high`: marcar build inestable.
- `medium`: registrar warning y seguimiento.

## Nota
Este repositorio no incluye un archivo nativo de configuracion del apartado Evaluacion.
Por eso los casos se entregan en varios formatos para adaptarse al import del portal.
