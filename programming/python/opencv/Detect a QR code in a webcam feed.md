Pieced together from a few tutorials on the web. Note that the webcam I was targeting is the second device on my system; you may need to change the argument to `VideoCapture` to get the proper feed on your computer.

```python
import cv2 as cv

cap = cv.VideoCapture(1)
if not cap.isOpened():
    print("Cannot open camera")
    exit()

detector = cv.QRCodeDetector()

while True:
    ret, frame = cap.read()
    if not ret:
        print("Can't receive frame (stream end?). Exiting ...")
        break

    data, bbox, _ = detector.detectAndDecode(frame)
    if data:
        frame = cv.polylines(frame, bbox.astype(int), True, (0, 255, 0), 3)

    cv.imshow('frame', frame)
    
    if cv.waitKey(1) == ord('q'):
        break

cap.release()
cv.destroyAllWindows()
```

prerequisite: `pip install opencv-python`