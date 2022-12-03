# Start with a Linux micro-container to keep the image tiny
# FROM alpine:3.7
FROM ubuntu

#Modified
# Document who is responsible for this image
MAINTAINER Wayne Zhu "jz3395@nyu.edu"

# Install just the Python runtime (no dev)
# Linux uses apt-get instead of brew
RUN apt-get update && apt-get install -y \
    #install compiler for c and fortran
    python3 python3-dev gcc gfortran musl-dev \
    #provides certificate authority
    python3-pip ca-certificates

# Set up a working folder and install the pre-reqs
WORKDIR /app
ADD mnist/requirements.txt /app
RUN pip3 install --upgrade pip setuptools 
RUN pip3 install -r requirements.txt
# RUN pip3 install torch
# RUN pip3 install torchvision
# RUN pip3 install torch===1.8.0+cpu torchvision===0.9.0+cpu -f https://download.pytorch.org/whl/torch_stable.html

# Add the code as the last Docker layer because it changes the most
#This is related to the layered structure of Docker that we learned in class.
ADD mnist/main.py  /app/main.py

# Run the service
WORKDIR /app
#There can only be one CMD instruction in Dockerfile.
#If listed multiple only the last one will take effect.
CMD [ "python3", "main.py", "--dry-run" ]
#The no-cude run takes a long time.
CMD [ "python3", "main.py", "--no-cuda"]
#This is similar to no-cuda
CMD [ "python3", "main.py", "--no-mps"]

CMD [ "python3", "main.py", "--batch-size=128", "--epochs=1","--save-model"]
#Similarly, we can change the training and testing batchsize, epochs, learning rate.
#But they all take a long time compared to --dry-run, so I am not training all of them here.


