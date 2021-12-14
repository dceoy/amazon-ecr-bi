FROM dceoy/sagvc:latest

ADD https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip /tmp/awscli.zip
ADD https://raw.githubusercontent.com/dceoy/s3-sync-entrypoint/main/s3-sync-entrypoint /usr/local/bin/s3-sync-entrypoint

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        unzip \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && chmod +x /usr/local/bin/s3-sync-entrypoint

RUN set -e \
      && cd /tmp \
      && unzip awscli.zip \
      && ./aws/install

RUN set -e \
      && /opt/conda/bin/python3 -m pip install -U --no-cache-dir \
        https://github.com/dceoy/ftarc/archive/main.tar.gz \
        https://github.com/dceoy/vanqc/archive/main.tar.gz \
        https://github.com/dceoy/sagvc/archive/main.tar.gz

ENV INPUT_DATA_DIR /input
ENV OUTPUT_DATA_DIR /output

RUN set -e \
      && mkdir -p "${INPUT_DATA_DIR}" "${OUTPUT_DATA_DIR}" \
      && chmod 777 "${INPUT_DATA_DIR}" "${OUTPUT_DATA_DIR}"

ENTRYPOINT ["/usr/local/bin/s3-sync-entrypoint"]
CMD ["sagvc"]
