## Requirements.

```bash
python 3.10
conda install pytorch==2.1.0 torchvision==0.16.0 torchaudio==2.1.0 pytorch-cuda=11.8 -c pytorch -c nvidia
pip install deepspeed==0.10.3
pip install six
pip install regex
wget https://developer.download.nvidia.com/compute/cuda/11.8.0/local_installers/cuda_11.8.0_520.61.05_linux.run
sh cuda_11.8.0_520.61.05_linux.run --toolkit --toolkitpath=/bigtemp/qxc4fh/cuda --tmpdir=/bigtemp/qxc4fh/tmp
export PATH=/home/hshen/zeyu/cuda_11.8/bin:$PATH
export LD_LIBRARY_PATH=/home/hshen/zeyu/cuda_11.8/lib64:$LD_LIBRARY_PATH
# install NVIDIA/apex (needs cuda, may git checkout 741bdf50825a97664db085749)
git clone https://github.com/NVIDIA/apex
pip install -v --disable-pip-version-check --no-cache-dir --no-build-isolation --config-settings "--build-option=--cpp_ext" --config-settings "--build-option=--cuda_ext" ./
pip install pybind11
pip install transformers==4.23.0
pip install flash-attn --no-build-isolation
```

## Intro

The quantization code is in ./quantization

All code is in one file: sp_transformer_infer_quant.py

IPS specifies the number of servers to use, and GPUS provides the GPU ID on which each rank should work. One server can have many ranks.

On each server, run "./sp_transformer_infer_quant.py -s" to run a launcher listener. Then on the first server, run "./sp_transformer_infer_quant.py" to start the inference.

The quantization code of QKV is in Class _SeqAllTOAll.
