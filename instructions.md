The following are instructions on how to use this repository to run LlaMa-Factory in  a docker container ans finetune a local model with a custom dataset.

Pre-requisites
- NVIDIA GPUs
- NVIDIA GPU drivers
- Docker
- Docker Desktop
- Linux distro in WSL2 (We used Ubuntu-22.04 LTS)

Step - 1 (Installing NVIDIA Dependencies)
  Install the Nvidia Container Toolkit in the Linux distro. Follow [these instructions](https://medium.com/@u.mele.coding/a-beginners-guide-to-nvidia-container-toolkit-on-docker-92b645f92006) to install it. Use the latest NVIDIA CUDA *base-ubuntu20.04* image from [NVIDIA's Docker hub repository](https://medium.com/@u.mele.coding/a-beginners-guide-to-nvidia-container-toolkit-on-docker-92b645f92006) in the verification step.

Step 2 (Loading local LLM model)
  Create a _models_ folder in the root directory and copy the LLM model folder inside _models_

Step-3 (Loading custom/local fine-tuning dataset)
  - Copy the dataset JSON into [_data_](./data).
  - Add your dataset in dataset_info.json with the file name and the SHA1 encription hex code. Refer to the instructions [here](https://www.howtohaven.com/system/how-to-hash-file-on-windows.shtml). Be sure to follow the key naming conventions in the json file. For more detailed instruction on how to format your entry into _dataset_info.json_, refer to [this document](./data/README.md).

Step-4 (configure docker desktop)
  In Docker Desktop go to Settings>General and make sure *Use the WSL@ based engine* is checked.
  Then go to Settings>Resources>WSL Integration and select the Linux distro with NVIDIA Container Toolkit and the CUDA image.

Step-5 (the container)
Open the cli (powershell or cmd) and `cd` into the root of this repository and use `docker-compose up -d` to create the docker container.

Step-6 (start the fine-tune)
  Open another terminal window and use `docker ps` to find the details of the image that is running in the container im the previous page, then execute `docker exec -it <name_of_image> /bin/bash` to open an interractive shell in that image, then execute one of the commands from [here](./examples/custom_commands/) to begin the finetune process
