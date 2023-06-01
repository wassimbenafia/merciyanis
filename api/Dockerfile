FROM python:3.7-alpine

RUN apk update
RUN apk add --no-cache --virtual .build-deps gcc musl-dev postgresql-dev
RUN apk add postgresql-client
RUN apk add supervisor
RUN apk add libffi-dev

COPY ./plugins /plugins/

RUN pip install pip==21.2.4
#RUN /usr/local/bin/python -m pip install --upgrade pip

RUN pip install pipdeptree
COPY ./dockerfiles/api/requirements.sh /tmp/
COPY ./dockerfiles/api/requirements.txt /tmp/requirements_plugins.txt
RUN ls /tmp
RUN ["chmod", "+x", "/tmp/requirements.sh"]
RUN cat /tmp/requirements_plugins.txt
RUN pip install --use-feature=2020-resolver --requirement /tmp/requirements_plugins.txt
RUN pipdeptree

WORKDIR /usr/src/app

RUN apk --purge del .build-deps

RUN mkdir -p /var/log/celery/
RUN touch /var/log/celery/project_beat.log
RUN touch /var/log/celery/project_worker.log

# Set up AWS
RUN mkdir -p /var/backups
ARG AWS_ACCESS_KEY_ID
ARG AWS_SECRET_ACCESS_KEY
RUN mkdir -p ~/.aws/
RUN touch ~/.aws/credentials
RUN echo [django-language-fieldault] >> ~/.aws/credentials
RUN echo aws_access_key_id = ${AWS_ACCESS_KEY_ID} >> ~/.aws/credentials
RUN echo aws_secret_access_key = ${AWS_SECRET_ACCESS_KEY} >> ~/.aws/credentials

#COPY ./plugins /usr/src/plugins
#COPY ./api /usr/src/app


