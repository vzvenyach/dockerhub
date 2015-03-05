# Install phantomjs per: http://phantomjs.org/build.html
# VERSION               0.0.1

FROM      ubuntu:14.04
MAINTAINER V. David Zvenyach <dave@esq.io>

# Install dependencies
RUN apt-get update && apt-get install -y build-essential g++ flex bison gperf ruby perl \
	libsqlite3-dev libfontconfig1-dev libicu-dev libfreetype6 libssl-dev \
	libpng-dev libjpeg-dev git python

# Build from source
RUN git clone git://github.com/ariya/phantomjs.git && cd phantomjs && git checkout 2.0 && yes | ./build.sh

ENTRYPOINT ["./phantomjs/bin/phantomjs"]
CMD ['-v']