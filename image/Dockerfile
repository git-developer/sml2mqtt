ARG BASE_IMAGE=alpine
FROM ${BASE_IMAGE}
VOLUME /sml2mqtt
ARG MODULE=git+https://github.com/spacemanspiff2007/sml2mqtt.git
RUN apk add --no-cache python3 py3-wheel py3-pip gcc musl-dev python3-dev git && \
    pip install --no-cache-dir --no-clean "${MODULE}" && \
    mkdir /opt/sml2mqtt && \
    repo="$(find /tmp -type d -name .git -exec dirname '{}' \;)" && \
    if [ -d "${repo}" ]; then \
      cd "${repo}" && \
      git rev-parse --short HEAD      >/opt/sml2mqtt/commit_short_sha && \
      git rev-parse --abbrev-ref HEAD >/opt/sml2mqtt/commit_ref_name && \
      git show -s --format=%ci HEAD   >/opt/sml2mqtt/commit_date && \
      true; \
    fi && \
    pip show -V sml2mqtt | sed -nE 's/^Version: (.+)$/\1/p' >/opt/sml2mqtt/app_version && \
    apk del py3-wheel py3-pip gcc musl-dev python3-dev git && \
    rm -fr /tmp/*
CMD [ "sml2mqtt" ]
