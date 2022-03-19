ARG BASE_IMAGE=alpine
FROM ${BASE_IMAGE}
VOLUME /sml2mqtt
ARG MODULE=git+https://github.com/spacemanspiff2007/sml2mqtt.git@master
RUN apk add --no-cache python3 py3-wheel py3-pip gcc musl-dev python3-dev git && \
    pip install --no-cache-dir "${MODULE}" && \
    pip show -V sml2mqtt | sed -nE 's/^Version: (.+)$/\1/p' >.app-version && \
    apk del py3-wheel py3-pip gcc musl-dev python3-dev git
CMD [ "sml2mqtt" ]
