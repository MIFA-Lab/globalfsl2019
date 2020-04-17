## Few-Shot Learning with Global Class Representations
Created by <a href="https://tiangeluo.github.io/" target="_blank">Tiange Luo*</a>, <a href="" target="_black">Aoxue Li*</a>, <a href="http://personal.ee.surrey.ac.uk/Personal/T.Xiang/index.html" target="_blank">Tao Xiang</a>, <a href="https://www.weiranhuang.com" target="_blank">Weiran Huang</a> and <a href="http://www.liweiwang-pku.com" target="_blank">Liwei Wang</a>

![Overview](https://github.com/huang-paper-code/fsl-global/blob/master/material/overview.png)

## About this repository
This is the repository for our ICCV 2019 [paper](https://www.weiranhuang.com/publications/GlobalRepresentation-ICCV19.pdf). In this paper, we propose to tackle the challenging few-shot learning (FSL) problem by learning global class representations for each class via involving both base and novel classes training samples from the beginning. For more details of our framework, please refer to our [paper](https://www.weiranhuang.com/publications/GlobalRepresentation-ICCV19.pdf) or <a href="https://zhuanlan.zhihu.com/p/78743300" target="_blank">知乎</a>.

Due to company and patent issues, the authors only release the codes of the proposed module. If you want to run those codes, you need to implement and train the hallucinator [Low-shot learning from imaginary data].

## Generalized FSL in the paper
The generalized FSL test way proposed in the paper is highly similar to the typical 5-way-5-shot FSL. The only difference is that we would do a **all-way** classification (100-way in section 4.2.1, 120-way classification in section 4.3.2). We set three types of evaluation. Please refer to section 4.2.1, in each episode, we will sample 5 classes from base classes (acc_b), novel classes (acc_n), or all classes (acc_a). Then, sampling 5 shots from each class. Finally, for all three types, we will do a all-way classification.

In section 4.2.1, follow the class splits as the original miniImageNet, we use the validation set to tune hyper-parameters, use both the training and validation sets as the base classes (80), and use the test set as the novel classes (20). In section 4.3.2, we still use the original training and validation sets as the base classes (80), but use the test set and the new added 20 classes as the novel classes (40).

## Usage

- convnet.py: the network for extracting feature and registrating.
- train_100way.py: train the model on the 100-way setting.
- test_100way.py: test in generalized FSL setting described in section 4.2.1.
- samplers.py: code for sampling data in a 5-way-5-shot manner.
- csv: dataset splits.

## Results
1. Standard few-shot learning on miniImageNet (5-way accuracy)

| **Model** | **1-shot** | **5-shot** |
|:-----:|:------:|:------:|
|MLSTM [21]     |43.44 ± 0.77| 60.60 ± 0.71|
|MN [34]        |43.56 ± 0.84| 55.31 ± 0.73|
|MA [9]         |48.70 ± 1.84| 63.11 ± 0.92|
|PN [29]        |49.42 ± 0.78| 68.20 ± 0.66|
|DLM [33]       |50.28 ± 0.80| 63.70 ± 0.70|
|RN [30]        |50.44 ± 0.82| 65.32 ± 0.70|
|MG [36]        |52.71 ± 0.64| 68.63 ± 0.67|
|MMN [3]        |**53.37** ± 0.48| 66.97 ± 0.35|
|**GCR (Ours)** |53.21 ± 0.40| **72.34** ± 0.32|

2. Generalized few-shot learning on miniImageNet 

| **Model** | **acc_a** | **acc_b** | **acc_n** |
|:-----:|:-----:|:-----:|:-----:|
|MN [34]        |26.98| 33.54| 0.75|
|PN [29]        |31.17| 39.53| 0.52|
|RN [30]        |32.48| 40.24| 1.42|
|**GCR (Ours)** |**39.14**| **46.32**| **12.98**|

1) acc_b: the accuracy of classifying the data samples from the base
classes to all the classes (both base and novel); 
2) acc_n: the accuracy of classifying the data samples from the novel
classes to all the classes; 
3) acc_a: the accuracy of classifying the all test samples to all the classes.

## Citation
If you find our work useful in your research, please consider citing:

        @InProceedings{Li_2019_ICCV,
            author = {Li, Aoxue and Luo, Tiange and Xiang, Tao and Huang, Weiran and Wang, Liwei},
            title = {Few-Shot Learning With Global Class Representations},
            booktitle = {The IEEE International Conference on Computer Vision (ICCV)},
            month = {October},
            year = {2019}
        }
