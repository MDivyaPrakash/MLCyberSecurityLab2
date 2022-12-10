# Lab 2 - Backdoor Model Detector : Pruning Defense Implementation.
To implement the code below directory structure is to be followed and the Google Colab file can be placed in the main folder.

```bash
├── data 
    └── cl
        └── valid.h5 // This is clean validation data used to design the defense
        └── test.h5  // This is clean test data used to evaluate the BadNet
    └── bd
        └── bd_valid.h5 // This is sunglasses poisoned validation data
        └── bd_test.h5  // This is sunglasses poisoned test data
├── models
    └── bd_net.h5
    └── bd_weights.h5
├── dm5309_MLCyberSec_Lab2.ipynb // This contains the experiments implemented and results obtained.
├── architecture.py
└── eval.py // this is the evaluation script
```

## Dataset Retrieval:

   1. Download the validation and test datasets from [here](https://drive.google.com/drive/folders/1Rs68uH8Xqa4j6UxG53wzD0uyI8347dSq?usp=sharing) and store them under `data/` directory.
   2. The dataset contains images from YouTube Aligned Face Dataset. We retrieve 1283 individuals and split into validation and test datasets.
   3. bd_valid.h5 and bd_test.h5 contains validation and test images with sunglasses trigger respectively, that activates the backdoor for bd_net.h5
   

## Notes

The Google drive link where the experiments were implemented is [here](https://drive.google.com/drive/folders/1GBAnKo04gTphDUpSpkQC7vQn-QICxfV7?usp=sharing).
 
Note :As mentioned in the reference Colab File, the Keras prevents from saving this kind of sub-classed model as HDF5 file since it is not serializable. So, the repaired model was directly used, for the evaluation,  instead of storing and retrieving. However, the Bprime weights are saved in the models folder in the attached in this repository.

## Running the Evaluation Script
As mentioned above we cannot directly store the weights of the repaired model. However, we can construct the repaired model and use it for evaluation.
The backdoor model with defense implemented can be by executing the below command:
```
python3 eval.py <path_to_clean_data_file> <path_to_poison_data_file>  <path_to_orginal_BadnetWeights> <path_to_BPrimeWeights>

```
For example, in the above directory structure if the Bprime2 has to be evaluated, the command would be
```
python3 eval.py data/<path_to_clean_data_file> data/<path_to_poison_data_file>  /models/bd_net.h5  /models/B_prime_10p.h5

```

