# Public-evacuation-model-based-on-network-flow-MCM2019-
public evacuation plan based on network flow
### refer to pdf for compelete Model report with Graphs
### Introduction
When an emergency occurs in a closed public space, its devastating effect can take thousands of lives away, causing considerable losses to public wealth. However, in most cases, the occurrence of an emergency is not the sentence to death but the poor emergency management and reaction mechanism. The chaos caused by the panic crowds fleeing in all directions can hinder the evacuation process and may block the way for the emergency personnel to get to the scene, carrying out their work. As a result, an effective and dedicated emergency evacuation plan should be designed for any public spaces, ensuring efficient responses that can help to minimize the losses.

Instead of considering individual choices of evacuation route, we primarily look at the evacuation plan from a macro perspective and think the personnel involved as a whole. We model the evacuation process by comparing it to the flow of networks. By analyzing the similarities and differences between our evacuation model and the typical flow network model,
 we make some adjustments to the flow network model and work out our evacuation model .
Then we start testing it on multiple scenarios, adjusting models accordingly with emphasizing on more detailed features. Further, we examine our model with the occurrence of random unexpected events, e.g., the existence of visitors with mobility difficulties, obstruction of evacuation routes. Our model eventually proves to have a real-time self-adjustment mechanism towards those unexpected situations and is robust in achieving its designed goal of minimizing the total evacuation time against any changes. We take the exact data from the Louvre as a test and analysis of our model and we also find this model’s general applicability to any crowded, public structure.

### Assumptions
* People are rational during the whole evacuation process and only follow the designated evacuation route as assigned
* People are generally viewed as being able to understand and follow the instructions from the security
* Each visitor moves at a consistent speed during the whole evacuation process
* People generally follow orders for evacuation
* We prioritize the evacuation by how close the rooms are from where the emergency happens as well as the depth of the room from the exit
* People always take the route away from where the emergency happens
* Hallways are modeled as rooms with same flow capacity in both ways
* We prioritize the evacuation of visitors inside the museum in our model

### Model specification 
The flow of crowds in an evacuation can be analogous to the flow network, which is a well- established model. Two inputs are required in this model, one is the flow network and the other is the ways that networks are connected. However, there exist some differences between the model we establish and the typical flow network model. In the typical flow network model, there are both inflow and outflow of people. Nevertheless, in the case of our evacuation model, though people can move in between the exhibition rooms, there is no inflow of people. At this point, we would like to keep evacuation personnel outside of our discussion, which we would address later.
### Model test by Louvre

This improvised model adopts the same logic of flow network as it is before, but by bring in the real-time quantified monitor on the remaining people in each evacuating room, it constantly rerun the previous model and brings the best route of evacuation at real-time. So each time with the rerunning, we would see a brand-new evacuation route. Now using the data we assigned for each flow network capacity, we regenerate the simulation with the additional estimate of the number of people in each room (Figure 10). In this simulation, we assume in the total 30 rooms, each has 200 people. So at the beginning of the evacuation, there are in total 6000 people in the Louvre. And the change of people inside the museum is plotted as the following applying the new model. The total amount of time for evacuation is 423s.

### Extending to general model
Although in the previous test cases, we only tested several specific cases including the Louvre, this model can be used much extensively. To be more precise, this model can be generally applicable to the evacuation plan of any public, crowded places with the following features:
* Any buildings, halls, or outdoor structures can be described by network models (can be described by structure of vertices and edges).
* The flow capacity of each edges are known or are able to be estimated.
* There exists accountable exits connected in the network.
* The amount of people in each vertex (or room) is known or able to be estimated.

### Sensitivity Test
In our previous model established, we consider a constant flow capacity for each network during the evacuation. However, in a real-life situation, unexpectancy happens such as disabled or injured people blocking the way, partial falling down of the ceiling, or multiple such events happening which would influence the flow capacity. We want to know how the total amount of evacuation time would fluctuate with the shift in flow capacity. To take the most cases into consideration, we here cover the following scenarios.
* Multiple change of flow capacity is considered
* Duration of each change of flow capacity is considered
* When each change of flow capacity happen is considered
* How much each flow capacity change is considered.

In order to run the sensitivity test, we give the following assumptions and set ranges for each variables we consider that may affect the optimal time for evacuation
* Each flow network has a 1% possibility of running into a flow capacity constraint situation
* The duration of each flow capacity constraint is any random integer in the range of 10- 30s
* The time for each flow capacity constraint is any random non-negative integer
* The parameter for the change of each flow capacity is any random number in the
range of 0.05-0.3

Below are two graphs showing the fluctuation of evacuation according to random parameters as listed above after running the algorithm 100 times and 1000 times.

