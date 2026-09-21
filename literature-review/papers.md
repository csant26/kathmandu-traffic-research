## Relevant research papers

### A Case Study of Traffic Chowk, Butwal

Link: https://www.nepjol.info/index.php/injet/article/download/78587/60190/226040

Notes:
- Uses SIDRA Intersection model to analyse the traffic scenario.
- Data collection is done via camera surveillance.
- Clearly maps out the lane system, traffic signals, peak hours, queue analysis.
- Quite very relevant to us during the analysis phase.
- **Cite for:** delay, queue, LOS as the intersection indicator set (gold-standard primary count we did not replicate).



### Microscopic Traffic Simulation using SUMO

Link: https://elib.dlr.de/127994/1/08569938.pdf

Notes:
- Very detailed and clear to follow.
- Data collection is done via the help of city administration.
- Serves as a guide to using SUMO and things that need to be considered while using SUMO.
- Thorough comprehension of it during the setting up of SUMO will be helpful to us.
- **Cite for:** SUMO workflow (network + demand + outputs); validation with RMSE; 85% of counts within 15%.


### Comparative Analysis of Traffic Simulation Parameters Using SUMO and TraCI API

Link: https://ijarcce.com/wp-content/uploads/2025/11/IJARCCE.2025.141106-Comparative.pdf

Notes:
- Analysis-focused.
- Data collection is smartly mapped here.
- Also, the paper looks very organised and easy to follow. So, could be useful during our paper to figure out what components of research should be included effectively.
- **Cite for:** travel time, queue length, throughput as comparison parameters; classified mode × peak-hour table layout; TraCI if we code bus priority.

### Refining SUMO Simulation Strategies for Realistic Traffic Patterns: Insights from Field Experience

Link: https://hal.science/hal-04408938/file/ICSRS_2023_paper_81.pdf

Notes:
- Focused more on how SUMO should be used rather than what SUMO does, which is an interesting insight.
- Very meticulous and covers the traffic analysis from mathematical aspect as well.
- Aims to improve the traffic flow in densely populated areas which is in direct correlation to our study.
- **Cite for:** calibration discipline in Discussion.

### Calibration of SUMO Microscopic Simulation for Heterogeneous Traffic Condition: The Case of the City of Khulna, Bangladesh

Link: https://www.sciencedirect.com/science/article/pii/S2666691X24000551

Notes:
- Analyses alternate scenarios by proposing alternate road geometries and traffic signals, which I found quite fascinating.
- Also, the vehicle attributes and data preparation model is really helpful.
- Also, accounts for driver's response to traffic and driver's mistakes, which may be informative.
- Contains large volume of mathematical data which could be a bit more out-of-scope for our research. Nevertheless, really useful overall.
- **Cite for:** heterogeneous-traffic SUMO; calibrate on flow, queue, travel time via RMSE; starting `sigma=0.3`, `tau=1.4`; scenarios only after calibration.

### Framework for AI-Driven Traffic Management in Kathmandu

Link: https://www.researchgate.net/publication/392543119_Framework_for_AI-Driven_Traffic_Management_in_Kathmandu

Notes:
- Similar to our research in the sense that Koteshwor is included in the study area and SUMO is used for simulating the traffic.
- Data collection is done through visual analysis of site and data from Ministry of Physical Infrastructure and Transport’s offcial website.
- Doesn't provide the SUMO output or methodology.
- Promises improvement in case of AI intervention. 
- Provides multiple instances around the world where AI solutions have been used.
- We could implement AI as one of the solutions to improving the traffic and leverage this report to cross-check our findings.
- **Cite for:** Koteshwor in a Kathmandu SUMO/AI study; secondary MoPIT/DoR data as an accepted local method.


### Real-Time Traffic Prediction Using Monte Carlo Simulation: A Case Study of Kantipath Road, Kathmandu, Nepal

Link: https://www.nepjol.info/index.php/BIBECHANA/article/view/46394

Notes:
- Mainly aimed at analysing the vehicles and predicting the traffic flow.
- Suggests a higher frequency of public transit for optimising the traffic congestion.
- Uses Sony camera for data collection.
- Although the process doesn't involve SUMO, this might come in use to reference the traffic scenario.
- **Cite for:** ~66% two-wheelers and ~90% private; MAPE as error metric; public share small vs private.

### Addressing Traffic Congestion: Strategic Approaches to Public Transport Optimization in Kathmandu

Link: https://easts.info/on-line/proceedings/vol.15/pdf/I_PP4016.pdf

Notes:
- Takes the established idea that congestion exists and suggests solutions.
- Analyses the realistic blockers and provides realistic solutions which I really like. Although the solution isn't explored in great depth, they still seem feastible if city administration chooses to act on them.
- This doesn't involve simulation or data collection, but I like how this poses a different view of traffic congestion.
- We could take some of the solutions and try to simulate them to stretch the study further.
- Overall, a nice summary on Kathmandu's traffic congestion.
- **Cite for:** Koteshwor named as a high-congestion site; motorcycle + weak public transport as the problem; justification for bus-priority / modest demand-shift scenarios (not BRT construction).


### Effectiveness of Reversible Lane Systems in Kathmandu Valley: A Case Study of Jadibuti-Koteshwor Section

Link: https://www.researchgate.net/publication/357483999_Effectiveness_of_Reversible_Lane_Systems_in_Kathmandu_Valley_A_Case_Study_of_Jadibuti-Koteshwor_Section

Notes:
- They've managed to take the data from Jadibuti pool.
- We could use this data, because this is very close to our research area.
- They've explored the case of reversible lane which isn't useful to us, but still since the research area is very close, we could utilise this.
- **Cite for:** closest corridor; morning Jadibuti→Koteshwor heavier; evaluate with travel time + queue; Tinkune as downstream spillover. We do not copy their reversible-lane solution.