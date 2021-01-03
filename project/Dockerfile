#pull official base image
FROM python:3.9.0-slim-buster

#set working directory
WORKDIR /usr/src/app

#set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1
ENV USER=app
ENV APP_HOME=/home/app/web

# install system dependencies
RUN apt-get update \ 
  && apt-get -y install netcat gcc \
  && apt-get clean

# install python dependencies
RUN pip install --upgrade pip
COPY ./requirements.txt .
RUN pip install -r requirements.txt

RUN adduser --system --group $USER
RUN mkdir $APP_HOME
WORKDIR $APP_HOME 


# add app
COPY . $APP_HOME
RUN chown -R $USER:$USER $APP_HOME
USER $USER

# run entrypoint.sh
ENTRYPOINT ["/usr/src/app/entrypoint.sh"]