The standard deviation of the 1000 times random test is 30.3405s, and the mean is 532.594s.

These statistics indicate that when an unexpectancy happens randomly, using our model, the optimized evacuation time would increase averagely by 109.594s. This suggests that when an unexpected situation such as a temporary obstruction happens, or any situation that affects the network capacity anywhere, the optimized evacuation time using our model would increase on average, yet does not fluctuate much according to how much or how bad the unexpectancies are. This is largely because our model is built upon the real-time situation processing and real- time evacuation plan adjustment. When any expectancies shift the original flow capacity in the network, the time for a specific room’s evacuation changes, and according to how the algorithm in our model works, this triggers a rerun of the model, thus correcting the current route for all room evacuation.

The sensitivity analysis shows how strong and flexible our model is in handling the real-time situation change, which is a constant occurrence in the real-life evacuation situation. It also shows how swift our model shifts in responding to the change in situation, thus optimizing in response to the change in the evacuation process.

### Strength and Weakness of our Model
#### Strength
1. Our model considers a dynamic evacuation process, allowing for a more comprehensive plan.
2. Our model can work flexibly for evacuation in any structures and perform real-time optimization.
3. Our model considers complex situation and unexpectancies and offers optimal solution accordingly.
4. Our algorithm is not computationally intensive and can be calculated for large data sets in a relatively short amount of time.
#### Weakness
1. Our model assumes that people move at constant speed generally and deal with unusual movements as friction of the model so that it does not offers solution if groups of people change their speed.
2. Our model gives priority to minimizing the amount of time it takes for all the personnel to evacuate, and only allows entry of emergency personnel when the flow capacity start to decrease from the maximum level. In other words, this model does not consider the circumstance where a certain type of incidents that prioritize the earliest arrival of emergency personnel over the fastest evacuation.
### Conclusion and Future Work
Our goal is to create a model (algorithm) to determine an optimal evacuation plan that minimizes the evacuation time for both the Louvre and any large, public and crowded structures. To accomplish this, we generate an algorithm that considers the following variables, the flow capacity, vertex connection, the number of people in each vertex, and the emergency spot. This algorithm provides a time-based comprehensive solution as to how many flow capacity should one vertex flow to other at a specific time spot. First, according to the layout of the vertices and how they are connected, we generate an adjacency matrix which shows the flow capacity and network relation in between vertices. Then we input the emergency spots and compute their depths. The vertex which has greater depth is assigned with higher priority to evacuate. Finally, we follow the priority to build the maximum flow and update state (amount of people) of vertices according to the time. Once we monitor that the vertices with the largest depth are fully evacuated, we detach them and rerun the model until all vertices are evacuated finally.

We also conduct a sensitivity analysis on our model, from which we find that our model, because of the real-time updating algorithm, are flexible in adjusting to different unexpectancies such as the unexpected block downs or the existence of disabled people constraining the normal network flow. And it is tested to handle multi occurrence of unexpectancy with different level of impact on the network flow. Besides, our model even offers the time range for the inflow of rescue personnel as it monitors the real-time flow at exits. Although our model is only tested on the Louvre case, it is versatile and has general applicability towards evacuation at multiple situations.

Our model mainly focuses on the macro arrangement of the crowds to provide the most feasible evacuation plans. Meanwhile, by monitoring the evacuation situation, our model adjusts itself to output the most efficient plan at realtime. However, in real life, human beings are unpredictable. People are not always rational, so there will be more unexpected issues happened. Although we have conducted sensitivity test to simulate the occurrence of unexpectancies during the evacuation process, it only uses an approximate rate to compute the probability of emergencies that happen. To be more precise, it is better to introduce a more micro model that can cooperate with the current model we have. For example, by using the simulated annealing model, we can predict the potential accidental rate dynamically
### Reference

[1] Research on The Large Public Place Evacuation Model,
https://wenku.baidu.com/view/10e9eb42e53a580217fcfebd.html

[2] Division of Maximum Flow, https://blog.csdn.net/M_AXSSI/article/details/50829795

[3] Mathematical Reflection of Wenchuan Earthquake,
https://wenku.baidu.com/view/3b3cab16c850ad02de8041fc.html

[4] Basis of Multiple flow network, https://www.cnblogs.com/victorique/p/8560656.html#autoid-1-2-0

[5] Max-flow, Min-cut Theorem, https://blog.csdn.net/yjr3426619/article/details/82715779

[6] 10.2 MM visitors to the Louvre in 2018, http://presse.louvre.fr/10-2-million-visitors-to-the- louvre-in-2018/

[7] Simulated Annealing Modeling, https://www.cnblogs.com/Qling/p/9326109.html
