# To Understand the Sculpture-Gan!

* I just added the comments in Korean about the code without any fixations
* All codes are from robbiebarrat!

1. 코드 구성 

* binvox_rw.py -> binvox 파일을 python에서 읽을 수 있게 도와주는 귀여운 친구이다. 
binvox 파일에 대한 설명은 다음에 있다. ->  http://dimatura.net/misc_projects/binvox_rw_py/  
이 코드 역시 저 링크에서 따온듯 하다!

* generate_dataset.py -> 데이터 파일을 만들어야한다! 
stl 파일을 binvox 파일로 변환하고 저장하는 역할을 한다. render가 True 면 그림을 그려준다.  
특이 사항은 파이썬 2.7을 사용했다는 점 -> 이 코드를 사용하려면 파이썬 3.x로 수정해주는 것이 좋을 것 같다.

* Train을 할 때 DCGAN을 사용 -> 모양을 만들 때 Mnist -DCGAN을 사용하였다.

* Visualize.py -> 그림을 그려준다.

# Sculpture-GAN
3D DCGAN inspired GAN trained on 32x32x32 voxelizations of [Thingi10k](https://ten-thousand-models.appspot.com/) - a corpus of 10,000 3D printable objects and sculptures - as a result, the generated sculptures are almost always 3D-printable, but usually do not have any real 'meaning', and are just abstract sorts of shapes.

I originally began this project as an attempt at generative architecture; but lack of an appropriate dataset held me back from that. Currently working with trying to get something usable from the google sketchup 3d workshop

# Example abstract shape generations

## 3D-printed generation

![1](images/3dprinted.jpg?raw=true)

## Computer visualized generations

![1](images/snapshot10.png?raw=true)
![2](images/snapshot6.png?raw=true)
![3](images/snapshot13.png?raw=true)



# Usage

There are really only 3 files you need to use to generate your own 3D shapes.

## generate_dataset.py

You need to download [Thingi10k](https://ten-thousand-models.appspot.com/), and in line 8 of generate_dataset.py, set the variable `path_to_dataset` to be the path to your `raw_meshes` folder from your thingi10k download.

Next, just run the file with `python generate_dataset.py`, and it will start generating numpy arrays that contain all of the  now-voxelized models in thingi10k and save them to your `data/` folder.

## train.py

On line 23 of `train.py`, point it to the desired (usually the largest) .npy file in your `data/` folder by setting `numpy_array_saved` equal to its path.

Then, you can just run `python train.py` and trained network checkpoints will start to populate your `network_checkpoints/` folder.

## visualize.py

Point `visualize.py` to an array of generations in your `generations` folder (an array is created every 50 epochs) by setting `array_to_visualize` equal to its path. 

This script will allow you to see the models that network has generated in 3D, with the option to save as PNG, obj, etc.

# Issues / Future efforts

Right now, the main issue is the fact that it's very hard to get data for this sort of project; the only two datasets I have encountered are shapnet and thingi10k; currently; i am trying to train a conditional version of the 3d GAN with shapenet so that you can select that you want to generate a table, chair, etc, and the network will move past just generating "shapes"...

