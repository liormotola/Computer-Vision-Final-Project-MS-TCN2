# Computer-vision - Final Project
## Goal
Suggest a modification to MSTCN++ aiming to improve performances of gesture recognition task over specific data of physicians performing practice surgery operations.<br>

## Description
<ul>
  <li> Used MSTCN++ pytorch implementation (https://github.com/sj-li/MS-TCN2) of the paper [MS-TCN++: Multi-Stage Temporal Convolutional Network for Action Segmentation](https://arxiv.org/pdf/2006.09220.pdf) to perform gesture recognition over data of physicians performing surgical activity as baseline results. </li>
  <li> Implementation of modifications to the original architecture such as weighted loss, adding GRU stages and performing down sampling.</li>
  <li> Reporting evaluation metrics.</li>
  <li> Tagging videos.</li>
 </ul>

## How to run?
#### Prepare environment
1. Clone this project
2. pip/conda install the requirments.txt file

### Reproduce results
#### main.py
The file which does all of the heavy lifting is `main.py`. <br>
`main.py` is responsible for running the baseline and modified architectures, performing gesture recognition over the data videos. It also reports loss and accuracy over train and validation sets and generates graphs in clearML. <br>


The script assumes the following paths:
1. labels are provided in a directory with the absolute path `/datashare/APAS/transcriptions_gestures/` where each video has a corresponding text file with the same name as the video, holding the ground truth labels in the following frame format:

```
0 524 G0
525 662 G1
663 808 G2
809 898 G3
899 970 G4
```

2. The video features are provided in the absolute path `/datashare/APAS/features/` where the directory tree is the following:
```
root
|->fold0
|->fold1
|->fold2
|->fold3
|->fold4
```
and each fold folder contains all the features of all the videos.

3. The Cross validation splitting methods are provided in the absolute path `/datashare/APAS/folds/` where the directory tree is the following:

```
root
|->valid 0
|->valid 1
|->valid 2
|->valid 3
|->valid 4
|->test 0
|->test 1
|->test 2
|->test 3
|->test 4
```
each text file contains list of videos relevant to its own fold.


##### Runing the model:
To reproduce the results use the following commands:

1. To get baseline results run:
```
main.py --action baseline 
```
2. To train the new architecture (our modification) run:
```
main.py --action train
```
3. To run the tradeoff experiment run:
```
main.py --action train_tradeoff
```
All the above commands include performing prediction over the test data.

#### test_analysis.py
This script assumes the same dir structure as `main.py` and outputs all of the metrics described in the report such as Accuracy, F1 and Edit Score over the test data (assumes predictions were already generated).
Additionally, this scripts plots segmentation plots and metric graphs.

#### video_creator.py
This script was used to annotate videos with the ground truth labels and their predicted labels.

### Annotated videos:
This git also includes 3 anotated videos (mp4 files). Those videos were annotated using our final trained model.
