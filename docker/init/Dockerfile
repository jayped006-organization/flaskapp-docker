FROM python:3.6.4-alpine3.7

RUN apk --update add gettext

ARG repo
ARG full_name
ARG email
ARG github_username
ARG docker_username
ARG app_name
ARG project_name
ARG project_short_description

ENV FULL_NAME $full_name
ENV EMAIL $email
ENV GITHUB_USERNAME $github_username
ENV DOCKER_USERNAME $docker_username
ENV APP_NAME $app_name
ENV PROJECT_NAME $project_name
ENV PROJECT_SHORT_DESCRIPTION $project_short_description

WORKDIR /root/

COPY cookiecutter.template.yml cookiecutter.template.yml

RUN envsubst <cookiecutter.template.yml >cookiecutter.yml && \
  pip install cookiecutter && \
  apk --update add git

RUN cookiecutter --no-input --config-file cookiecutter.yml $repo

RUN sed -i 's/NODE_ENV=debug webpack-dev-server --port 2992 --hot --inline/NODE_ENV=debug webpack-dev-server --port 2992 --hot --inline --host 0.0.0.0/' ./$APP_NAME/package.json && \
  sed -i 's/FLASK_DEBUG=1 flask run/FLASK_DEBUG=1 flask run --host=0.0.0.0/' ./$APP_NAME/package.json
