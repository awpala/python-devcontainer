# Use the miniconda3 image as the base
FROM continuumio/miniconda3

# Set values for environment variables
ARG PYTHON_VERSION=3.10
ARG CONDA_ENV_NAME=dev

# Update the package list and install necessary packages
RUN apt-get update && apt-get install -y \
    curl \
    git \
    && rm -rf /var/lib/apt/lists/*

# Create a new conda environment with the specified name and install the dependencies from the requirements.txt file
COPY requirements.txt /tmp/requirements.txt
RUN conda create --name ${CONDA_ENV_NAME} python=${PYTHON_VERSION} --file /tmp/requirements.txt

# Activate the environment and ensure conda is available in all terminals
RUN echo "conda activate ${CONDA_ENV_NAME}" >> ~/.bashrc

# Add alias `jn` for Jupyter Notebook
RUN echo "alias jn='jupyter notebook --ip 0.0.0.0 --port 8888 --no-browser --allow-root --notebook-dir=/home/dev-files'" >> ~/.bashrc

# Ensure the conda environment is on the PATH
ENV PATH /opt/conda/envs/${CONDA_ENV_NAME}/bin:$PATH

# Set the default notebook directory to /opt/notebooks
WORKDIR /home/dev-files

# Set the default shell to bash
SHELL ["/bin/bash", "--login", "-c"]

# Set the container name when running the container
CMD ["--name", "python-dev-env"]
