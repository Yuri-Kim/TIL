# torch-geometric  



docker 환경에서 사용하기  



```
$ docker pull pytorch/pytorch:1.4-cuda10.1-cudnn7-devel

$ docker run --runtime=nvidia -e NVIDIA_VISIBLE_DEVICES=$number --volume ~/workspace:/workspace -it --name yuri_torch pytorch/pytorch:1.4-cuda10.1-cudnn7-devel  

$ nvcc --version  
$ python -c "import torch; print(torch.__version__)"  
$ python -c "import torch; print(torch.cuda.is_available())"  
$ pip install torch-scatter==latest+cu101 torch-sparse==latest+cu101 -f https://s3.eu-central-1.amazonaws.com/pytorch-geometric.com/whl/torch-1.4.0.html  

$ pip install torch-cluster  
$ pip install torch-geometric  
```

