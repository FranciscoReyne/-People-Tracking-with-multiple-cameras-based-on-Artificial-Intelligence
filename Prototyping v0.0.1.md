
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





# The End.

Love is all:

https://youtu.be/VaOyotHRj3k?si=UOCVC48h2twSYg3l
