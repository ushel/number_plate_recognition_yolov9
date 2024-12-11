# number_plate_recognition_yolov9

[Dataset](https://universe.roboflow.com/arvind-kumar-wjygd/anpr2-syxl7)

Clone and Install YOLOv9 repository

Download model weights

Download model weights

Train Custom model

Examine Training Results

Validate Custom Model   

Use Custom Model model weights and check results

Use the same detect.py for video to check if its tracking license plate using car.mp4 video if not present upload it in yolov9 folder

use Yolo v9 + easyOCR for extracting text from the license plate

Edit detect.py file and do the following changes 

1. Add module to detect.py file
    def perform_ocr_on_image(img, coordinates):
        x, y, w, h = map(int, coordinates)
        cropped_img = img[y:h, x:w]

        gray_img = cv2.cvtColor(cropped_img, cv2.COLOR_RGB2GRAY)
        results = reader.readtext(gray_img)

        text = ""
        for res in results:
            if len(results) == 1 or (len(res[1]) > 6 and res[2] > 0.2):
                text = res[1]

        return str(text)
        
2. Call the module

# EasyOCR code

    in write results module

        text_ocr = perform_ocr_on_image(im0,xyxy)
        label = text_ocr
        annotator.box_label(xyxy, label, color=colors(c, True))

        annotator.box_label(xyxy, label, color=colors(c, True))

save the file with different name say detect1.py

run and check the results
