
## Segmentation process can be parted into 3 parts:
### 1 — Pre-processing,
### 2 — Processing, and
### 3 — Post-segmentation.


## 1 — Pre-processing:

  First of all, we will convert our colored images to grayscale image, in order
to have only one channel image. Even without converting, we can observe
difference between these images characteristics. The first image         
contains small objects, and some have the same pixels values with the  
background. This aspect can cause the egdes detecting problem. 
So to prevent this, we think about image contrast adjustment, so we have to choose
among all contrast improving methods.

## 2  - Processing:

  we have different segmentation techniques that can be grouped into two parts: 
edges based techniques and region based techniques.
Otherwise, we can use threshold techniques to do a segmentation, in this case 
we must follow other processing techniques in order to get satisfactory result.

## 3  - Post-segmentetion:

  After the thresholding, we have many connected regions, this can not help us to count 
objects in the image cause the counting of objects is due to number of connected regions, so 
in addition, we have to apply some other techniques before count number of objects in the image.
We will go to follow erosion and dilatation techniques which will help us to connected 
nearest regions in order to have on region per object.
