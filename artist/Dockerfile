FROM tensorflow/magenta

ADD https://github.com/openfaas/faas/releases/download/0.6.9/fwatchdog /usr/bin
RUN chmod +x /usr/bin/fwatchdog

WORKDIR /root/

ADD patch.sh .
RUN sh patch.sh

COPY index.py           .
COPY requirements.txt   .
RUN pip install -r requirements.txt

COPY function function

RUN touch ./function/__init__.py

WORKDIR /root/function/
COPY function/requirements.txt	.
RUN pip install -r requirements.txt

WORKDIR /root/

COPY input input

ENV fprocess="python index.py"

HEALTHCHECK --interval=1s CMD [ -e /tmp/.lock ] || exit 1

CMD [ "/usr/bin/fwatchdog"]
