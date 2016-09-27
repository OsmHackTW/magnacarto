FROM osmtw/mapnik3:v3.0.9

MAINTAINER Rex Tsai "https://about.me/chihchun"

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update \
 && apt-get install -y vim-tiny \
 && apt-get install -y golang git build-essential

ENV GOPATH=/opt/magnacarto
RUN mkdir -p ${GOPATH} \
 && cd ${GOPATH} \
 && go get -u github.com/omniscale/magnacarto \
 && cd $GOPATH/src/github.com/omniscale/magnacarto \
 && make install

# Setup sample data.
RUN apt-get install -y --no-install-recommends wget unzip
RUN cd /opt/magnacarto/src/github.com/omniscale/magnacarto/docs/examples/ \
 && wget http://www.naturalearthdata.com/http//www.naturalearthdata.com/download/10m/cultural/ne_10m_admin_0_countries.zip \
 && mkdir ne_10m_admin_0_countries \
 && cd ne_10m_admin_0_countries \
 && unzip ../ne_10m_admin_0_countries.zip \
 && rm -fv ../ne_10m_admin_0_countries.zip

RUN cd /opt/magnacarto/src/github.com/omniscale/magnacarto/docs/examples/ \
 && wget https://s3.amazonaws.com/metro-extracts.mapzen.com/hamburg_germany.imposm-shapefiles.zip \
 && mkdir hamburg_germany \
 && cd hamburg_germany \
 && unzip ../hamburg_germany.imposm-shapefiles.zip \
 && rm -fv ../hamburg_germany.imposm-shapefiles.zip    

# Setup runtime path.
RUN ln -s /opt/magnacarto/bin/* /usr/local/bin

RUN apt-get install -y mapserver-bin
RUN apt-get autoremove -y --purge git build-essential wget unzip \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

VOLUME /build
WORKDIR /build
