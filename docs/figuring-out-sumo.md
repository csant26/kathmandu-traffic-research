### SUMO stages:

#### 1. Export the map from OSM(Open Street Map).

#### 2. OSM to XML

- The .osm file contains geometrical data. We need to convert it into data that SUMO can actually work with. For this, we use ***netconvert*** that reads the osm file and extracts the xml file containing information that SUMO needs and understands.
- Since the conversion isn't perfect, we need bunch of options like: geometry.remove, junctions.join, tls.guess-signals, tls.join etc. to make sure that the data is automatically cleaned-out before we perform futher operations on it.
- SUMO reads the lane information from OSM where `lanes` tags are available. On stretches where the Ring Road is mapped as separate one-way carriageways, each direction may appear with fewer lanes per edge; that still reflects how the corridor is represented in OSM.

```bash
> netconvert \
  --osm-files maps/koteshwor-corridor.osm \
  --geometry.remove \
  --junctions.join \
  --tls.guess-signals \
  --tls.join \
  -o networks/koteshwor-corridor.net.xml
```

#### 3. Then we open the .xml file created using ***netconvert*** in ***sumo-gui***. Here, we inspect the network and decide what to edit.

- We locate the Koteshwor–Tinkune corridor and review the main highway first.
- We note lane counts on the main approaches and check whether traffic signals are present at Koteshwor before making changes in netedit.

```bash
> sumo-gui networks/koteshwor-corridor.net.xml
```

#### 4. Further manipulation of the network is done via ***netedit***.

- Firstly, take a copy of the network to make recovering easy.

```bash
> cp networks/koteshwor-corridor.net.xml \
    networks/koteshwor-corridor-copy.net.xml
```

- Then open the copy in ***netedit***.

```bash
> netedit networks/koteshwor-corridor-copy.net.xml
```

- Edits are focused on the main corridor (lane counts and traffic signals at Koteshwor as needed). After each set of changes, we reopen the network in sumo-gui to verify the result before moving on to demand and simulation.
