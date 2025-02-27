# Mixture of Experts for materials science

## Dependencies

This package requires:
- PyTorch
- pymatgen

It has been tested with python==3.8, pytorch==1.10.1 and pymatgen==2022.3.29. See
below for example installation.

```
conda create -n moe python==3.8

conda activate moe

conda install pytorch==1.10.1 torchvision==0.11.2 torchaudio==0.10.1 cudatoolkit=11.3 -c pytorch -c conda-forge

conda install --channel conda-forge pymatgen=2022.3.29
```

## Usage
For conducting baseline experiments with single-task learning, see 
`main_singletask.py`. As an example, single-task learning on experimental 
formation energies can be executed as:

```
python main_singletask.py --property_to_train expt_eform --seed 0 --path_to_partition_indices data/matminer/saved_partition_indices/all_task_partition_indices_seed0.pkl --train_ratio 0.7 --val_ratio 0.15 --test_ratio 0.15 --h_fea_len 32
```

To run the mixture of experts or transfer learning code, see `main.py`. As an 
example, transfer learning from an extractor pre-trained on Materials Project 
formation energies to experimental formation energies can be executed as:

```
python main.py --option pairwise_TL --dataset_name expt_eform --extractor_name mp_eform
```

Mixture of experts with k=4 gated extractors on experimental formation energies can 
be executed as:

```
python main.py --dataset_name expt_eform --option add_k --use_all_extractors --k_extractor_gating 4
```

## Pre-training data
For datasets used during extractor pre-training, see
https://drive.google.com/drive/folders/1lPphRgFheI7vhUGKZXR6acWcC59tVo5w?usp=sharing

