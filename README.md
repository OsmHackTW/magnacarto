# Docker image of Magnacarto

# Usage

## Web fontend

Start web-frontend for Magnacarto

    docker run -t -i --rm -p 8080:8080 -v `pwd`:/build osmtw/magnacarto \
        sh -c "cd /opt/magnacarto/src/github.com/omniscale/magnacarto/docs/examples && magnaserv -listen 0.0.0.0:8080"

You can now access to the frontend with browser via http://127.0.0.1:8080

## rendering maps
Please see the example in [magnacarto/docs/examples](https://github.com/omniscale/magnacarto/tree/master/docs/examples)

    # Create a Mapnik XML
    docker run -t -i --rm -v `pwd`:/build osmtw/magnacarto \
        magnacarto -mml /opt/magnacarto/src/github.com/omniscale/magnacarto/docs/examples/world.mml > world.xml   
    # Render map with nik2img
    docker run -t -i --rm -v `pwd`:/build osmtw/magnacarto \
        nik2img.py -d 1000 1000 world.xml world.png

    # OSM Roads
    docker run -t -i --rm -v `pwd`:/build osmtw/magnacarto \
        magnacarto -mml /opt/magnacarto/src/github.com/omniscale/magnacarto/docs/examples/roads.mml > roads.xml
    docker run -t -i --rm -v `pwd`:/build osmtw/magnacarto \
        nik2img.py -d 500 500 -s 3857 -e 1120261 7086018 1122707 7088464 roads.xml roads.png

## Issue
* nik2img does not work well with mapnik3 for the roads demo.

# Reference
* Magnacarto is a CartoCSS map style processor that generates Mapnik XML and MapServer map files.  https://github.com/omniscale/magnacarto


[![Docker Automated build](https://img.shields.io/docker/automated/osmtw/magnacarto.svg?maxAge=2592000)](https://hub.docker.com/r/osmtw/magnacarto/)

[![](https://images.microbadger.com/badges/image/osmtw/magnacarto.svg)](https://microbadger.com/images/osmtw/magnacarto)
