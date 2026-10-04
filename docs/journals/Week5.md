### Week 5

- Now that the data has been finished, we move towards simulation.
- To run simulation, we approach it steadily; step by step.
- We tried converting the OSM to SUMO XML network and manipulating it haphazardly. But we got more lost as we progressed.
- Let's build structure.
- For SUMO simulation, we need four things:
1. Network (.net.xml) => which we already have from OSM. We'll further operate on this.
2. Vehicle types/composition (vtypes.xml) => the types of vehicles that run on our network. We've already decided this from [this](../../data/data-collection.md)
3. Routes/Trips (.rou.xml) => what vehicle goes where and when.
4. Config (.sumocfg) => points to the config file that acts as starting point and runs the simulation. 

### A) Network

- We already have a network from OSM.
- 