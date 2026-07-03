# Dataset ampliado Aves Chile - 2026-07-02

## Fuente principal

Se amplio el dataset local usando la API de iNaturalist con fotos licenciadas como `cc0`, `cc-by` o `cc-by-sa`.

Las imagenes quedaron organizadas por clase en:

`data/final/raw/`

Los metadatos y licencias quedaron en:

- `data/final/processed/inaturalist_photos_expanded.csv`
- `data/final/processed/inaturalist_not_bird_photos.csv`
- `data/final/processed/inaturalist_not_bird_photos_expanded.csv`
- `data/final/processed/inaturalist_not_bird_extra_photos.csv`

## Conteo por clase

| Clase | Imagenes |
| --- | ---: |
| milvago_chimango | 180 |
| not_bird | 773 |
| patagioenas_araucana | 93 |
| phrygilus_gayi | 180 |
| pygochelidon_cyanoleuca | 63 |
| sephanoides_sephaniodes | 180 |
| sturnella_loyca | 180 |
| turdus_falcklandii | 180 |
| vanellus_chilensis | 180 |
| zenaida_auriculata | 180 |
| zonotrichia_capensis | 180 |

## Manifest de entrenamiento

Se regeneraron los manifests usados por el entrenamiento:

- Especies + no ave: `data/final/processed/final_chile_not_bird_manifest.csv`
- Gate ave/no-ave: `data/final/processed/final_bird_gate_manifest.csv`

El manifest principal contiene 2368 imagenes entrenables:

| Split | Imagenes |
| --- | ---: |
| train | 1893 |
| val | 236 |
| test | 239 |

Para el gate binario:

| Clase | Total |
| --- | ---: |
| bird | 1596 |
| not_bird | 772 |

## Observaciones

- Algunas especies no llegaron a 180 imagenes porque no habia suficientes fotos disponibles con los filtros de Chile, calidad de investigacion y licencias abiertas.
- `not_bird` incluye negativos de iNaturalist como plantas, hongos, perros, gatos, insectos, reptiles y anfibios.
- El siguiente paso recomendado es reentrenar ambos modelos con estos manifests ampliados y volver a copiar los `.tflite` a la app Flutter.
