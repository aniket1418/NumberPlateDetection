Here is the project for the licence Plate detector.

Some guidelines to run the program 
1. Install Python 3.6
2. pip install opencv-python - install opencv-python from https://pypi.org/project/opencv-python/
3. pip install tesseract

Small description 
First importing the opencv package from 
-import cv2
Next import the pytesseract
-import pytesseract
Now need to read the image file from the local system
using this command 
-image = cv2.imread('26.jpg') - Here the way of reading the file 
Now we need to convert the color image into the black and white.
-gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

Now detection of the edges 
canny_edge = cv2.Canny(gray_image, 170, 200)


Now initialising of the licence plate coordinator
-contour_with_license_plate = None
license_plate = None
x = None
y = None
w = None
h = None

-Find the contour with 4 potential corners and creat ROI around it
for contour in contours:
    # Find Perimeter of contour and it should be a closed contour
    perimeter = cv2.arcLength(contour, True)
    approx = cv2.approxPolyDP(contour, 0.01 * perimeter, True)
    if len(approx) == 4:  # see whether it is a Rect
        contour_with_license_plate = approx
        x, y, w, h = cv2.boundingRect(contour)
        license_plate = gray_image[y:y + h, x:x + w]
        break

-Removing Noise from the detected image, before sending to Tesseract

-Text Recognition

-Detect the licence plate and the make a rectangele to the image
image = cv2.rectangle(image, (x, y), (x+w, y+h), (34, 148, 3), 3)
