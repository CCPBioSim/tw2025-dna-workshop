# Start with BioSim base image.
ARG BASE_IMAGE=latest
FROM ghcr.io/ccpbiosim/jupyterhub-base:$BASE_IMAGE

LABEL maintainer="James Gebbie-Rayet <james.gebbie@stfc.ac.uk>"

# Switch to jovyan user.
USER $NB_USER
WORKDIR $HOME

# Install workshop deps
#RUN conda install -c acellera -c conda-forge ambertools htmd matplotlib mdtraj nglview numpy -y

RUN conda install -c acellera -c conda-forge ambertools htmd matplotlib mdtraj nglview numpy -y

# Get workshop files and move them to jovyan directory.
COPY --chown=1000:100 . .
RUN rm -rf requirements.txt LICENSE README.md docker .git .github

RUN wget https://www.hecbiosim.ac.uk/file-store/tw2025-dna-workshop/01_Prod-0.nc && \
    wget https://www.hecbiosim.ac.uk/file-store/tw2025-dna-workshop/01_Prod-2.nc && \
    cp 01_Prod-0.nc data/ && \
    mv 01_Prod-0.nc 01_Prod-2.nc tested_files/

# Copy updated lab workspace
COPY --chown=1000:100 docker/default-37a8.jupyterlab-workspace /home/jovyan/.jupyter/lab/workspaces/default-37a8.jupyterlab-workspace

# UNCOMMENT THIS LINE FOR REMOTE DEPLOYMENT
COPY docker/jupyter_notebook_config.py /etc/jupyter/

# Always finish with non-root user as a precaution.
USER $NB_USER
