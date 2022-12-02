ARG VARIANT="ubuntu-20.04"
FROM mcr.microsoft.com/vscode/devcontainers/base:0-${VARIANT}

RUN apt-get update \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install curl 

RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-$(uname -m).zip" -o "awscliv2.zip" && \
    unzip awscliv2.zip && \
    ./aws/install && \
    rm -rf ./aws awscliv2.zip

ARG TERRAFORM_VERSION="1.1.3"
ARG TERRAFORM_CHECKSUM="b215de2a18947fff41803716b1829a3c462c4f009b687c2cbdb52ceb51157c2f"
RUN curl -sSL -o terraform.zip "https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip" && \
    echo "${TERRAFORM_CHECKSUM} terraform.zip" | sha256sum -c && \
    unzip terraform.zip && \
    mv -f terraform /usr/local/bin/terraform && \
    rm terraform.zip && \
    chmod +x /usr/local/bin/terraform && \
    terraform version

ARG TERRAGRUNT_VERSION="0.35.20"
ARG TERRAGRUNT_CHECKSUM="79c7756d5913858e245c1319c15b4dc1615a6c1dccc569f88f38e92d112671da"
RUN curl -sSL -o terragrunt "https://github.com/gruntwork-io/terragrunt/releases/download/v${TERRAGRUNT_VERSION}/terragrunt_linux_amd64" && \
    echo "${TERRAGRUNT_CHECKSUM} terragrunt" | sha256sum -c && \
    mv -f terragrunt /usr/local/bin/terragrunt && \
    chmod +x /usr/local/bin/terragrunt && \
    terragrunt --version

ARG GH_VERSION="2.5.0"
ARG GH_CHECKSUM="4390bc476cc79c33346be3e0098cfbb3afe2257006fcd38765ef83569df11a0f"
RUN curl -sSL -o gh.tar.gz "https://github.com/cli/cli/releases/download/v${GH_VERSION}/gh_${GH_VERSION}_linux_amd64.tar.gz" && \
    echo "${GH_CHECKSUM} gh.tar.gz" | sha256sum -c && \
    tar -xvzf gh.tar.gz -C /tmp/ --strip-components=1 && \
    mv /tmp/bin/gh /usr/local/bin/gh  && \
    rm -rf gh.tar.gz /tmp/gh  && \
    chmod +x /usr/local/bin/gh && \
    gh --version
    
ARG YQ_VERSION="4.20.2"
ARG YQ_CHECKSUM="3fbb76eaf00c3639468eb2613a6fa21933b53744e0918c4b12cdf4e1c6788de3"
RUN curl -sSL -o yq "https://github.com/mikefarah/yq/releases/download/v${YQ_VERSION}/yq_linux_amd64" && \
    echo "${YQ_CHECKSUM} yq" | sha256sum -c && \
    mv -f yq /usr/local/bin/yq && \
    chmod +x /usr/local/bin/yq && \
    yq --version
    
RUN apt-get update \
  && DEBIAN_FRONTEND=noninteractive apt-get -y --no-install-recommends install \
    bash-completion \
  && apt-get clean \
  && rm /etc/apt/apt.conf.d/docker-clean

USER vscode