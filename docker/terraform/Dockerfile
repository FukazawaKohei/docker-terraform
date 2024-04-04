FROM ubuntu:22.04

WORKDIR /tmp

# 共通利用のパッケージのインストール
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y less vim curl unzip git

# aws cli v2 のインストール
# https://docs.aws.amazon.com/ja_jp/cli/latest/userguide/install-cliv2-linux.html
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
RUN unzip awscliv2.zip
RUN ./aws/install
RUN rm awscliv2.zip

# terraformのインストール（バイナリを落としてきてパスの通っているところに解凍する方法）
ENV TF_VERSION=1.7.5
RUN curl "https://releases.hashicorp.com/terraform/${TF_VERSION}/terraform_${TF_VERSION}_linux_amd64.zip" -o "terraform.zip"
RUN unzip -d /usr/local/bin/ terraform.zip
RUN rm terraform.zip

WORKDIR /src
