# VERSION               0.0.1

FROM      ubuntu:14.04
MAINTAINER V. David Zvenyach <dave@esq.io>

# USAGE
# interactive
# 	sudo docker run -ti --rm --name pa11y -p 4000:4000 vzvenyach/pa11ydash
# or daemonized: 
# 	sudo docker run -ti -d --name pa11y -p 4000:4000 vzvenyach/pa11ydash

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

# Install MongoDB
RUN sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10 &&  echo 'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen' | sudo tee /etc/apt/sources.list.d/mongodb.list && apt-get update && apt-get install -y mongodb-org

# Install pa11y-dashboard
RUN git clone https://github.com/nature/pa11y-dashboard.git && cd pa11y-dashboard && cp config/production.sample.json config/production.json && npm install
RUN git clone https://github.com/nature/pa11y-webservice.git && cd pa11y-webservice && cp config/production.sample.json config/production.json && npm install
EXPOSE 4000
EXPOSE 3000

RUN mkdir -p /data/db
EXPOSE 27017
RUN chown -R mongodb:mongodb /var/lib/mongodb/.

WORKDIR /pa11y-dashboard
ENTRYPOINT mongod --fork --dbpath /var/lib/mongodb/ --smallfiles --logpath /var/log/mongodb.log --logappend && NODE_ENV=production node .

# Run it
CMD ["/bin/bash"]