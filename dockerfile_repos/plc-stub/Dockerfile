#jbang入りのコンテナイメージ
FROM registry.access.redhat.com/ubi8/ubi-minimal:latest

# 必要なパッケージインストール
RUN microdnf install -y \
    curl \
    tar \
    gzip \
    unzip \
    git \
    java-17-openjdk-headless && \
    microdnf clean all

# JBangインストール
RUN curl -Ls https://sh.jbang.dev | bash -s - && \
    mv /root/.jbang/bin/jbang /usr/local/bin/jbang

# 信頼するURLを事前登録
RUN jbang trust add https://github.com/apache/camel/

# Camel JBangインストール
RUN jbang app install camel@apache/camel

ENV PATH="/root/.jbang/bin:/usr/local/bin:${PATH}"

RUN mkdir -p /workspace/routes \
 && curl -o /workspace/routes/plc-stub-route.yaml \
    https://raw.githubusercontent.com/keyamam0/DataDrivenManu2025/main/routes/plc-stub-route.yaml

# GitHubから sampledata ディレクトリのみ取得
RUN git clone --depth 1 https://github.com/keyamam0/DataDrivenManu2025.git /tmp/repo \
&& cp -r /tmp/repo/sampledata /workspace/sampledata \
&& rm -rf /tmp/repo

WORKDIR /workspace

# コンテナ起動時にCamelルートを実行
CMD ["camel", "run", "/workspace/routes/plc-stub-route.yaml"]