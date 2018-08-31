FROM python:2.7-alpine

# create directory with alpine and set working directory
RUN mkdir /app
WORKDIR /app

# install dependencies first
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt

# Then copy the entire directory where you code lives
# will copy everything in the current docker directory on local into the WORKDIR in IMAGE
COPY . .

# You want as close to the bottom, but not the last line
# KEY:VALUE, optional, used for filtering docker images
LABEL maintainer="Alfredo Marquez <alfredo@gmail.com>"\
      version="1.0"

# Gets executed when the image gets built, not when the dockerfile builds the image.
CMD flask run --host=0.0.0.0 --port=5000
