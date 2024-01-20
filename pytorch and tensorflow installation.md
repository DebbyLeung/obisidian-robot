# Driver installation

[Official Drivers | NVIDIA](https://www.nvidia.com/Download/index.aspx?lang=en-us)
# Cuda toolkit
[CUDA Toolkit 12.3 Update 1 Downloads | NVIDIA Developer](https://developer.nvidia.com/cuda-downloads?target_os=Windows&target_arch=x86_64&target_version=11&target_type=exe_network)
## Checking
```
nvidi-smi
```
# Pytorch_local
[Start Locally | PyTorch](https://pytorch.org/get-started/locally/)
download from pytorch and nvidia channels
```
pip install chardet
conda install chardet pytorch torchvision torchaudio pytorch-cuda=12.1 -c pytorch -c nvidia
```

## Checking
```
import torch
torch.cuda.is_available()
```

# Tensorflow_local
```
conda install tensorflow-gpu cudatoolkit=12.1.0
```