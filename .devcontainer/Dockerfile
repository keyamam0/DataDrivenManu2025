#jbankg入りのコンテナイメージ
FROM registry.access.redhat.com/ubi8/ubi-minimal:latest

# 必要なパッケージインストール
RUN microdnf install -y \
    curl \
    tar \
    gzip \
    unzip \
    java-17-openjdk-headless && \
    microdnf clean all

# JBangインストール
RUN curl -Ls https://sh.jbang.dev | bash -s - && \
    mv /root/.jbang/bin/jbang /usr/local/bin/jbang

# 信頼するURLを事前登録
RUN jbang trust add https://github.com/apache/camel/

# Camel JBangインストール
RUN jbang app install camel@apache/camel

ENV PATH="/usr/local/bin:${PATH}"

WORKDIR /workspace

# CMD ["camel", "version"]
