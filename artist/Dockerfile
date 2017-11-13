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

# Monet
# ---------------------
# --num_styles=10 \
# --checkpoint=/magenta-models/multistyle-pastiche-generator-monet.ckpt \
# --input_image=$IMAGE \
# --which_styles="{$i:1}" \
# --output_dir="out_""$IMAGE" \
# --output_basename="monet_styles"

# Varied
# ---------------------
# --num_styles=32 \
# --checkpoint=/magenta-models/multistyle-pastiche-generator-varied.ckpt \
# --input_image=$IMAGE \
# --which_styles="{$i:1}" \
# --output_dir="out_""$IMAGE" \
# --output_basename="varied_styles"

ENV fprocess="python index.py"

HEALTHCHECK --interval=1s CMD [ -e /tmp/.lock ] || exit 1

CMD [ "/usr/bin/fwatchdog"]
