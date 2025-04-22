
# CAMERA CONEXIONS

## Wyze cam v3.

### Yolo v8

### Python code.
    
    import os
    import cv2
    import wyzecam
    
    # Autenticación con credenciales de Wyze
    auth_info = wyzecam.login(os.environ["WYZE_EMAIL"], os.environ["WYZE_PASSWORD"])
    account = wyzecam.get_user_info(auth_info)
    
    # Obtener la lista de cámaras y seleccionar la primera
    camera = wyzecam.get_camera_list(auth_info)[0]
    
    # Conectar y recibir el video en tiempo real
    with wyzecam.WyzeIOTC() as wyze_iotc:
        with wyze_iotc.connect_and_auth(account, camera) as sess:
            for (frame, frame_info) in sess.recv_video_frame_ndarray():
                cv2.imshow("Video Feed", frame)
                cv2.waitKey(1)

Pasos para usarlo:
- Instala la librería con pip install wyzecam.
- Configura tus credenciales de Wyze en variables de entorno (WYZE_EMAIL y WYZE_PASSWORD).
- Ejecuta el código en Jupyter Notebook y deberías ver el video en tiempo real.

Si necesitas más detalles, puedes revisar la documentación de la librería wyzecam en PyPI y revisar esta web:

    https://github.com/ai2ys/Jupyter-Notebook-with-Webcam-Liveview



33

##  Ideas para acceder al video 

acceder al video en tiempo real desde tu cámara Wyze V3 y luego procesarlo como desees. Algunas ideas de lo que podriamos hacer:
    
    - **Guardar fotogramas** en imágenes (`cv2.imwrite()`).
    - **Grabar el video** en un archivo (`cv2.VideoWriter()`).
    - **Aplicar visión artificial** con **OpenCV** o **YOLO** para detección de objetos.
    - **Transmitir el video** en streaming a otro dispositivo o servidor.
    - **Procesar eventos** con IA, como detección de movimiento o reconocimiento facial.

🚀📷✨



## PASARLO A UN MONITOR EN GODOT. :D !

Para mostrar el video de tu cámara **Wyze V3** en **Godot**, puedes usar el nodo **VideoPlayer**, que permite reproducir archivos de video en formatos compatibles como **Ogg Theora**. Sin embargo, como la cámara transmite en tiempo real, necesitarás convertir el flujo de video a un formato que Godot pueda manejar.

### Pasos para lograrlo:
1. **Capturar el video en Python** usando `cv2.VideoWriter()` para guardarlo en un archivo `.ogv`.
2. **Importar el video en Godot** y usar un nodo `VideoPlayer` para reproducirlo.
3. **Actualizar el video dinámicamente** si quieres que se muestre en tiempo real.

Si prefieres transmitir el video directamente, podrías explorar opciones como **RTSP** y usar un plugin en Godot para recibir el flujo de video.

Aquí tienes un tutorial sobre cómo reproducir videos en **Godot**.


        https://www.youtube.com/watch?v=FXzYjbX0nK0


🚀🎮

### trasmitir directamente o en vivo.

Para transmitir el video en vivo desde tu **Wyze V3** a **Godot**, puedes usar el protocolo **RTSP** (Real-Time Streaming Protocol), que permite enviar el video en tiempo real a otro software.

### Pasos para lograrlo:
1. **Habilitar RTSP en la cámara Wyze**:
   - Ve a la app de Wyze.
   - Activa **RTSP** en la configuración avanzada.
   - Obtén la URL RTSP (ejemplo: `rtsp://usuario:contraseña@ip_de_la_cámara/live`).

2. **Recibir el video en Python**:
   - Usa **OpenCV** para capturar el stream RTSP.
   - Convierte los fotogramas en una textura compatible con **Godot**.

3. **Mostrar el video en Godot**:
   - Usa un nodo `TextureRect` o `Sprite` para visualizar el video.
   - Actualiza la textura en tiempo real con los fotogramas recibidos.

Aquí tienes un tutorial sobre cómo ver la **Wyze Cam en una computadora** usando RTSP, lo cual puede ayudarte a integrarlo en **Godot** [aquí](https://aprendacctv.com/wyze-cam-en-una-computadora/). También puedes revisar cómo reproducir videos dentro de **Godot** en este [video](https://www.youtube.com/watch?v=FXzYjbX0nK0).

#### El código. 🚀🎮📷

Para transmitir el video en vivo desde tu **Wyze V3** a **Godot**, puedes usar el protocolo **RTSP** (Real-Time Streaming Protocol), que permite enviar el video en tiempo real a otro software.

### Pasos para lograrlo:
1. **Habilitar RTSP en la cámara Wyze**:
   - Ve a la app de Wyze.
   - Activa **RTSP** en la configuración avanzada.
   - Obtén la URL RTSP (ejemplo: `rtsp://usuario:contraseña@ip_de_la_cámara/live`).

2. **Recibir el video en Python**:
   - Usa **OpenCV** para capturar el stream RTSP.
   - Convierte los fotogramas en una textura compatible con **Godot**.

3. **Mostrar el video en Godot**:
   - Usa un nodo `TextureRect` o `Sprite` para visualizar el video.
   - Actualiza la textura en tiempo real con los fotogramas recibidos.

Aquí tienes un tutorial sobre cómo ver la **Wyze Cam en una computadora** usando RTSP, lo cual puede ayudarte a integrarlo en **Godot** [aquí](https://aprendacctv.com/wyze-cam-en-una-computadora/). También puedes revisar cómo reproducir videos dentro de **Godot** en este [video](https://www.youtube.com/watch?v=FXzYjbX0nK0).

#### Transmitir el video en vivo de tu **Wyze V3** a **Godot** usando **RTSP** y OpenCV:

### **1. Capturar el video desde la cámara Wyze**
```python
import cv2

# URL RTSP de la cámara Wyze V3 (debes activarlo en la app de Wyze)
rtsp_url = "rtsp://usuario:contraseña@ip_de_la_cámara/live"

# Abrir el stream de video
cap = cv2.VideoCapture(rtsp_url)

while True:
    ret, frame = cap.read()
    if not ret:
        break

    # Mostrar el video en una ventana de OpenCV
    cv2.imshow("Wyze Cam Stream", frame)

    # Guardar cada fotograma como imagen para enviarlo a Godot
    cv2.imwrite("frame.jpg", frame)

    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

cap.release()
cv2.destroyAllWindows()
```

### **2. Mostrar el video en Godot**
En **Godot**, puedes usar un nodo `TextureRect` para actualizar la imagen en tiempo real:

```gdscript
extends TextureRect

func _process(delta):
    var image = Image.new()
    image.load("res://frame.jpg")  # Cargar el fotograma guardado
    var texture = ImageTexture.new()
    texture.create_from_image(image)
    self.texture = texture  # Actualizar la textura en tiempo real
```

### **Pasos para hacerlo funcionar**
1. **Habilita RTSP** en la app de Wyze y obtén la URL del stream.
2. **Ejecuta el código en Python** para capturar el video.
3. **En Godot**, usa el script para actualizar la textura con los fotogramas en tiempo real.


# The End.

Love is all:

https://youtu.be/VaOyotHRj3k?si=UOCVC48h2twSYg3l
