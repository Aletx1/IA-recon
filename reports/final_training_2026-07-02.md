# Avance final IA Recon Birds - 2026-07-02

## Dataset usado

Se amplio el dataset local desde iNaturalist con fotos licenciadas `cc0`, `cc-by` o `cc-by-sa`.

- Total entrenable: 2368 imagenes
- Aves: 1596 imagenes
- No ave (`not_bird`): 772 imagenes
- Clases: 10 especies chilenas + `not_bird`
- Splits: 1893 train, 236 val, 239 test

Carpeta:

`data/final/raw/`

Manifests:

- `data/final/processed/final_chile_not_bird_manifest.csv`
- `data/final/processed/final_bird_gate_manifest.csv`

## Modelos entrenados

Se entrenaron dos modelos MobileNetV3Small con transferencia desde ImageNet:

1. Gate binario: decide si la imagen parece ave o no ave.
2. Clasificador: predice una de las especies chilenas o `not_bird`.

Ambos se exportaron a TensorFlow Lite para Android.

## Resultados gate ave/no-ave

Archivo de evaluacion:

`reports/evaluation_final_bird_gate_2026-07-02.json`

- Imagenes test: 239
- Accuracy top-1: 83.26%
- Umbral usado: 0.60
- Fraccion aceptada: 91.63%
- Accuracy entre aceptadas: 87.21%

Interpretacion: el gate quedo suficientemente util para filtrar contenido, pero en la app se agrego una regla conservadora para evitar falsos rechazos de aves reales.

## Resultados clasificador de especies

Archivo de evaluacion:

`reports/evaluation_final_species_2026-07-02.json`

- Imagenes test: 239
- Accuracy top-1: 56.07%
- Umbral usado: 0.40
- Fraccion aceptada automaticamente: 51.46%
- Accuracy entre aceptadas: 73.98%

Comparacion por umbral:

| Umbral | Fotos aceptadas | Precision entre aceptadas |
| --- | ---: | ---: |
| 0.30 | 72.80% | 64.94% |
| 0.40 | 51.46% | 73.98% |
| 0.50 | 38.91% | 81.72% |
| 0.60 | 24.69% | 88.14% |

Se eligio 0.40 para balancear demostracion y confiabilidad.

## Integracion en app

Se actualizaron los assets IA de la app Flutter:

- `assets/ai/bird_gate_int8.tflite`
- `assets/ai/bird_gate.labels.json`
- `assets/ai/species_int8.tflite`
- `assets/ai/species.labels.json`

Tambien se ajusto `BirdAiService`:

- El clasificador de especies se ejecuta junto al gate.
- Se acepta automaticamente solo cuando gate y especie tienen confianza suficiente.
- Si el gate duda, pero hay una especie probable, queda como revision manual.
- El rechazo `not_bird` es duro solo con confianza alta.
- La pantalla muestra las 3 predicciones principales.

## Validacion app

- `flutter analyze`: sin errores
- `flutter build apk --debug`: compilacion exitosa

APK:

`C:/Users/palo-/Desktop/uni/app aves/galeria_aves/build/app/outputs/flutter-apk/app-debug.apk`

Nota: la instalacion directa no se completo porque el celular ya no aparecia conectado por Flutter al final del proceso.
