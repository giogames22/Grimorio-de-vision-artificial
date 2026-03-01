# 📚 Anotaciones y Dibujo Básicos en Imágenes

Este módulo enseña cómo interactuar visualmente con las imágenes. Aprenderás a obtener las dimensiones de una imagen (importante para cálculos de robótica) y a dibujar formas geométricas básicas y texto. Estas técnicas son fundamentales para resaltar objetos detectados en sistemas de visión.

## 🛠 Requisitos
* Python 3.x
* NumPy (`pip install numpy`)
* OpenCV (`pip install opencv-python`)
* Una imagen de prueba (en el código la llamaremos `imagen_prueba.jpg`)

---

## 🖌️ Dibujo de Formas y Texto sobre Imágenes

Este script carga una imagen, imprime sus dimensiones en la terminal y luego dibuja sobre ella una línea, un rectángulo, un círculo y texto antes de mostrar el resultado.



```python
import numpy as np
import cv2

# --- 1. Carga de Imagen ---
# Reemplaza 'imagen_prueba.jpg' con la ruta de tu imagen
# Asegúrate de usar una imagen de 1024x683 para que coincida con las coordenadas originales,
# o usa una imagen propia y ajusta los puntos de dibujo.
ruta = 'imagen_prueba.jpg' 
image = cv2.imread(ruta)

if image is None:
    print("Error: No se pudo cargar la imagen. Verifica la ruta.")
    exit()

# --- 2. Obtener Medidas de la Imagen ---
# image.shape devuelve (alto, ancho, canales)
height, width, channels = image.shape
print(f"Dimensiones de la imagen:")
print(f" - Ancho: {width}px")
print(f" - Alto: {height}px")
print(f" - Canales de color: {channels}")

# --- 3. Dibujar Formas Geométricas ---
# Nota: OpenCV usa el orden de color BGR (Blue, Green, Red)

# A. Dibujar una LÍNEA
# cv2.line(imagen, punto_inicio(x,y), punto_fin(x,y), color(B,G,R), grosor)
# Dibuja una línea azul diagonal
cv2.line(image, (0, 0), (width, height), (255, 0, 0), 4)

# B. Dibujar un RECTÁNGULO
# cv2.rectangle(imagen, punto_sup_izq(x,y), punto_inf_der(x,y), color(B,G,R), grosor)
# Dibuja un rectángulo verde en los bordes. Si grosor es -1, se rellena.
cv2.rectangle(image, (0, 0), (width, height), (0, 255, 0), 3)

# C. Dibujar un CÍRCULO
# cv2.circle(imagen, centro(x,y), radio, color(B,G,R), grosor)
# Dibuja un círculo rojo
centro_x, centro_y = 410, 310
radio = 63
cv2.circle(image, (centro_x, centro_y), radio, (0, 0, 255), 2)

# --- 4. Añadir Texto ---
# Definimos la fuente
font = cv2.FONT_HERSHEY_SIMPLEX
# cv2.putText(imagen, texto, punto_inicio(x,y), fuente, escala, color(B,G,R), grosor, tipo_linea)
# Añade el texto 'OpenCV' en blanco
cv2.putText(image, 'OpenCV', (10, 500), font, 4, (255, 255, 255), 2, cv2.LINE_AA)

# --- 5. Mostrar Resultado ---
cv2.imshow('Imagen con Anotaciones', image)
cv2.waitKey(0) # Espera a que presiones una tecla para cerrar
cv2.destroyAllWindows()
```

---

### 🔬 Desglose de Puntos Clave:

1.  **`image.shape`**: Es fundamental recordar que NumPy devuelve las dimensiones en orden `(Alto, Ancho)`. Al dibujar en OpenCV, las coordenadas se usan como `(x, y)` donde `x` es el ancho e `y` es el alto.
2.  **Sistema de Coordenadas**: El origen `(0,0)` se encuentra en la esquina superior izquierda de la imagen.
3.  **Colores BGR**: A diferencia de la mayoría de los estándares (RGB), OpenCV lee y dibuja en Azul, Verde, Rojo. `(255, 0, 0)` es azul puro.
4.  **Grosor**: En las formas geométricas, un grosor positivo dibuja el contorno. Un grosor de `-1` (o la constante `cv2.FILLED`) rellena la forma por completo.
5.  **`cv2.LINE_AA`**: Se usa en `putText` para que los bordes de las letras se vean suavizados (anti-aliasing).

---
