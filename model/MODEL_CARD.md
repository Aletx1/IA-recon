# Model Card - IA Recon AvesCL

## Objetivo

Reconocer aves chilenas en imagenes y reducir cargas incorrectas mediante una clase de rechazo `not_bird`.

## Arquitectura de decision

Se usa un flujo de dos etapas:

1. `bird_gate`: decide si la imagen parece ave o no.
2. `species_chile_not_bird`: estima la especie probable o `not_bird`.

Esta separacion mejora la seguridad del sistema porque evita confiar solo en un clasificador de especies cuando la imagen no corresponde a un ave.

## Modelos publicados

- `bird_gate_int8.tflite`: version cuantizada para app movil.
- `bird_gate_float32.tflite`: version Float32 de referencia.
- `bird_gate.keras`: respaldo Keras del modelo binario.
- `species_chile_not_bird_int8.tflite`: version cuantizada para app movil.
- `species_chile_not_bird_float32.tflite`: version Float32 de referencia.
- `species_chile_not_bird.keras`: respaldo Keras del modelo multiclase.

## Clases

El modelo multiclase incluye 10 especies chilenas y una clase `not_bird`.

Las labels exactas estan en:

- `bird_gate.labels.json`
- `species_chile_not_bird.labels.json`

## Umbrales

- `bird_gate`: aceptacion desde 0,60.
- `species_chile_not_bird`: aceptacion desde 0,40.
- Rechazo fuerte de `not_bird`: desde 0,90 en la integracion movil.

## Limitaciones

- El dataset todavia es pequeno para uso productivo.
- Algunas especies visualmente parecidas pueden confundirse.
- Fotos con mala luz, baja resolucion o ave pequena en el encuadre bajan la confianza.
- Se recomienda mantener revision humana para casos de confianza media.

## Mejoras futuras

- Ampliar dataset por especie.
- Balancear clases con mas imagenes reales de Chile.
- Agregar mas clases `not_bird`.
- Medir precision/recall por especie.
- Entrenar con aumentos de datos mas variados.
