FROM dceoy/samtools:latest

ADD https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip /tmp/awscli.zip
ADD https://raw.githubusercontent.com/dceoy/s3-sync-entrypoint/main/s3-sync-entrypoint /usr/local/bin/s3-sync-entrypoint
ADD https://raw.githubusercontent.com/dceoy/replace-sam-read-group/main/replace-sam-read-group /usr/local/bin/replace-sam-read-group

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        unzip \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && chmod +x /usr/local/bin/{s3-sync-entrypoint,replace-sam-read-group}

RUN set -e \
      && cd /tmp \
      && unzip awscli.zip \
      && ./aws/install

ENV INPUT_DATA_DIR /input
ENV OUTPUT_DATA_DIR /output

ENTRYPOINT ["/usr/local/bin/s3-sync-entrypoint"]
CMD ["replace-sam-read-group"]
