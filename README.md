# CMSF
This is the Pytorch implementation of our ICDE'23 paper: **A Contextual Master-Slave Framework on Urban Region Graph for Urban Village Detection**.

## Requirements

* python 3.x
* torch == 1.7.1 
* dgl == 0.6.1

## Data
### 1. Download datasets

The three real-world datasets used in our paper can be downloaded here: 

Put all data files in dir: data/


### 2. Data description

(1) city_poi_features.npy: (num_nodes, 64) numpy array of our constructed POI features.

* poi_features[:, 0] : region id (not used)
* poi_features[:, 1] : Index of basic living facility
* poi_features[:, 2:26] : Category distribution in the given region
* poi_features[:, 26:50] : Category distribution in the 3x3 grids centered by the given region
* poi_features[:, 50:] : POI radius features

(2) city_img_features.npy: (num_nodes, 4096) numpy array of image features extracted by the VGG16 model pre-trained on ImageNet.

(3) city_labels.npy: (num_nodes, ) numpy array of ground truth binary label indicating that whether a region is urban village (y=1) or not (y=0).
* Notes: The y value for unlabeled regions are also set to 0 in this array, they will be masked when calculating the loss and evaluation metrics.

(4) city_adj.npy: (2, num_edges) array of edges of the urban region graph (URG).
* adj[0]: start nodes list of edegs
* adj[1]: end nodes list of edegs

(5) city_mask.json : the dict recording the region id in train / val / test set under each dataset split for nested cross validation.


## Model training
Set the hyper-parameters in script.sh, and train the master model by:
```
sh script.sh master train
```
Then, train the slave model based on the saved master model by:
```
sh script.sh slave train
```
## Inference
Make urban village prediction with the trained slave model by:
```
sh script.sh slave test
```

## Paper Download
Please refer to the full version: 

## Reference
Please cite our work if you find our data/code/paper is useful to your work:
