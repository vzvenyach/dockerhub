# VERSION               0.0.1

FROM      ubuntu:14.04
MAINTAINER V. David Zvenyach <dave@esq.io>

# Usage
# sudo docker run -ti vzvenyach/pa11y 

# Install dependencies
RUN apt-get update && apt-get install -y build-essential g++ flex bison gperf ruby perl \
	libsqlite3-dev libfontconfig1-dev libicu-dev libfreetype6 libssl-dev \
	libpng-dev libjpeg-dev git python curl

# Install phantomjs per: http://phantomjs.org/build.html
RUN git clone git://github.com/ariya/phantomjs.git && cd phantomjs && git checkout 2.0 && yes | ./build.sh


# Install node
RUN curl -sL https://deb.nodesource.com/setup | sudo bash - && apt-get install -y nodejs


# Install Pally CLI
RUN npm install -g pa11y

RUN ln -s /phantomjs/bin/phantomjs /usr/local/bin/phantomjs

# Run it
ENTRYPOINT ["pa11y"]
CMD ["-v"]