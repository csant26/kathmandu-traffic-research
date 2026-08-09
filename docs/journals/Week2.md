### Week 2

- If/when data collection is successful,
    - Smoothing out the vehicles for clear analysis.
    - Using ML/IP to hide the license plates.
    - Using ML/IP to categorise the vehicles.
    - Figuring out how to normalise the data. (Maybe stop signal timer could help us with this.)
    - Presenting the data metrics.

- SUMO stages:
    1. Export the map from OSM(Open Street Map).

    2. OSM to XML
    - The .osm file contains geometrical data. We need to convert it into data that SUMO can actually work with. For this, we use ***netconvert*** that reads the osm file and extracts the xml file containing information that SUMO needs and understands.
    - Since the conversion isn't perfect, we need bunch of options like: geometry.remove, junctions.join, tls.guess-signals, tls.join etc. to make sure that the data is automatically cleaned-out before we perform futher operations on it.

        ```bash
        > netconvert \
        --osm-files maps/koteshwor-corridor.osm \
            --geometry.remove \
            --junctions.join \
            --tls.guess-signals \
            --tls.join \
            -o networks/koteshwor-corridor.net.xml
        ```

    3.  Then we open the .xml file created using ***netconvert*** in ***sumo-gui***. Here, we inspect the network and decide what to edit.

        ```bash
        > sumo-gui networks/koteshwor-corridor.net.xml
        ```

    4.  Further manipulation of the network is done via ***netedit***.
    - Firstly, take a copy of the network to make recovering easy.

        ```bash
        >  cp networks/koteshwor-corridor.net.xml \
              networks/koteshwor-corridor-copy.net.xml
        ```
    
    - Then open the copy in ***netedit***.

        ```bash
        > netedit networks/koteshwor-corridor-copy.net.xml
        ```


