FROM ubuntu:14.04

ENV a_HOME /opt/webapp
RUN mkdir -p "$a_HOME"
WORKDIR $a_HOME

RUN apt-get update

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y -q python-all python-pip

RUN mkdir -p "$a_HOME"

ADD app.py $a_HOME
ADD requirements.txt /tmp/

RUN pip install -qr /tmp/requirements.txt

EXPOSE 5000

ENTRYPOINT ["python", "app.py"]