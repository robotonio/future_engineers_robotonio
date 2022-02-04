# Jetson project

## Circuit
~ to be constructed ~

## Scripts
- run1.py

- run2.py

- prep1.py

- prep2.py

- camera.py: class Camera
  - properties:
    - type (-1 for csi, > 0 for web cam)
    - width (1920X1080-30fps, 1280X720-60fps, **640**X480-90fps)
    - height (1920X1080-30fps, 1280X720-60fps, 640X**480**-90fps)
    - framerate (1920X1080-30fps, 1280X720-60fps, 640X480-**90**fps)
    - flip
      - **Default: 0, “none”**
      - (0): none – Identity (no rotation)
      - (1): counterclockwise – Rotate counter-clockwise 90 degrees
      - (2): rotate-180 – Rotate 180 degrees
      - (3): clockwise – Rotate clockwise 90 degrees
      - (4): horizontal-flip – Flip horizontally
      - (5): upper-right-diagonal – Flip across upper right/lower left diagonal
      - (6): vertical-flip – Flip vertically
      - (7): upper-left-diagonal – Flip across upper left/low
  - methods
    - get_frame()
      - parameters: -
      - returns: an image 
- pillar.py: class Pillar
  - properties:
    - name (string, like 'red', 'green')
    - lowers (lower HSV bounds)
    - uppers (upper HSV bounds)
    - min_area (the minimum valid area)
  - methods
    - get_info() 
      - parameters: -
      - returns: a string eith the pillar's info
- pillar_detector.py: class PillarDetector
  - properties:
    - pillars: the list with all possible pillars
  - methods:
    - pre_processing(self, image, blur=5, canny_thres=None, dia=1)
      - Prepares the image before processing
      - parameters:
        - image: the image to process
        - blur: the size of the kernel
        - canny_thres: the canny's algorithm threshold
        - dia: the dilation's iteations
    - find_color(self, image, hsv_image, hsv_bounds)
      - Creates the mask in the image with the desired hsv ranges and returns its bitwise_and with the image
      - parameters:
        - image: the image to look for color
        - hsv_image: the same image in HSV color space
        - hsv_bounds: the HSV lower and upper ranges
      - returns:
        - the bitwise_and result from the mask and the original image
    - find_contours(self, image, img_pre, min_area=10, sort=True, filter=0, draw_con=True)
      - looks for the outer contours of the image and returns the list of what was found
      - parameters:
        - image: the original image
        - img_pre: The image prepared by the method pre_processing
        - min_area: the size of the minimum area of valid contours in (square) pixels
        - sort: if True the list will be sorted in descending order of area (starting from the biggest)
        - filter: if > 0, the valid shape of the contours (eg 4 for rectangles), if 0, we don't care for the shape
        - draw_con: if True a green rectangle will enclose the contours found
      - returns:
        - returns a tuple with the list of detected outer contours and the processed image
    - detect_pillars(self, image)
      - detects all the pillars (see propetries) in the image
      - parameters:
        - image: the original image  
      - returns: 
        - the list with all the detected pillars
- communication.py: class Communication
  -  properties:
      - port (default "/dev/ttyTHS1")
      - baudrate (default 115200)
  -  methods
      - send_json(data)
        - data: the dictionary to send with serial
        - return: None
      - get_json()
        - return: the incoming dictionary from serial 
