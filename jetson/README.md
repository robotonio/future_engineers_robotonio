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
    - get_image()
      - parameters: -
      - returns: an image 
- pillar.py: class Pillar
  - properties:
    - name (string, like 'red', 'green')
    - lowers (lower HSV bounds)
    - uppers (upper HSV bounds)
    - min_area (the minimum valid area)
  - methods
    - get_pos_size(image)
      - image: the image in which the search will be made
      - returns: a list with all pillars, sorted fron bigger to smaller eg [], [{'area':50, 'x':100, 'y':70, 'h'=-2, 'v'=4}], where
        - area: the pillar's area
        - x: x position on image
        - y: y position on image
        - h: horizontal distance from the center, from -10 to 10
        - v: vertical distance from the center, from -10 to 10
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
