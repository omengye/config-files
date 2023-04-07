FROM ubuntu:20.04
LABEL maintainer="omengye"

ENV NAIVEPROXY_VERSION=v112.0.5615.49-1
ENV NAIVEPROXY_HOME="/usr/local/bin/naive"
ENV NAIVEPROXY_RM="naiveproxy-${NAIVEPROXY_VERSION}-linux-x64"
ENV FILE="${NAIVEPROXY_RM}.tar.xz"

RUN set -xe \
  && apt update \
  && apt install -y --no-install-recommends libnss3 curl ca-certificates xz-utils\
  && mkdir -p "$NAIVEPROXY_HOME" \
  && cd "$NAIVEPROXY_HOME"\
  && curl -fsSLO --compressed "https://github.com/klzgrad/naiveproxy/releases/download/${NAIVEPROXY_VERSION}/${FILE}" \
  && tar xJvf "${FILE}" -C "$NAIVEPROXY_HOME" \
  && ls -al \
  && mv ${NAIVEPROXY_HOME}/${NAIVEPROXY_RM}/* ${NAIVEPROXY_HOME} \
  && rm -rf "${NAIVEPROXY_HOME}/${FILE}" "${NAIVEPROXY_HOME}/${NAIVEPROXY_RM}" LICENSE USAGE.txt \
  && rm -rf /var/lib/{apt,dpkg,cache,log}/ \
  && adduser naiveproxy_user

COPY config.json "${NAIVEPROXY_HOME}/config.json"
COPY entrypoint.sh /entrypoint.sh
RUN chmod a+x /entrypoint.sh

RUN echo "export NAIVEPROXY_HOME=${NAIVEPROXY_HOME}" >> /etc/profile
VOLUME "$NAIVEPROXY_HOME"

USER naiveproxy_user
CMD [ "/entrypoint.sh" ]
