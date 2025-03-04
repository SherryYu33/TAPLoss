# TAPLoss

Official Pytorch Implementation of [TAPLoss: A Temporal Acoustic Parameter Loss For Speech Enhancement](https://arxiv.org/abs/2302.08088) accepted to ICASSP 2023. 

## Prerequisites

TAPLoss requires **Numpy** and **Pytorch**, install versions that are compatible with your project. Refer to [Demucs](Demucs/denoiser/README.md) and [FullSubNet](FullSubNet/README.md) for installing required packages for **Demucs** and **FullSubNet**.

## Dataset

The TAP esimator is trained on the **DNS 2020** dataset. Download the DNS Interspeech 2020 dataset from [here](https://github.com/microsoft/DNS-Challenge/tree/interspeech2020/master) and follow the instructions to prepare the dataset.

## Temporal Acoustic Parameters

Ground truth temporal acoustic parameters are calculated using [Opensmile](https://audeering.github.io/opensmile-python/usage.html). The 25 temporal acoustic parameters include:

- Loudness_sma3
- alphaRatio_sma3
- hammarbergIndex_sma3
- slope0-500_sma3
- slope500-1500_sma3
- spectralFlux_sma3
- mfcc1_sma3
- mfcc2_sma3
- mfcc3_sma3
- mfcc4_sma3
- F0semitoneFrom27.5Hz_sma3nz
- jitterLocal_sma3nz
- shimmerLocaldB_sma3nz  
- HNRdBACF_sma3nz  
- logRelF0-H1-H2_sma3nz  
- logRelF0-H1-A3_sma3nz  
- F1frequency_sma3nz   
- F1bandwidth_sma3nz  
- F1amplitudeLogRelF0_sma3nz  
- F2frequency_sma3nz  
- F2bandwidth_sma3nz  
- F2amplitudeLogRelF0_sma3nz  
- F3frequency_sma3nz  
- F3bandwidth_sma3nz  
- F3amplitudeLogRelF0_sma3nz 


## Use TAPLoss in your own project

1. You'll need the  `TAPLoss.py` and `TAP_estimator.py` located under `TAPLoss/`, you'll also find a `.pt` file under the same directory, which is the pretrained TAP estimator model checkpoint.
```python
from TAPLoss import AcousticLoss
```
2. Initialize TAPLoss 
```python
TAPloss = AcousticLoss(loss_type, acoustic_model_path, paap, paap_weight_path)
# loss_type: choose one from ["l2", "l1", "frame_energy_weighted_l2", "frame_energy_weighted_l1"]
# acoustic_model_path: path to the .pt TAP pretrained estimator model checkpoint.
# paap: set to True if you want to use Paaploss, default is False.
# paap_weight_path: path to the paap weights .npy file, must specify if paap == True.
```
3. Call TAPloss as a function
```python
loss = TAPloss(clean_waveform, enhan_waveform, mode)
# clean_waveform: waveform of clean audio, sampled at 16khz.
# enhan_waveform: waveform of enhanced audio, sampled at 16khz.
# mode: "train" if your enhancement model is in train mode,
#        "eval" if your enhancement model is in eval mode,
#        gradients won't be calculated in eval mode.
```

## Related Resources

More details about the official implementation of [PAAPLoss: A Phonetic-Aligned Acoustic Parameter Loss for Speech Enhancement](https://arxiv.org/abs/2302.08095) can be found at https://github.com/muqiaoy/PAAP. 

## Citation

Please cite our paper if you use this code for your research.
```
@article{zeng2023taploss,
  title={TAPLoss: A Temporal Acoustic Parameter Loss for Speech Enhancement},
  author={Zeng, Yunyang and Konan, Joseph and Han, Shuo and Bick, David and Yang, Muqiao and Kumar, Anurag and Watanabe, Shinji and Raj, Bhiksha},
  journal={arXiv preprint arXiv:2302.08088},
  year={2023}
```
