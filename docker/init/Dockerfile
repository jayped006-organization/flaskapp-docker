FROM python:3.6.4-alpine3.7

RUN apk --update add gettext

ARG repo
ARG full_name
ARG email
ARG github_username
ARG app_name
ARG project_name
ARG project_short_description

ENV FULL_NAME $full_name
ENV EMAIL $email
ENV GITHUB_USERNAME $github_username
ENV APP_NAME $app_name
ENV PROJECT_NAME $project_name
ENV PROJECT_SHORT_DESCRIPTION $project_short_description

WORKDIR /root/

COPY cookiecutter.template.yml cookiecutter.template.yml

RUN envsubst <cookiecutter.template.yml >cookiecutter.yml && \
  pip install cookiecutter && \
  apk --update add git

RUN git clone $repo && \
  cd cookiecutter-flask && \
  git reset --hard df50c8ad6e26dc528996f0cf0ea388d9e84448db

RUN cookiecutter --no-input --config-file cookiecutter.yml cookiecutter-flask
