# 📚  Manejo de Video y Captura

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

## 2. 📷 Captura de Foto con la Webcam
Este código inicializa la cámara por defecto de tu computadora y captura una sola foto instantánea (un frame).

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

## 3. 🔴 Transmisión en Vivo desde la Webcam
Fundamental para proyectos de robótica en tiempo real. Utiliza un ciclo `while` para capturar y mostrar imágenes de tu cámara web continuamente hasta que decidas detenerlo.

```python
import cv2 as cv

# Abrimos la cámara por defecto (ID 0)
cap = cv.VideoCapture(0)

if not cap.isOpened():
    print("Error: No se puede acceder a la webcam")
else:
    print("Cámara iniciada. Presiona 'q' para salir.")
    
    # Ciclo para leer frames continuamente
    while True:
        ret, frame = cap.read()
        
        if not ret:
            print("Error al capturar el frame. Saliendo...")
            break
            
        # Mostramos el video en tiempo real
        cv.imshow("Video en Vivo", frame)
        
        # Esperamos 1 ms y verificamos si se presiona la tecla 'q' para salir
        if cv.waitKey(1) & 0xFF == ord('q'):
            break

# Liberamos la cámara y cerramos las ventanas
cap.release()
cv.destroyAllWindows()
```

---

## 4. 🎥 Reproducción de Video Completo
Este script utiliza un ciclo `while` para procesar la secuencia de imágenes (frames) de un archivo de video guardado en tu computadora, mostrando sus propiedades técnicas.

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
* **Salir de los videos:** En los scripts de reproducción continua (webcam y video), asegúrate de tener seleccionada la ventana de la imagen y presiona la tecla **'q'** para cerrarla limpiamente.
* **Múltiples Cámaras:** Si tienes más de una cámara conectada (por ejemplo, una USB para un robot), puedes cambiar `cv.VideoCapture(0)` por `cv.VideoCapture(1)` o `2`.
