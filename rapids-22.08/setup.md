# Rapids-22.08

This tutorial works for Ubuntu and Debian. It might also work for other linux distributions. Please install all packages in the excat order because it might otherwise brake the enviroment.

## Create Conda enviroment
to create the rapids base enviroment in the default location

```
conda create -n rapids-22.08 -c rapidsai -c nvidia -c conda-forge  \
    rapids=22.08 python=3.9 cudatoolkit=11.5 cudnn cutensor cusparselt leidenalg louvain fa2 
```
If you want to create the enviroment in a specific folder (like on a server) use the `-p` flag
```
conda create -p ~/conda/rapids-22.08 -c rapidsai -c nvidia -c conda-forge  \
    rapids=22.08 python=3.9 cudatoolkit=11.5 cudnn cutensor cusparselt leidenalg louvain fa2 
```
The enviroment setup may take a while.

## Install the single cell packages
First activate your enviroment
```
conda activate rapids-22.08
```
or
```
conda activate ~/conda/rapids-22.08
```
Than install the base single cell packages with pip
```
pip install scanpy muon mofax mofapy2 scirpy decoupler squidpy scfates scikit-misc
```
Then install the needed deep learning libraries for scvi-tools.
Here we install pytorch for cuda version 11.6 you can also install it for version 11.3
```
pip install --upgrade "jax[cuda]" -f https://storage.googleapis.com/jax-releases/jax_cuda_releases.html
pip install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu116
```
Now we can install scvi-tools and pyMDE. This will result in some errors. Protobuf 3.20.1 works with all packages. So we have to manually reinstall that and force this specific version.
```
pip install scvi-tools
pip install protobuf==3.20.1
pip install pymde
```
Now we can install rapids_singlecell. rapids_singlecell lets you run scRNA Analysis on the GPU, while beeing compatible with scanpy.
For the newest version check the [git](https://github.com/Intron7/rapids_singlecell)
```
pip install https://github.com/Intron7/rapids_singlecell/releases/download/v0.2.1/rapids_singlecell-0.2.1-py3-none-any.whl
```

## Set Jupyter Lab
If you want to start jupter lab from this enviroment. You have to install it:
```
pip install jupyterlab
```
If you just want the Kernel to be accsesble from a different Jupyter Notebook server or Jupyter Hub just install the kernel
```
ipython kernel install --user --name=rapids-22.08
```
You can than start your Jupyter and you should be able to select the rapids-22.08 kernel.


