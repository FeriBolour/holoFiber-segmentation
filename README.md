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
    <td><img src="https://github.com/FeriBolour/holoFiber-segmentation/blob/main/Images/MaskRCNN1.png" width=400 height=300 ></td>
    <td><img src="https://github.com/FeriBolour/holoFiber-segmentation/blob/main/Images/MaskRCNN2.png" width=400 height=300 ></td>
    <td><img src="https://github.com/FeriBolour/holoFiber-segmentation/blob/main/Images/MaskRCNN3.png" width=400 height=300 ></td>
  </tr>
 </table>

Therefore, various techniques and state-of-the-art architectures were explored for this task.

## TensorMask

TensorMask follows a different approach to Instance Segmentation: Dense Sliding-Window framework

