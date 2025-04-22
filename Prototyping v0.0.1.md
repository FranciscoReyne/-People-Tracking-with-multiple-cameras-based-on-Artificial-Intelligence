
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




# The End.

Love is all:

https://youtu.be/VaOyotHRj3k?si=UOCVC48h2twSYg3l
