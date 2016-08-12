FROM ruby:2.3.1

MAINTAINER Renuo Developers <dev@renuo.ch>

# Install gdal
ENV GDAL_VERSION 2.1.1

RUN DEBIAN_FRONTEND=noninteractive apt-get -qq update \
    && apt-get -qqy upgrade \
    && apt-get -qqy --fix-missing install wget g++ make pkg-config zlib1g-dev libkml-dev \
    && cd /usr/src \
    && wget http://download.osgeo.org/gdal/${GDAL_VERSION}/gdal-${GDAL_VERSION}.tar.gz \
    && tar xzf gdal-${GDAL_VERSION}.tar.gz \
    && cd gdal-${GDAL_VERSION} \
    && ./configure --prefix=/usr --sysconfdir=/etc --with-libkml \
    && make -j4 \
    && make install


# Install gdal_calculations
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y python-pip python-gdal
RUN pip install git+git://github.com/lpinner/gdal-calculations@1.1

# Install missing libraries
RUN DEBIAN_FRONTEND=noninteractive && apt-get --fix-missing install -y --force-yes \
  libproj-dev \
  python-numpy \
  python-dev \
  libgdal-dev \
  libgdal1h \
  libproj-dev \
  libgeos-dev

# Set flag for rgeo gem
RUN bundle config build.rgeo --with-geos-dir=/usr/bin/

ENV app /app
RUN mkdir $app
WORKDIR $app
