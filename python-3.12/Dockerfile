# using rhels images, can change to any base image
FROM registry.redhat.io/ubi9:latest

USER root

WORKDIR /app

# uncomment and update 'course_repo_directory' below if using
# with a course repository that has a defined 'requirements.txt'
# file.

# COPY course_repo_directory/requirements.txt /tmp/.

RUN dnf install -y python3.12 && \
    dnf install -y python3.12-pip && \
    dnf install -y python3.12-requests && \
    dnf install -y python3.12-Cython && \
    dnf install -y java-17-openjdk && \
    alternatives --install /usr/bin/python python $(which python3.12) 10 && \
    alternatives --install /usr/bin/python python $(which python3.12) 20 && \
    alternatives --install /usr/bin/pip pip $(which pip3.12) 10 && \
    alternatives --set python $(which python3.12) && \
    dnf clean all

RUN python -m venv /tmp/.venv && \
    source /tmp/.venv/bin/activate && \
    python -m pip install --upgrade pip && \
    pip install -r /tmp/requirements.txt && \
    pip install ipykernel && \
    python -m ipykernel install --user --name=.venv

EXPOSE 8888 54321

# Start Jupyter Lab
CMD ["/bin/bash", "-c", "source /tmp/.venv/bin/activate && jupyter lab --ip=0.0.0.0 --port=8888 --no-browser --allow-root"]