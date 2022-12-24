# Cotton Fiber Maturity Assessment via Digital Holography
 
Goal: Maturity assessment and quality estimation of the cotton fibers in holographic images.

Solution: Estimating fiber maturity by extracting per fiber structural and textural features using deep learning and image processing methods.

_Note: This project is currently under development. More updates to this repo would be commited._

_Please contact [me](mailto:farshad.bolouri@gmail.com) or the project lead, [Yildirim Kocoglu](mailto:mrkocoglu@yahoo.com), for more information regarding the project._


# Instance Segmentation of the Cotton Fibers

Standard methonds such as MaskRCNN performed very poorly for instance segmentation of the holographic cotton fibers.

Here are some output examples from the MaskRCNN model:

<table>
  <tr>
    <td><img src="https://github.com/FeriBolour/holoFiber-segmentation/blob/main/Images/MaskRCNN2.png" width=250 height=250 ></td>
    <td><img src="https://github.com/FeriBolour/holoFiber-segmentation/blob/main/Images/MaskRCNN3.png" width=250 height=250 ></td>
  </tr>
 </table>

Therefore, various techniques and state-of-the-art architectures were explored for this task.

## TensorMask

[TensorMask](https://arxiv.org/abs/1903.12174) follows a Dense Sliding-Window approach to solve the Instance Segmentation problem.

This approach did not give us good results either. Here's an example of output for a rather simple image.

<img src="https://github.com/FeriBolour/holoFiber-segmentation/blob/main/Images/TensorMask.png" alt="Bottom Camera Example" width="250" height="250">

you can see that even in case of two very well separated fibers, TensorMask is classifying some of the pixels belonging to the fiber on the right as the one on the left.

## VitDet

[VitDet](https://arxiv.org/abs/2203.16527) explores the use of state-of-the-art Vision Transformers as the backbone of the Object Detection network.

With VitDet, we definitely got better results than before. Here are some examples for rather complicated images:

<table>
  <tr>
    <td><img src="https://github.com/FeriBolour/holoFiber-segmentation/blob/main/Images/VitDet1.png" width=250 height=250 ></td>
    <td><img src="https://github.com/FeriBolour/holoFiber-segmentation/blob/main/Images/VitDet2.png" width=250 height=250 ></td>
  </tr>
 </table>
 
However, when giving much more complex input with more fibers intersecting with each other, the model didn't perform as well:

<table>
  <tr>
    <td><img src="https://github.com/FeriBolour/holoFiber-segmentation/blob/main/Images/VitDet3.png" width=250 height=250 ></td>
    <td><img src="https://github.com/FeriBolour/holoFiber-segmentation/blob/main/Images/VitDet4.png" width=250 height=250 ></td>
  </tr>
 </table>
 
 ## Rotated-MaskRCNN
 
After studying the outputs of the original Mask-RCNN model, we realized the fundamental issue with the approach to individualize the fibers, is the axis-aligned bounding boxes. 

As we know, Mask-RCNN follows the general approach of _Detection Followed by Segmention_ to solve the instance segmentation problem. Therefore, the inputs to the segmenation (semantic segmentation) network is the areas of the image enclosed by the their respective bounding-boxes. 

In our images, it is common to have fibers being alongside the diagonal of the image. The bounding-box for a fiber that is on the diagonal of the image, is basically the image itself, therefore, it would enclose all the other fibers in the image. This will make it very difficult for the semantic segmentation network to only pick out the pixels of the target fiber. Here's an example:

<img src="https://github.com/FeriBolour/holoFiber-segmentation/blob/main/Images/MaskRCNN1.png" width=250 height=250>

It can be seen that the bounding-box enclosing the fiber on the left is also enclosing the other three fibers. You can see how the segmentation for this fiber (red pixels) also includes other fibers.

Subsequently, we decided that the fundamental issue is the axis-aligned bounding-boxes. To solve this issue, we developed a custom Mask-RCNN model that uses Rotated-BBoxes in the object detection network instead of the axis-aligned ones. 

Here's an example of the output by the custom Faster-RCNN network that uses Rotated-BBoxes:

<img src="https://github.com/FeriBolour/holoFiber-segmentation/blob/main/Images/RotatedFastRCNN.png" width=350 height=350>

Currently we are actively working on a Rotated-MaskRCNN architecture that basically extends the Rotated-FasterRCNN.

Here are some preliminary results from our custom Rotated-MaskRCNN:

<table>
  <tr>
    <td><img src="https://github.com/FeriBolour/holoFiber-segmentation/blob/main/Images/RotatedMaskRCNN1.png" width=350 height=350 ></td>
    <td><img src="https://github.com/FeriBolour/holoFiber-segmentation/blob/main/Images/RotatedMaskRCNN2.png" width=350 height=350 ></td>
  </tr>
 <tr>
    <td><img src="https://github.com/FeriBolour/holoFiber-segmentation/blob/main/Images/RotatedMaskRCNN3.png" width=350 height=350 ></td>
    <td><img src="https://github.com/FeriBolour/holoFiber-segmentation/blob/main/Images/RotatedMaskRCNN4.png" width=350 height=350 ></td>
  </tr>
 </table>
