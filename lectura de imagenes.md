## Redimensionamiento de imágenes con OpenCV

Este código utiliza la librería OpenCV para cargar una imagen desde disco,
obtener sus dimensiones originales (altura, anchura y canales de color)
y redimensionarla manteniendo la proporción original.

La nueva altura se calcula a partir de un factor de escala basado en la
nueva anchura deseada, lo que evita la deformación de la imagen.

Finalmente, se muestran en pantalla tanto la imagen original como la
imagen redimensionada para poder compararlas visualmente.

``` python
import cv2 as cv
# Importa la librería OpenCV y la renombra como 'cv' para facilitar su uso

image = cv.imread("Biblioteca.JPG")
# Carga la imagen desde el archivo "Biblioteca.JPG"
# La imagen se almacena como un arreglo NumPy (matriz de píxeles)
# Si el archivo no se encuentra, 'image' será None

height, width, channels = image.shape
# Obtiene las dimensiones de la imagen:
# height   -> altura en píxeles
# width    -> ancho en píxeles
# channels -> número de canales de color (normalmente 3: BGR)

print("vector de la imagen:", image.shape)
# Muestra la forma de la matriz (alto, ancho, canales)

print("altura de la imagen:", height)
# Imprime la altura de la imagen

print("ancho de la imagen:", width)
# Imprime el ancho de la imagen

print("canales de la imagen:", channels)
# Imprime el número de canales de color

new_width = 600
# Define el nuevo ancho deseado para la imagen redimensionada

ratio = new_width / width
# Calcula el factor de escala para mantener la proporción original

new_height = int(height * ratio)
# Calcula la nueva altura usando el factor de escala
# Se convierte a entero porque OpenCV no acepta valores flotantes

resize_image = cv.resize(image, (new_width, new_height))
# Redimensiona la imagen usando el nuevo ancho y alto calculados

cv.imshow("imagen rescalada", resize_image)
# Muestra la imagen redimensionada en una ventana

cv.imshow("imagen preview", image)
# Muestra la imagen original en otra ventana

cv.waitKey(0)
# Espera indefinidamente hasta que el usuario presione una tecla

cv.destroyAllWindows()
# Cierra todas las ventanas abiertas por OpenCV
```
---
<img width="1024" height="576" alt="image" src="https://github.com/user-attachments/assets/b3528b11-2897-44e0-8857-2a33129c62be" />

