# General Concepts of Computer Graphics

## 1) Image Capture and Transformation
- Although humans and computers use different mechanisms, both follow a similar process: they receive raw signals and interpret them. In humans, light hits sensory cells (rods and cones), and the brain interprets the resulting electrical signals. Computers, on the other hand, receive digital data from an image file or sensor, composed of bits, and analyze it through algorithms
- While humans rely on a single passive visual system, computers can capture data either actively (using infrared sensors, thermal cameras, motion sensors, etc.) or passively (via a traditional RGB image file)
  - Different sensors (RGB, thermal, depth, ultrasound cameras, etc.) allow algorithms to capture different aspects of reality, such as color, depth, heat, motion, and more

## 2) Pixel ("picture element"): The smallest visual unit of an image
- A digital image is typically composed of minimal units of color and brightness: pixels
- In the most common color model, RGB, each pixel is a numeric tuple consisting of 3 *channels*, where each channel represents a value for Red, Green, or Blue
- Bit depth defines how many color variations can be represented — that is, the precision with which each color is stored in a pixel
  - The higher the bit depth, the more accurate and nuanced the color representation will be, enabling smoother gradients and more realistic images
<img width="929" height="300" alt="image" src="https://github.com/user-attachments/assets/0a59aa18-50b1-447a-b636-23fdabcb6a30" />


- Another common model derived from RGB is *Grayscale*, where each pixel contains only one channel representing the intensity of light, usually ranging from 0 (black) to 255 (white) in 8-bit images
  - Grayscale is widely used due to its simplicity and lower computational cost, as it represents the image using only one intensity channel instead of three, preserving luminance information without requiring color

## 3) Image Formation
- Ultimately, an image is the visual reconstruction of a three-dimensional matrix — more accurately, a *Tensor*
- This *tensor* is composed of the (x, y) coordinates of each pixel and its associated color data, rendered on a display device or printed on paper
- Libraries such as OpenCV, PIL, and NumPy provide tools to access, modify, and analyze this data structure in Python in various ways
