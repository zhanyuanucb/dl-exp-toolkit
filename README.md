# Deep Learning Experiment Toolkit
Tools helping you set up deep learning experiments in a second

### Usage & Explanations
- _config.py_: Configuration file for setting:
    - Random seed
    - Default path for datasets, model zoo, etc.
    - Default parameters (i.g. mean and std of a dataset)
    
- _model_utils.py_: Training and evaluation functions that are capable to:
    - Create log file for training and testing
    - Create informative checkpoint
    
- _datasets_: Manage all the datasets and corresponding default transformations durint training and testing. Current available datasets:
    - MNIST
    - CIFAR10
    - ImageNet
    
- _modelzoo_: Manage all the models trained on different datasets. Current available datasets:
    - MNIST
    - CIFAR10
    - ImageNet
    
    
### Example

```
import modelzoo.zoo as zoo
import datasets
import config as cfg

params = {"model_name":"resnet50",
          "dataset_name":"ImageNet1k", # CIFAR10 or MNIST
          "num_classes":1000,
          "pretrained":"imagenet"}
```

```
# Load model
model_name = params["model_name"]
dataset_name = params["dataset_name"]
modelfamily = datasets.dataset_to_modelfamily[dataset_name]
num_classes = params["num_classes"]
pretrained = params["pretrained"]
model = zoo.get_net(model_name, modelfamily, num_classes=num_classes, pretrained=pretrained)

```

```
# Load dataset

modelfamily = datasets.dataset_to_modelfamily[dataset_name]
dataset = datasets.__dict__[dataset_name]

```