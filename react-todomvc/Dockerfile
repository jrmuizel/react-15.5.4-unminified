FROM ubuntu:xenial
RUN apt-get update && \
   DEBIAN_FRONTEND=noninteractive apt-get install -y \
     git vim
#RUN DEBIAN_FRONTEND=noninteractive apt-get install -y nodejs npm
RUN cd root && git clone https://github.com/facebook/react && cd react && git checkout v15.5.4
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y curl
ENV NVM_DIR /root/.nvm
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.2/install.sh | bash \
     && . $NVM_DIR/nvm.sh \
    && nvm install 7.10.1
RUN cd /root/react && . $NVM_DIR/nvm.sh && npm install
RUN cd /root/react && . $NVM_DIR/nvm.sh && npm run build
ADD no-minify.patch /tmp/no-minify.patch
RUN cd /root/react && patch -p1 < /tmp/no-minify.patch
RUN cd /root/react && . $NVM_DIR/nvm.sh && npm run build
# \
#    && nvm alias default $NODE_VERSION \
#    && nvm use default
