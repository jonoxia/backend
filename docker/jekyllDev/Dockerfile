# FROM jekyll/jekyll:pages
FROM grahamc/jekyll

RUN apt-get update

# for editing 
RUN apt-get install -y vim-tiny

RUN apt-get install -y git

# RUN apk --update add git vim

RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get install -y nodejs

RUN npm install -g webpack
RUN npm install -g webpack-cli

ARG CACHEBUST=1
ARG FE_PATH=/usr/src/app/frontend/
ARG BRANCH_NAME=master
ARG REPO=https://github.com/voteamerica/voteamerica.github.io

WORKDIR /usr/src/app/

RUN git clone --single-branch --branch $BRANCH_NAME $REPO frontend \
&& cd $FE_PATH \
&& git checkout $BRANCH_NAME

WORKDIR $FE_PATH

RUN pwd
RUN ls

RUN git fetch origin
RUN git merge origin/$BRANCH_NAME

# run webpack as background task
# RUN webpack --watch --progress --info-verbosity verbose &

COPY ./_config-local-host.yml /
COPY ./_config-local-ip.yml /

COPY ./expo-start.sh /
RUN chmod +x /expo-start.sh

RUN echo "expo-start.sh"
RUN more /expo-start.sh

# ENTRYPOINT ["jekyll serve -H 0.0.0.0 --watch --config _config-dev.yml"]
# ENTRYPOINT [""]
# ENTRYPOINT ["/bin/bash"]
ENTRYPOINT ["/expo-start.sh"]

# CMD ["/bin/bash"]
