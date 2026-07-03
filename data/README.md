# Dataset

Esta carpeta contiene evidencia del dataset usado para el avance del proyecto.

## `mini_dataset/`

Muestra reducida con 55 imagenes:

- 5 imagenes por clase.
- 10 especies chilenas.
- 1 clase `not_bird`.

Esta muestra permite inspeccionar visualmente la composicion del dataset sin subir el dataset completo.

## `manifests/`

Contiene los CSV que documentan el dataset final:

- `final_bird_gate_manifest.csv`: manifiesto para el modelo binario `bird` vs `not_bird`.
- `final_chile_not_bird_manifest.csv`: manifiesto para el modelo multiclase.

## Dataset completo local

El dataset completo utilizado durante el entrenamiento contiene 2.368 imagenes y pesa aproximadamente 301 MB. No se incluye completo para mantener el repositorio liviano y facil de revisar.
