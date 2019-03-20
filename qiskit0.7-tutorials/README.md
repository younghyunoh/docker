## QISKIT-Tutorial  
- Qiskit v0.7 
- Python v3.5 

## Building a docker container image for [qiskit-tutorials](https://github.com/Qiskit/qiskit-tutorials)  

### 1. Donwload a pre-built qiskit-tutorial image from docker hub
$ docker pull younghyunoh/qiskit0.7-tutorials

### 2. Create a docker image for qiskit-tutorial 
#### Download **Dockerfile** and **environment.yml** to your local machine.  
$ docker build -t image_name .  
$ docker images  

### 3. Run a container from image   
- Interactive Mode      
$ docker run -it --rm --name qiskit-tutorial -p 8888:8888 younghyunoh/qiskit0.7-tutorials (or your_image_name)  
The Jupyter Notebook is running at:  
[I 18:39:51.766 NotebookApp] http://(43ef0692097b or 127.0.0.1):8888/?token=59015a0e15846de1155bdda60e3916e7d839fed2f2b2b4aa  

- Daemon Mode   
$ docker run -d --name qiskit-tutorial -p 8888:8888 younghyunoh/qiskit0.7-tutorials (or your_image_name)    
$ docker logs qiskit-tutorial     
The Jupyter Notebook is running at:      
[I 18:39:51.766 NotebookApp] http://(43ef0692097b or 127.0.0.1):8888/?token=59015a0e15846de1155bdda60e3916e7d839fed2f2b2b4aa     

#### Jupyter notebook  
- Copy the token and paste into your browser  
http://localhost:8888/?token=59015a0e15846de1155bdda60e3916e7d839fed2f2b2b4aa     
