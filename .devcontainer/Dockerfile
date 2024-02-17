# Arguments
ARG PYTHON_VER="3.10"
FROM python:$PYTHON_VER

# Arguments
ARG PYTHON_VER="3.10"
ARG QUARTO_VER="1.4.549"
ARG ENV_NAME="shiny-express"
# Environment variables
ENV ENV_NAME=$ENV_NAME
ENV PYTHON_VER=$PYTHON_VER
ENV QUARTO_VER=$QUARTO_VER

# Copy files
RUN mkdir requirements

COPY install_quarto.sh install_dependencies.sh requirements/
RUN bash ./requirements/install_dependencies.sh
RUN bash ./requirements/install_quarto.sh $QUARTO_VER


# Install dependencies
COPY requirements.txt install_requirements.sh requirements/
RUN bash requirements/install_requirements.sh $ENV_NAME $PYTHON_VER

# Copy the app
RUN mkdir my_app
COPY app.py my_app/

ENV PATH="/opt/conda/envs/shiny-express/bin:$PATH"

CMD shiny run --host 0.0.0.0 --port 8080 /my_app/app.py
EXPOSE 8080
