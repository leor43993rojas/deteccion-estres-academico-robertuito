# Detección de Estrés Académico con RoBERTuito — Fine-Tuning NLP

Proyecto de clasificación binaria de estrés académico en comentarios de estudiantes universitarios peruanos, mediante ajuste fino (fine-tuning) del modelo RoBERTuito (`pysentimiento/robertuito-base-cased`).

## Estructura del repositorio

```
├── README.md                   
├── data_estudiantes.csv         #si aparecen caracteres raros indicar: no guardar cambios. El dataset esta correcto, problema de visualización de Excel. 
├── 1_Expo_IA_PNL.ipynb          
├── Prueba_robertitu.ipynb       # Notebook ligero: solo predicción con el modelo ya entrenado

```

**Nota:** el modelo entrenado (`modelo_estres_final/`, ~385 MB) no está incluido en este repositorio de GitHub por exceder el límite de tamaño de archivo (100 MB). Está disponible en Google Drive mediante el siguiente enlace:

📁 **Modelo entrenado (descarga o acceso directo):**
`https://drive.google.com/drive/folders/1KS68tLE3svlmMI9DBbUTXqBrTTD-z8PY?usp=sharing`

Este enlace da acceso a la carpeta `modelo_estres_final`, que contiene:
- `model.safetensors` (pesos del modelo ajustado)
- `config.json`
- `tokenizer_config.json`
- `vocab.txt` / `tokenizer.json`
- `special_tokens_map.json`
- `training_args.bin`

## Instrucciones de ejecución (paso a paso)

### 1. Descargar este repositorio
Descarga el ZIP completo desde GitHub (botón verde "Code" → "Download ZIP") y descomprímelo.

### 2. Subir los archivos a Google Drive
1. Entra a (https://drive.google.com) con tu cuenta.
2. En **Mi unidad** (raíz principal, no dentro de otra carpeta), crea una carpeta llamada exactamente: `Proyecto_NLP`
3. Dentro de `Proyecto_NLP`, sube estos archivos descargados del repositorio:
   - `data_estudiantes.csv`
4. Descarga la carpeta `modelo_estres_final` desde el enlace de Google Drive indicado arriba (sección "Nota"), y súbela también dentro de `Proyecto_NLP`, manteniendo el nombre de carpeta y los 6 archivos internos intactos

La estructura final en tu Drive debe verse exactamente así:
```
Mi unidad/
└── Proyecto_NLP/
    ├── data_estudiantes.csv
    └── modelo_estres_final/
        ├── model.safetensors
        ├── config.json
        └── ... (resto de archivos)
```

**Importante:** el nombre de la carpeta (`Proyecto_NLP`) y de los archivos deben coincidir exactamente, incluyendo mayúsculas y guiones bajos — el código busca estas rutas de forma literal.

### 3. Elegir qué notebook ejecutar

Hay dos opciones, según lo que se quiera revisar:

**Opción A — Ver el proceso completo (`1_Expo_IA_PNL.ipynb`)**
Reproduce todo el pipeline desde cero. Toma entre 5 y 10 minutos en total.

**Opción B — Solo probar el modelo ya entrenado (`Prueba_robertitu.ipynb`)**
Carga directamente el modelo ya ajustado (sin reentrenar) y permite ingresar cualquier texto para obtener una predicción inmediata (Estrés / No Estrés) con su nivel de confianza. Toma menos de 1 minuto.

### 4. Subir el notebook elegido a Google Colab
1. Ve a [Google Colab](https://colab.research.google.com)
2. Archivo → Subir notebook → selecciona el `.ipynb` elegido

### 5. Activar GPU 
Cambiar tipo de entorno → GPU (T4)** → Guardar

### 6. Ejecutar
Corre todas las celdas en orden, de arriba hacia abajo (Entorno de ejecución → Ejecutar todas, o celda por celda con Shift+Enter). Al llegar al paso de `drive.mount()`, autoriza el acceso a tu Google Drive con tu cuenta.

## Autor
[Leonardo Abraham Rojas Payano] — Universidad de Lima
