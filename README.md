# P5-Reconocimiento-De-Matriculas

###  Desarrollo

## Reconocimiento de matrículas y extracción de los carácteres

- Se ha entrenado un modelo de YoloV8 usando un un dataset de coches con matrícula española.
- Las funciones de `read_license_plate_easyocr` y `read_license_plate_pytesseract` realizan la lectura de los carácteres en una imagen con easyocr y pytesseract respectivamente.
- Para una imagen recorren los resultados obtenidos al aplicarle el modelo entrenado, se dibuja el rectangulo y se sacan las matrículas.
  ```py
  for r in results:
    boxes = r.boxes

    # Matriculas detectadas
    for box in boxes:
        x1, y1, x2, y2 = box.xyxy[0]
        x1, y1, x2, y2 = int(x1), int(y1), int(x2), int(y2)

        # Dibuja el contenedor y clase
        cv2.rectangle(img, (x1-10, y1-10), (x2+10, y2+10), (0, 0, 255), 4)

        # Imagen recortada de la matricula
        license_plate_crop = img[y1 - 10:y2 + 10, x1 - 10:x2 + 10]

        license_text = read_license_plate_easyocr(license_plate_crop)
        cv2.putText(img, license_text, [x1 -10, y1 -10], cv2.FONT_HERSHEY_SIMPLEX, 2, (0, 0, 255), 3)
  ```
- Se recorren los boxes obtenidos(las matrículas) y se obtienen las coordenadas del box obtenido `x1, y1, x2, y2 = int(x1), int(y1), int(x2), int(y2)`
- Se recorta la imagen de la matrícula y leemos sus caracteres utilizando easyocr
- Finalmente se dibuja el texto de la matrícula en la imagen original

  
- Para un video siendo procesado a tiempo real se recorre frame por frame y se trata como en el apartado anterior.

- 
- Para un video el cual primero es procesado primero y luego se muestra el video entero es necesario tener una lista `processed_frame` donde guardar los frames para luego mostrarlos.





###Fuentes de Información

Para conseguir los datasets utilizados y como ayuda para la realización de la práctica hemos accedido a las siguientes fuentes de información

- [roboflow](https://universe.roboflow.com/)
- [ultralytics](https://docs.ultralytics.com/modes/track/)
  

    
