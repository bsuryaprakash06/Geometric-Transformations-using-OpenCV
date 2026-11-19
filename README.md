# Geometric Transformations using OpenCV

## Objective
The objective of this project is to implement and evaluate fundamental 2D geometric transformations on digital images using OpenCV, NumPy, and Matplotlib in Python. Geometric transformations alter the spatial relationship between pixels by mapping source coordinates to destination coordinates, serving as essential preprocessing operations in computer vision pipelines. This experiment demonstrates the mathematical formulations and practical implementations of translation, scaling, shearing, reflection, rotation, and cropping on standard color imagery.

## Algorithm / Approach
Geometric transformations are executed using 2D affine mapping and direct spatial array manipulation:

- **Affine Transformation Framework**: General 2D affine transformations preserve collinearity and distance ratios using a $2 \times 3$ transformation matrix $M$ applied via `cv2.warpAffine(src, M, dsize)`:
  $$\begin{bmatrix} x' \\ y' \end{bmatrix} = \begin{bmatrix} m_{00} & m_{01} & m_{02} \\ m_{10} & m_{11} & m_{12} \end{bmatrix} \begin{bmatrix} x \\ y \\ 1 \end{bmatrix}$$
- **Image Translation**: Displaces pixel coordinates horizontally by $t_x$ and vertically by $t_y$ using the matrix:
  $$M = \begin{bmatrix} 1 & 0 & t_x \\ 0 & 1 & t_y \end{bmatrix}$$
  Implemented with translation offsets $t_x = 100$ and $t_y = 200$ pixels into an expanded destination canvas.
- **Image Scaling**: Resizes spatial dimensions using `cv2.resize` with bilinear interpolation (`cv2.INTER_LINEAR`), applying independent horizontal scaling factor $f_x = 2.0$ and vertical scaling factor $f_y = 1.0$.
- **Image Shearing**: Deforms image coordinates along the spatial axes using the affine shearing matrix:
  $$M = \begin{bmatrix} 1 & s_x & 0 \\ s_y & 1 & 0 \end{bmatrix}$$
  Configured with shear parameters $s_x = 0.5$ and $s_y = 0.5$.
- **Image Reflection**: Inverts coordinates across specified axes using `cv2.flip(image, flipCode)`, where a positive flip code yields a horizontal mirror reflection across the vertical axis.
- **Image Rotation**: Rotates the image about its center coordinates $(W/2, H/2)$ by an angle $\theta = 45^\circ$ using a matrix generated via `cv2.getRotationMatrix2D(center, angle, scale)` and mapped with `cv2.warpAffine`.
- **Image Cropping**: Isolates a rectangular region of interest (ROI) of dimensions $150 \times 200$ pixels using NumPy multi-dimensional array slicing `image[y:y+h, x:x+w]`.

## Results
The transformations were executed on an input color image (`Kia.jpg`, dimensions $400 \times 600 \times 3$ pixels) and visualized with Matplotlib:

- **Translation Output**: Shifts the input image downward and to the right within a $636 \times 438$ canvas, creating black border padding across unmapped regions.
- **Scaling Output**: Generates an anamorphically stretched image ($2\times$ width expansion while maintaining original height) with smooth boundary transitions via bilinear interpolation.
- **Shearing Output**: Displays angular parallelogram distortion resulting from simultaneous horizontal and vertical shear forces.
- **Reflection Output**: Produces a horizontal mirror image displayed in a two-panel side-by-side comparison alongside the original image.
- **Rotation Output**: Yields a $45^\circ$ counter-clockwise rotation centered within the original frame bounds, displaying black corner padding where transformed coordinates lie outside the canvas.
- **Cropping Output**: Extracts the top-left quadrant region ($150 \times 200$ sub-array), presented side-by-side with the complete source image for comparative inspection.

## References
- OpenCV Documentation: Geometric Transformations of Images (`cv2.warpAffine`, `cv2.getRotationMatrix2D`, `cv2.resize`, `cv2.flip`). https://docs.opencv.org/
- Gonzalez, R. C., & Woods, R. E. (2018). *Digital Image Processing* (4th ed.). Pearson.
- Szeliski, R. (2022). *Computer Vision: Algorithms and Applications* (2nd ed.). Springer.
