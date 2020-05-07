# Deep Learning Experiment Toolkit
Provides infrastructure to help you set up deep learning experiments in a second so that you focus on implementing your own idea.  
_Acknowledgement:_ This toolkit is mainly adapted and modified from https://github.com/tribhuvanesh/knockoffnets/tree/master/knockoff

### Usage & Explanations
- _config.py_: Configuration file for setting:
    - Random seed
    - Default path for datasets, model zoo, etc.
    - Default parameters (i.g. mean and std of a dataset)
    
- _model_utils.py_: Training and evaluation functions that are capable to:
    - Create log file for training and testing
    - Create informative checkpoint. 
    - Checkpoint struction:
        - epoch
        - arch
        - state_dict
        - best_test_acc
        - optimizer
        - created_on
    
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

```
# Load model checkpoint
checkpoint = torch.load(model_path)
start_epoch = checkpoint["epoch"]
best_test_acc = checkpoint["best_acc"]
model.load_state_dict(checkpoint["state_dict"])
optimizer.load_state_dict(checkpoint["optimizer"])
```