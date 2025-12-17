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

## Redimensionamiento de imágenes por factor de escala

Este programa utiliza OpenCV para redimensionar una imagen aplicando
factores de escala en los ejes horizontal y vertical.

Se definen dos factores de reescalamiento: uno para reducir el tamaño
de la imagen (scaling down) y otro para ampliarla (scaling up).
La función `cv.resize()` utiliza estos factores junto con un método
de interpolación lineal para generar las nuevas imágenes.

Finalmente, se muestran en pantalla la imagen original, la imagen
reducida y la imagen ampliada para comparar los resultados.

```python
#redimensionamiento por factor de escala
import cv2 as cv

#cargamos la imagen 
image = cv.imread ("Biblioteca.JPG")

#agregamos los factores de reescalamiento
scale_down = 0.077
scale_up =  0.088

#imagen reescalada (scaling down)
rezised_down = cv.resize(image,None,fx=scale_down,fy=scale_down,interpolation=cv.INTER_LINEAR)
#imagen reescalada (scaling up)
rezised_up = cv.resize(image,None,fx=scale_up,fy=scale_up,interpolation=cv.INTER_LINEAR)

#mostrar los resultados
cv.imshow("Imagen original:", image)
cv.imshow("Imagen reducida:", rezised_down)
cv.imshow("Imagen ampliada:",rezised_up)

#cerrar hasta que presionemos una tecla
cv.waitKey(0)
cv.destroyAllWindows()
```
| Método | Descripción | Mejor uso para... |
| :--- | :--- | :--- |
| `INTER_NEAREST` | Interpolación por el vecino más cercano (rápida, baja calidad). | Redimensionado simple (pixel art, imágenes binarias). |
| `INTER_LINEAR` | Interpolación bilineal (**por defecto**). | Propósito general (equilibrio velocidad/calidad). |
| `INTER_CUBIC` | Interpolación bicúbica (entorno 4x4). | **Agrandar** con alta calidad (más suave). |
| `INTER_AREA` | Remuestreo por relación de área. | **Reducir** imágenes sin *aliasing* (sin ruido). |
| `INTER_LANCZOS4` | Interpolación Lanczos (entorno 8x8). | Alta calidad para agrandar/reducir (preserva detalles). |
