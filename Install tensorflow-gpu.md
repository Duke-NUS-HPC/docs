# Install tensorflow-gpu

- recommend to install via **conda** only

- build a conda environment with python version ≥ 3.7

  `(bash)$ conda create --name <your_env> python=3.8`

- activate conda environment

  `(bash)$ conda activate <your_env>`

- install packages. **tensorflow-gpu** **MUST** be installed through **conda**. The following command will install `tensorflow-gpu 2.2.0` by default.

  `(your_env)$ conda install -c anaconda tensorflow-gpu`

- check if packages that support GPU are installed

  `(your_env)$ conda list | grep cud`

  should return

  ```
  cudatoolkit               10.1.243             h6bb024c_0    anaconda
  cudnn                     7.6.5                cuda10.1_0    anaconda
  ```

  - if returned nothing, enter `(your_env)$ conda list | grep tensorflow-gpu`

    - if returned:

    - ````
      tensorflow                2.2.0           gpu_py38hb782248_0    anaconda
      tensorflow-base           2.2.0           gpu_py38h83e3d50_0    anaconda
      tensorflow-estimator      2.2.0              pyh208ff02_0    anaconda
      tensorflow-gpu            2.2.0                h0d30ee6_0    anaconda
      ````

      uninstall via `conda uninstall tensorflow-gpu` and reinstall it, or enter `conda search tensorflow-gpu` to specify the version you want to install

    - if returned nothing, uninstall tensorflow via `conda uninstall tensorflow` and enter `conda search tensorflow-gpu` to specify the version you want to install

  - if supportive packages are correctly returned, ask for 1 GPU and open a jupyter notebook for your environment. Please refers to [Add customized conda environment to jupyter notebook kernel](https://github.com/Duke-NUS-HPC/docs/blob/main/Add%20customized%20conda%20environment%20to%20jupyter%20notebook%20kernel.md).

    - type `!nvidia-smi`. Should have the following results displayed.

    ![image](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/71da8b18-dfbf-4f77-9d51-2dfdfabab02a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220301%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220301T061708Z&X-Amz-Expires=86400&X-Amz-Signature=d3d0baa7ac52f7b11b73ace99d82d58ec0c5f72347ff095bf28d4166084c912e&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

- check if tensorflow can access gpu

```python
import tensorflow as tf
!jupyter kernelspec list
if not tf.config.list_physical_devices('GPU'):    
    print("No GPU was detected.")
```

![image](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2c606e3d-f99f-4b01-a456-677c9b874d98/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220301%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220301T061957Z&X-Amz-Expires=86400&X-Amz-Signature=b8febd8bb17a51cd6f5d3c953a6cc7415269047835d673454399fc91bc2612da&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

- `Adding visible gpu devices: 0` is expected. Since in python, indexing start from 0.
- For specific tensorflow-gpu version other than those listed in conda distribution and specific version of cuda toolkit support, please contact admin for installation.
