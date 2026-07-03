# IA Recon AvesCL

Repositorio del avance final del agente de inteligencia artificial para reconocimiento de aves chilenas.

## Infografia web

La infografia publica del proyecto esta disponible en:

https://aletx1.github.io/IA-recon/

## Contenido del repositorio

- `index.html`: infografia web publicada con GitHub Pages.
- `assets/`: imagenes usadas por la infografia.
- `model/`: modelos entrenados y labels.
- `reports/`: metricas, evaluaciones y resumen del entrenamiento.
- `data/manifests/`: manifiestos CSV del dataset final usado para entrenamiento/evaluacion.
- `data/mini_dataset/`: muestra visual reducida del dataset, con 5 imagenes por clase.

## Modelos incluidos

El flujo final usa dos modelos:

1. `bird_gate`: clasificador binario para distinguir `bird` vs `not_bird`.
2. `species_chile_not_bird`: clasificador multiclase para especies chilenas y clase `not_bird`.

Archivos principales:

- `model/bird_gate_int8.tflite`: modelo binario optimizado para app movil.
- `model/species_chile_not_bird_int8.tflite`: modelo multiclase optimizado para app movil.
- `model/*.keras`: versiones Keras usadas como respaldo del entrenamiento.
- `model/*.labels.json`: labels asociados a cada modelo.

## Dataset

El dataset final local contiene 2.368 imagenes entrenables:

- 1.596 imagenes de aves.
- 772 imagenes de clase `not_bird`.
- 10 especies chilenas + clase `not_bird`.

Para mantener el repositorio liviano, se incluye:

- Una muestra en `data/mini_dataset/` con 55 imagenes, 5 por clase.
- Manifiestos CSV en `data/manifests/` para documentar la composicion completa del dataset.

## Resultados principales

Modelo `bird_gate`:

- Top-1 accuracy: 83,26%.
- Accepted accuracy: 87,21%.
- Accepted fraction: 91,63%.
- Threshold de aceptacion: 0,60.

Modelo `species_chile_not_bird`:

- Top-1 accuracy: 56,07%.
- Accepted accuracy: 73,98%.
- Accepted fraction: 51,46%.
- Threshold de aceptacion: 0,40.

## Uso esperado

El modelo fue preparado para una app movil de galeria de aves:

1. La imagen pasa primero por `bird_gate`.
2. Si parece ave, pasa por el clasificador de especies.
3. Si la confianza es suficiente, se acepta automaticamente.
4. Si la confianza es media, queda pendiente de revision.
5. Si parece no ser ave, se rechaza para evitar cargas incorrectas.

## Estado

Avance funcional para demostracion academica:

- Modelo entrenado.
- Dataset documentado.
- Muestra de imagenes incluida.
- Infografia publicada.
- Modelo exportado a TensorFlow Lite para integracion movil.
