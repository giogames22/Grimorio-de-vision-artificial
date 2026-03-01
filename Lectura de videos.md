# 📚 Módulo 01: Manejo de Video y Captura

Este módulo contiene los scripts fundamentales para interactuar con archivos de video y periféricos (webcam) utilizando **OpenCV**. Es el primer paso para cualquier sistema de visión artificial, desde un seguidor de líneas hasta un detector de rostros.

## 🛠 Requisitos
* Python 3.x
* OpenCV (`pip install opencv-python`)

---

## 1. 🖼️ Captura del Primer Frame (Imagen Estática)
Este script permite abrir un archivo de video y extraer únicamente el primer cuadro. Es útil cuando necesitamos analizar una escena inicial o configurar una región de interés (ROI).

```python
import cv2 as cv

# Reemplaza 'ruta_de_tu_video.mp4' con el path de tu archivo
path = "ruta_de_tu_video.mp4"
video = cv.VideoCapture(path)

if not video.isOpened():
    print("Error: no se pudo abrir el archivo.")
else:
    print("El video abrió correctamente")
    
    # Leemos solo el primer frame
    ret, frame = video.read()

    if ret:
        cv.imshow("Primer Frame Extraído", frame)
        cv.waitKey(0) # Presiona cualquier tecla para cerrar
        cv.destroyAllWindows()
    else:
        print("Error al leer el frame")
    
    video.release()
```

---

## 2. 📷 Acceso a la Webcam
Fundamental para proyectos en tiempo real. Este código inicializa la cámara por defecto de tu computadora y captura una foto instantánea.

```python
import cv2 as cv 

# Abrimos la cámara por defecto (ID 0)
cap = cv.VideoCapture(0)

# Revisar si podemos abrir la cámara con éxito
if not cap.isOpened():
    print("Error: no se puede acceder a la webcam")
else:
    print("Se accedió a la cámara con éxito")
    
    # Leemos el primer frame para confirmar la captura
    ret, frame = cap.read()

    if ret:
        # Mostrar el frame usando imshow
        cv.imshow("Captura de Webcam", frame)
        cv.waitKey(0)
        cv.destroyAllWindows()
    else:
        print("Error: No se pudo capturar el frame")
        
# Liberar la webcam
cap.release()
```

---

## 3. 🎥 Reproducción de Video Completo
A diferencia de los anteriores, este script utiliza un ciclo `while` para procesar la secuencia de imágenes (frames) de forma continua, mostrando las propiedades técnicas del archivo.

```python
import cv2

# Reemplaza 'ruta_de_tu_video.mp4' con tu archivo
path = "ruta_de_tu_video.mp4"
cap = cv2.VideoCapture(path)

# Revisar si el video puede abrirse con éxito
if not cap.isOpened():
    print("Error: No se puede abrir el archivo de video")
else:
    print("El archivo de video se abrió con éxito")
    
    # Conseguir las propiedades del video
    frame_count = int(cap.get(cv2.CAP_PROP_FRAME_COUNT))
    fps = cap.get(cv2.CAP_PROP_FPS)
    print(f"Total frames: {frame_count}, FPS: {fps}")

    # Leer y mostrar cada frame del video
    while True:
        ret, frame = cap.read()
        
        if not ret:
            print("El video finalizó o ha ocurrido un error")
            break
            
        cv2.imshow("Reproductor de Video", frame)
        
        if cv2.waitKey(1) & 0xFF == ord('q'):
            break

# Parar la captura de video y cerrar la ventana
cap.release()
cv2.destroyAllWindows()
```

---

### 💡 Tips de Uso:
* **Salir de los videos:** En el script de reproducción continua, presiona la tecla **'q'** para cerrar la ventana limpiamente.
* **FPS:** Si el video se ve muy rápido o lento, puedes ajustar el valor dentro de `cv2.waitKey(valor)`.
