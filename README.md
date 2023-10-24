 # <p align="center" width="100%" > BLASTOCYST IMAGE CLASSIFICATION </p> 
 
 In the context of in vitro fertilization (IVF), where the goal is to help individuals and couples achieve pregnancy, assessing the quality of blastocysts is of paramount importance.
 This quality assessment is typically guided by a set of well-established criteria known as the Gardner criteria. These criteria, consisting of Expansion (EXP), Inner Cell Mass (ICM), and Trophectoderm (TE), serve as the foundational benchmarks for evaluating blastocyst quality.
 Traditionally, this assessment has been the domain of expert embryologists. However, this essay explores an innovative avenue that leverages deep learning architectures, a subset of Deep learning models, including the xception architecture, is considered as promising alternatives for automating the task of grading blastocyst images.
 The key distinguishing feature of these deep learning models lies in their ability to automatically learn and extract meaningful features from blastocyst images. This holds the potential to significantly enhance the efficiency and consistency of the quality assessment
 process.
 In the evaluation of these deep learning models, I employed critical performance metrics such as accuracy, loss, precision and recall. With the xception architecture, we achieved 83,78% accuracy in the Expansion classification, 81%,08 in the ICM classification and 77%.30 in the TE classification.
 
 Key words : Deep learning, IVF, Time-lapse imaging, Automated blastocyst grading, Image processing...

 A blastocyst is a ball of cells that forms early, about five to six days after a sperm fertilizes an egg eventually becoming the embryo and then the fetus. Blastocysts are given a quality grade for each of the 3 components and the score is expressed with the expansion EXP(Expansion) grade listed first, the inner cell mass ICM grade listed second and the trophectoderm TE grade third. Here is a little break down to the embryo structure in
 the following figure:
 <p align="center" width="100%">
    <img width="33%" src="https://github.com/HraghiArij/Blastocyst-Image-Classification/assets/103947168/9f4ccb81-a2b8-480c-a4d0-38e2aa839c41"> 
    
</p><p align="center"><em>Expansion, Inner Cell Mass & TE </em></p>

## I- Preprocessing:
### 1- Canny filtering
 Canny Filtering leverages OpenCV for a series of image processing operations. It begins by loading the specified images and converting them to grayscale. Following this, Gaussian blurring is applied to reduce noise and create a smoother representation of the image. The Canny edge detection algorithm is then used to identify edges within the blurred image. To enhance the edges further, dilation is performed, which expands the detected edges. Subsequently, the code extracts the largest contour, assuming it to be the region of interest within the image. A bounding rectangle is computed around this region, and a mask is created to isolate it. The region of interest is then cropped from the original image and resized to a target size.
 ### 2- Hough:
 I proceeded to detect circles using the HoughCircles method. The code filters the detected circles. It identifies the largest circle and overlays a red circle on the original image to  highlight it. 
 The code then crops and resizes the region of interest defined by this circle, saving it as an enhanced image. The script is designed to process multiple images, iterating through a specified 
 directory, and saving the processed images to another directory. In cases where no valid circles are found in an image, the code handles this scenario by returning ’None.
 ### 3-Yolov8:
 Leveraging the YOLOv8 (You Only Look Once) model, I trained "yolov8n.yaml" model on 120 epochs after labeling images using CVAT.
 
 The Yolov8 gave the best result.
 
 ### 4- Blastocoel mask generation : 
 I was able to generate the ground truth blastocoel using the existing mask which was  necessary in the expansion classification.

 ### 5- Data augmentation on train set: 
 Horizontal flip, vertical flip, transpose horizontal flip, and transpose. This allowed us to increase the images number up to 940. The augmentation was  due to the limited size of the dataset.
 ### 6- Resizing : All images was resized to 299 x 299 pixels

## II- Results:
*Blastocyst Classification Results*
 <p align="center" width="100%">
    <img src="https://github.com/HraghiArij/Blastocyst-Image-Classification/assets/103947168/671a4101-423c-457a-82f3-17e009ed9f87"> 
</p>


