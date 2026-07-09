# Detección de Estrés Académico con RoBERTuito — Fine-Tuning NLP

Proyecto de clasificación binaria de estrés académico en comentarios de estudiantes universitarios peruanos, mediante ajuste fino (fine-tuning) del modelo RoBERTuito (`pysentimiento/robertuito-base-cased`).

## Estructura del repositorio

```
├── README.md                    # Este archivo
├── data_estudiantes.csv         # Dataset final (720 filas, balanceado, auditado)
├── 1_Expo_IA_PNL.ipynb          # Notebook completo: carga, split, fine-tuning, evaluación
├── Prueba_robertitu.ipynb       # Notebook ligero: solo predicción con el modelo ya entrenado
├── matriz_confusion_final.png   # Resultado visual de la evaluación final
└── modelo_estres_final/         # Modelo ya entrenado (pesos + tokenizer)
    ├── model.safetensors
    ├── config.json
    ├── tokenizer_config.json
    ├── vocab.txt
    ├── special_tokens_map.json
    └── training_args.bin
```

## Requisitos previos

- Cuenta de Google (para usar Google Colab y Google Drive)
- Conexión a internet
- No se requiere instalación local — todo corre en la nube (Google Colab con GPU gratuita)

## Instrucciones de ejecución (paso a paso)

### 1. Descargar este repositorio
Descarga el ZIP completo desde GitHub (botón verde "Code" → "Download ZIP") y descomprímelo.

### 2. Subir los archivos a Google Drive
1. Entra a [Google Drive](https://drive.google.com) con tu cuenta.
2. En **Mi unidad** (raíz principal, no dentro de otra carpeta), crea una carpeta llamada exactamente: `Proyecto_NLP`
3. Dentro de `Proyecto_NLP`, sube estos archivos (todos al mismo nivel, sin subcarpetas adicionales):
   - `data_estudiantes.csv`
   - `matriz_confusion_final.png`
   - la carpeta completa `modelo_estres_final` (con sus 6 archivos internos)

La estructura final en tu Drive debe verse exactamente así:
```
Mi unidad/
└── Proyecto_NLP/
    ├── data_estudiantes.csv
    ├── matriz_confusion_final.png
    └── modelo_estres_final/
        ├── model.safetensors
        ├── config.json
        └── ... (resto de archivos)
```

**Importante:** el nombre de la carpeta (`Proyecto_NLP`) y de los archivos deben coincidir exactamente, incluyendo mayúsculas y guiones bajos — el código busca estas rutas de forma literal.

### 3. Elegir qué notebook ejecutar

Hay dos opciones, según lo que se quiera revisar:

**Opción A — Ver el proceso completo (`1_Expo_IA_PNL.ipynb`)**
Reproduce todo el pipeline desde cero: carga de datos, división train/validation/test, tokenización, fine-tuning del modelo, y evaluación final con matriz de confusión. Toma entre 5 y 10 minutos en total.

**Opción B — Solo probar el modelo ya entrenado (`Prueba_robertitu.ipynb`)**
Carga directamente el modelo ya ajustado (sin reentrenar) y permite ingresar cualquier texto para obtener una predicción inmediata (Estrés / No Estrés) con su nivel de confianza. Toma menos de 1 minuto.

### 4. Subir el notebook elegido a Google Colab
1. Ve a [Google Colab](https://colab.research.google.com)
2. Archivo → Subir notebook → selecciona el `.ipynb` elegido

### 5. Activar GPU (obligatorio para ambos notebooks)
Menú superior: **Entorno de ejecución → Cambiar tipo de entorno → GPU (T4)** → Guardar

### 6. Ejecutar
Corre todas las celdas en orden, de arriba hacia abajo (Entorno de ejecución → Ejecutar todas, o celda por celda con Shift+Enter). Al llegar al paso de `drive.mount()`, autoriza el acceso a tu Google Drive con tu cuenta.

### 7. Resultados esperados (Opción A — pipeline completo)
- **F1-score del modelo fine-tuneado:** ≈ 0.97
- **Accuracy:** ≈ 0.97
- Matriz de confusión generada automáticamente y guardada en Drive

## Notas metodológicas importantes

- El dataset fue generado sintéticamente con apoyo de un LLM (Gemini) y sometido a un proceso de auditoría y limpieza para eliminar plantillas repetitivas y cuasi-duplicados, documentado en el informe adjunto.
- Se validó la dificultad del dataset mediante un modelo baseline (TF-IDF + Regresión Logística), obteniendo F1 = 0.868, lo que confirma que el dataset no es trivialmente separable antes del fine-tuning.
- El split de datos es estratificado: 70% entrenamiento / 15% validación / 15% test, con semilla fija (`random_state=42`) para reproducibilidad exacta.

## Autor
[Tu nombre] — Systems Engineering, Universidad de Lima
