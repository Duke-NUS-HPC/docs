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

  ![image-20220301140057333](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/69e597f3-bf30-4ef4-93f9-e3184df9e932/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220301%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220301T085355Z&X-Amz-Expires=86400&X-Amz-Signature=463a2ee2c7b88647a2f3eec640cb62871e7597053342ab8cc189aee1ab573aa2&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

- open a new Notebook

- change the kernel (example: kernel name is 'mypy38')

  ![image](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/34212fe7-688d-4d67-a0ef-e8527312dc47/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220301%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220301T060337Z&X-Amz-Expires=86400&X-Amz-Signature=2756a7c6aeedca43e92345e67f817562393e66dbea834c36341817467cd3c8a7&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

![image2](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c797389c-3d5f-4031-a13d-474b28443566/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220301%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220301T060418Z&X-Amz-Expires=86400&X-Amz-Signature=5972545845e6b0fd9c3c6aaffee29d2289cf1190d7673466ca6fa40042f3253f&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

- you will be using your customized conda environment within jupyter notebook
