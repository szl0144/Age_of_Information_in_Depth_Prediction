![](https://img.shields.io/badge/Python-3.6.9-blue) ![](https://img.shields.io/badge/PyTorch-1.0-yellow) ![](https://img.shields.io/badge/CUDA-9.0-orange) ![](https://img.shields.io/badge/OpenCV_Python-4.1.2-red)![](https://img.shields.io/badge/SciPy-1.1-green)
### <p align="center">Age of Information (AoI) in Depth Prediction</p>  

This is a revised version of model [struct2depth](https://github.com/tensorflow/models/tree/archive/research/struct2depth) using PyTorch library to evaluate the influence of AoI in monocular video depth prediction. We mainly do the changes in the following:<br>  
1. We change the predicted image from the second one to the last one in the 3 RGB image sequences for model training.<br> 
2. We add a time age with a range of (0,20)*20/fps to the target predicted image when we create the input dataset.<br>
3. We combine the dataset loading and model training into one interface [main.py](https://github.com/szl0144/Age_of_Information_in_Depth_Prediction/blob/master/main.py)<br>
4. We add a breakpoint of AoI for model training to solve the problem of 12 hours running time limit in Google Colab<br>
<br>
<div align=center><img width="550" height="300" src=./misc/model.png></div>

<br> 

```
Age_of_Information(AoI)  Supported
handle_motion  False
architecture    simple
joint_encoder  False
depth_normalization  True
compute_minimum_loss  True

Comment: There is no motion obejects prediction in this model!
```
![gif](./misc/rst.gif)  

The gif above is the training result of 1634 pictures and 95 epochs. 
<br> 
If you want to change the dataset size, you can change the length of the videos which are used for training.<br> 
If you want to change the training epochs, you can change the variable <i>args_epochs</i> at [main.py line 160](https://github.com/szl0144/Age_of_Information_in_Depth_Prediction/blob/47d4acc799c0d061810acd17756382727793546f/main.py#L160)<br>
``` 
args_epochs = 100
``` 


**Environment**  
Google_Colab 
<br>  

**Instruction**  

1. Film 2 videos which are 5-10 minutes using a smartphone without any moving objects, named the video as 1.mp4 and 2.mp4 and save them in the folder [video](https://github.com/szl0144/Age_of_Information_in_Depth_Prediction/tree/master/video) <br />
2. Print the image [Calib_Image_Print.png](https://github.com/szl0144/Age_of_Information_in_Depth_Prediction/blob/master/calib_jpg/Calib_Image_Print.png). Then take several photos of the chessboard image from differet viewpoint (Front, upper, lower, left and right).  <br />
4. Save all the images of the chessboard into the folder [calib_jpg](https://github.com/szl0144/Age_of_Information_in_Depth_Prediction/tree/master/calib_jpg) and replace the old images  <br />
5. Open the file Depth [Prediction.ipynb](https://github.com/szl0144/Age_of_Information_in_Depth_Prediction/blob/master/Depth_Prediction.ipynb) using Google Colab. <br />
6. Upload the depth prediction code into Google drive. <br />
7. Mount your Google drive on your Google Colab <br />
8. Come into the depth prediction project folder <br />
```
cd drive/My Drive/Colab_Notebooks/Age_of_Information_in_Depth_Prediction 
``` 
9. Update required packages SciPy 1.1 <br />
```
pip install scipy==1.1.0    
``` 
10. Run file [calib.py](https://github.com/szl0144/Age_of_Information_in_Depth_Prediction/blob/master/calib.py) <br />
```
!python calib.py 
``` 
11. Get camera intrinsics and copy the parameter matrix to [data_loader.py line 129](https://github.com/szl0144/Age_of_Information_in_Depth_Prediction/blob/master/data_loader.py#L129) <br />
12. run [main.py](https://github.com/szl0144/Age_of_Information_in_Depth_Prediction/blob/master/main.py) to train the model by.<br />
``` 
!python main.py
``` 
13. Run the next inference cell for depth inference of a single RGB image.<br />
14. Because google colab's maximum lifetime is only 12 hours, but our project can run more than 24 hours. I set a pattern that let the model can learn from AoI break point in the [main.py line 383](https://github.com/szl0144/Age_of_Information_in_Depth_Prediction/blob/47d4acc799c0d061810acd17756382727793546f/main.py#L383). You can restart the model training from the AoI value in the previous training if Google Colab terminate the previous training. To be mentioned, you should comment [main.py line 381](https://github.com/szl0144/Age_of_Information_in_Depth_Prediction/blob/47d4acc799c0d061810acd17756382727793546f/main.py#L381) if you restart the breakpoint traning.<br />
15. The validation loss, training loss and AoI in seconds are saved in loss_new.txt.<br />
16. The MATALB code which plot AoI vs training loss and validation loss figures is in [Loss_Depth.m](https://github.com/szl0144/Age_of_Information_in_Depth_Prediction/blob/master/MATLAB/Loss_Depth.m)</i>.<br />

**Credits**  
Heavily borrow code from [simplified_struct2depth](https://github.com/necroen/simplified_struct2depth), [sfmlearner](https://github.com/ClementPinard/SfmLearner-Pytorch), [monodepth](https://github.com/ClubAI/MonoDepth-PyTorch) and  
[original code in tensorflow](https://github.com/tensorflow/models/tree/master/research/struct2depth)  





