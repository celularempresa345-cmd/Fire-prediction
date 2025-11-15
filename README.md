# ForestGuard
Código que se implementará en satelites con el objetivo de predecir incendios forestales.

Este proyecto utiliza una combinación de **Transfer Learning (MobileNetV2)** y **análisis de color en espacio HSV** para clasificar imágenes de bosques según su posible **riesgo de incendio**.  

Las clases disponibles son:

- 🟩 **Baja** → bosques muy verdes  
- 🟧 **Moderada** → tonos amarillos, naranjas o aspecto otoñal  
- 🟫 **Alta** → árboles secos: cafés, blancos o tonos deslavados  

El modelo fue diseñado para aprender correctamente incluso con un **dataset pequeño (~50 imágenes por clase)** gracias a técnicas avanzadas de regularización, aumento de datos y análisis de color.

---
## 📁 Dataset

Debido al tamaño de las imágenes, el dataset no está incluido directamente en este repositorio.  
Puedes descargarlo desde Google Drive en el siguiente enlace:

[📂 Descargar Dataset](https://drive.google.com/file/d/1WKnrjc4o1n9ZAiZsEtalPZdsOmuDWxYU/view?usp=sharing)

El dataset debe tener la siguiente estructura después de descargarlo:

`dataset/`
- `Baja/`
- `Moderada/`
- `Alta/`


Las carpetas deben llamarse exactamente:

- `Baja`
- `Moderada`
- `Alta`

---

## 🧠 Enfoque del Modelo

### ✔ Transfer Learning – MobileNetV2  
Se utiliza MobileNetV2 preentrenada en ImageNet, congelada para evitar sobreajuste.  
Encima se añaden capas densas con dropout para mejorar generalización.

### ✔ Data Augmentation  
Aplicado para incrementar variabilidad:

- rotaciones  
- desplazamientos  
- zoom  
- cambios de brillo  
- volteos horizontales  

### ✔ Análisis de Color en HSV  
La imagen se convierte a HSV y se calcula el porcentaje de píxeles:

- **verdes** → clase Baja  
- **amarillo/naranja** → clase Moderada  
- **café/blanco** → clase Alta  

La predicción final combina:
60% MobileNetV2 + 40% análisis de colores


Esto mejora mucho el rendimiento con datasets pequeños.

---

## 🚀 Flujo del Notebook

1. Importación de librerías  
2. Definición de parámetros  
3. Carga personalizada de imágenes (RGB/HSV)  
4. Generadores con aumentación  
5. Construcción del modelo MobileNetV2  
6. Entrenamiento con EarlyStopping  
7. Cálculo de color features (HSV)  
8. Función combinada de predicción  
9. Subida de imágenes para pruebas  

---

## ▶️ Ejemplo de Predicción

```python
label, conf = predict_image_color("mi_imagen.jpg")
print(f"Clase: {label} ({conf*100:.2f}%)")

El notebook mostrará:

-La imagen
-La clase predicha
-La confianza final

📦 Requisitos

Python 3.10+
TensorFlow / Keras
OpenCV
NumPy
Matplotlib
Google Colab (recomendado)

Instalación:

pip install tensorflow opencv-python numpy matplotlib
```
---

## 📸 Objetivo del Proyecto

Crear un sistema capaz de identificar el nivel de riesgo de incendio según:
1. La composición de colores
2. El estado aparente de la vegetación
3. Los patrones captados por MobileNetV2

Aplicable a investigación, análisis ambiental, proyectos estudiantiles y prototipos de alerta temprana.

---

## 🤖 Uso de ChatGPT

Este proyecto hizo uso de **ChatGPT (OpenAI)** como asistente para:

- Generación de código en Python y TensorFlow/Keras.
- Optimización del flujo de entrenamiento y predicción.

El uso de ChatGPT permitió acelerar el desarrollo y mejorar la claridad del código, aunque todas las decisiones finales de diseño, entrenamiento y prueba fueron tomadas por el autor.
