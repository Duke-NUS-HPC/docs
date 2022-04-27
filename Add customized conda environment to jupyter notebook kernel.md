# Add customized conda environment to jupyter notebook kernel

- On login node `login-10-03 ` build a conda environment, example here showed an environment for python version 3.8

  `(bash)$ conda create --name <your_env> python=3.8`

- activate conda environment

  `(bash)$ conda activate <your_env>`

- install packages for your need via `pip` or `conda`

- install jupyter notebook within your environment

  `(your_env)$ pip install jupyter`

  or

  `(your_env)$ conda install jupyter`

- add your conda environment as python kernel, `<env_name>`can be the same or be different from your name of the environment

  `(your_env)$ ipython kernel install --name <env_name> --user`

- On DUKE-NUS HPC dashboard, select Jupyter notebook and select the resources you need

  ![image-20220301140057333](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/69e597f3-bf30-4ef4-93f9-e3184df9e932/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220427%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220427T101217Z&X-Amz-Expires=86400&X-Amz-Signature=42a2a30649daa8edbab1e6b94f348719ee5da73e3444f1effec9b9ab67877bee&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

- open a new Notebook

- change the kernel (example: kernel name is 'mypy38')

  ![image](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/34212fe7-688d-4d67-a0ef-e8527312dc47/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220427%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220427T101238Z&X-Amz-Expires=86400&X-Amz-Signature=ac1bbb3ec95b1b6f8cbc27833bed258792ce1149fe02aa51051f218857acfbb1&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

![image2](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c797389c-3d5f-4031-a13d-474b28443566/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220427%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220427T101257Z&X-Amz-Expires=86400&X-Amz-Signature=a1875e56ef51708fbc680eb9f3713da1d61a6f0afc481fa8a2319a79a2e6dec0&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

- you will be using your customized conda environment within jupyter notebook
