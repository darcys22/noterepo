https://www.runpod.io

setup a network volume, it will be available under `/workspace`

First thing change the huggingface cache directory to live in workspace. Otherwise it will fill ~/.cache/huggingface
```
$ export HF_DATASETS_CACHE="/workspace/huggingface/datasets"
```
