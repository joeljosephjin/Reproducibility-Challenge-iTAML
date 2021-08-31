# Reproducibility Challenge: iTAML ( An Incremental Task-Agnostic Meta-learning Approach )
Implementation of "iTAML : An Incremental Task-Agnostic Meta-learning Approach". (CVPR 2020) [(paper link)](https://arxiv.org/abs/2003.11652) for the Reproducibility Challenge 2021.

Read the Reproducibility Report at Weights and Biases [here](https://wandb.ai/joeljosephjin/itaml/reports/iTAML-An-Incremental-Task-Agnostic-Meta-learning-Approach--Vmlldzo4OTY3NDM).

iTAML : An Incremental Task-Agnostic Meta-learning Approach (accepted at IEEE Conference on Computer Vision and Pattern Recognition, Seattle, Washington, 2020), hypothesizes that generalization is a key factor for continual learning. In this pursuit, we learn a set of generalized parameters, that are neither specific to old nor new tasks by introducing a novel meta-learning approach that seeks to maintain an equilibrium between all the encountered tasks. This is ensured by a task-agnostic meta-update rule which avoids catastrophic forgetting. When presented with a continuum of data, our model automatically identifies the task and quickly adapts to it with just a single update. 

This code provides an implementation for iTAML. This repository is implemented using PyTorch and it includes code for running the incremental learning domain experiments on MNIST, SVHN, CIFAR100, ImageNet, and MS-Celeb-10K datasets.

<p align="center"><img src="./utils/figs/front.png" width="400"></p>
<p align="center">(a) iTAML overall learning process</p>

### Dependencies
This code requires the following:
* matplotlib==3.2.1
* numpy==1.18.2
* pandas==1.0.3
* Pillow==7.0.0
* scipy==1.4.1
* torch==1.4.0
* torchvision==0.5.0
* wandb==0.12.1

run `pip3 install -r requirements.txt` to install all the dependencies. 

### Data
All the dataloading is handled at `incremental_dataloader.py` and the experimental setting for the datasets are handled at `args` class in `train_<dataset>.py`. `args` class contains all the hyper-parameters settings to run the experiment. For example, consider the following:
   
 ``` 
class args:
    dataset = "cifar100"
    checkpoint = "results/cifar100/test1"
    savepoint = "models/" + "/".join(checkpoint.split("/")[1:])
    data_path = "../Datasets/CIFAR100/"
    
    num_class = 100
    class_per_task = 10
    num_task = 10

    memory = 2000
    beta = 1
    r = 1
    .
    .
```
Here, `dataset` can be set to the following:
- "cifar100"
- "cub200"
- "imagenet"
- "celeb"
- "mnist"
- "svhn"

`checkpoint` and `savepoint` saves the records of performance and trained models, respectively. `data_path` points to the location of the dataset downloaded, if it is not downloaded previously, the script will download and extract at the pointed location. As mentioned in our paper, each dataset can be run with different class incremental settings, hence the total number of classes included in the experiment, number of classes assigned per each task and the total number of tasks are defined at `num_class`,  `class_per_task`, and `num_task`. Also, `memory` is the upper bound for the number of exemplars. Further, `beta` is the decay-rate, which controls the amount of fusion between old parameters and current parameters and `r` is the number of inner loop updates.
    
### Usage
To run the experiment, run `CUDA_VISIBLE_DEVICES=0 python3 train_cifar.py [x]`. Here `[x]` is a system argument of the starting task id. begins with `0`.

### Results

We perform extensive experiments on five datasets in a class-incremental setting, leading to significant improvements over the state of the art methods (e.g.,a  21.3%  boost on  CIFAR100  with  10  incremental tasks). Specifically, on large-scale datasets  that generally prove difficult cases for incremental learning, our approach delivers absolute gains as high as 19.1% and 7.4% on ImageNetand MS-Celeb datasets, respectively.

<p align="center"><img src="./utils/figs/results3.png" width="800"></p>
<p align="center">(b) iTAML performance on CIFAR100 with class incremental setting of 5,10,20 classes per task respectivly.</p>
<br/>
<br/>
<p align="center"><img src="./utils/figs/results.png" width="800"></p>
<p align="center">(c) iTAML performance on ImageNet-100, ImageNet-1K and MS-Celeb-10K.</p>


### We Credit
Thanks to https://github.com/khurramjaved96/incremental-learning, for the preliminary implementation of the data loader.

### Contact
Jathushan Rajasegaran - jathushan.rajasegaran@inceptioniai.org or brjathu@gmail.com
<br/>
To ask questions or report issues, please open an issue on the [issues tracker](https://github.com/brjathu/iTAML/issues).
<br/>
Discussions, suggestions and questions are welcome!


## Citation
```
@article{rajasegaran2020itaml,
  title={iTAML : An Incremental Task-Agnostic Meta-learning Approach},
  author={Rajasegaran, Jathushan and Khan, Salman and Hayat, Munawar and Khan, Fahad Shahbaz and Shah, Mubarak},
  journal={The IEEE Conference on Computer Vision and Pattern Recognition (CVPR)},
  month = {June},
  year = {2020}
}
```
