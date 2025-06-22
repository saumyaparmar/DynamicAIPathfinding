# AI Pathfinding with Dynamic Obstacles using A* and Flow Field Algorithms

This project showcases a dynamic AI pathfinding system developed in Unity, integrating multiple pathfinding techniques to create intelligent and realistic agent behaviors. The player character utilizes the A* pathfinding algorithm to navigate through an environment filled with obstacles, responding to mouse clicks.

Inspired by _A Plague Tale: Innocence_ by Asobo Studios, a rat swarm AI system is implemented using a combination of single-goal flow fields and boid-based local movement behaviors. The rats are attracted to the player (who holds a torch) while avoiding light sources in the environment, which act as repulsive dynamic obstacles. When the rats aren’t chasing the player, they demonstrate natural wandering behavior through custom AI algorithms.

This hybrid approach combines goal-driven flow fields, local avoidance, and group dynamics, creating a responsive and immersive AI experience. The system adapts to player movement, making it ideal for real-time game environments that require complex, dynamic AI pathfinding.

[YOUTUBE LINK TO DEMO](https://youtu.be/Exb5lNoAV9Y?si=_Js-mx4dGaEeYzhg)


[LINK TO BUILD EXECUTABLE](https://drive.google.com/file/d/1vWgNkWoEk6IvHWHAB0tKlxFfcuJz4W2C/view?usp=sharing)

I don't provide codes for my project online, this is just to explain in an overview what tehcniques I have used to implement this project.

If you want a detailed research document about my project here is the link😃 : 

[RESEARCH DOCUMENT LINK](https://drive.google.com/file/d/1RPDCTwuyIj0FDKya6IPvtPuAcMLKsa41/view?usp=drive_link) 



## Introduction
The project was created in Unity and is centred around two main systems. The first is a standard A* pathfinding implementation, used by a player-controlled character to navigate around obstacles which is inspired by _RuneScape_. The second is a swarm-based AI inspired by the behaviour of rats in _A Plague Tale: Innocence_. These agents pursue the player using a single-goal flow field algorithm, while actively avoiding light sources that dynamically appear in the environment.

To add realism to the swarm movement, a Boids-based flocking system is also implemented. This enables the rats to move as a group and surround the player, simulating natural coordination within the swarm.

The goal of this project is to explore how different AI techniques—individual pathfinding, flow field navigation, dynamic avoidance, and flocking behaviour—can be combined to create believable and responsive agent behaviour in real-time. The system also serves as an educational tool to better understand the strengths and limitations of each technique, especially when applied to dynamic environments and goal-driven behaviour.


## Technical Overview  

### (a) A* Pathfinding
A* (A-Star) is a widely used graph traversal and pathfinding algorithm in games and simulations, designed to efficiently find the shortest path between two points. It operates by evaluating nodes based on two costs: the actual cost from the starting node (G-cost) and an estimated cost to the goal (H-cost), known as the heuristic. Common heuristics include Manhattan, Diagonal, or Euclidean distance, depending on the grid structure and movement constraints.

In this project, A* is used to control the movement of the player character within a grid-based environment containing dynamic obstacles. As the environment changes, the path is recalculated to adapt to new conditions. 

The player moves using a "click-to-move" mechanic, similar to that seen in _RuneScape_, allowing for intuitive control while showcasing the responsiveness of the pathfinding system in real time.
<p align="center">
  <img src="https://github.com/user-attachments/assets/39628dac-b16c-4d96-8635-c908437d52d0">
</p>

### (b) Flow Field Pathfinding
Flow field pathfinding is a technique designed to efficiently guide large numbers of agents toward a common target. Unlike traditional algorithms such as A*, which calculate a separate path for each individual agent, a flow field generates a global vector map across the environment. Each cell in this map contains a direction vector that points toward the goal, allowing agents to simply follow the flow to navigate.

In this project, the flow field is centred on the player's position, who serves as the dynamic goal while holding a torch. The rat agents continuously follow the generated vectors, allowing them to move fluidly and adapt in real time as the player's location changes. Since all agents share the same vector field, this approach enables scalable and coordinated swarm behaviour with minimal computational overhead.

While flow field navigation may not produce paths as precise as A*, it is significantly more efficient in high-agent scenarios. In this case, with over 500 rat agents active at once, generating individual paths for each would be computationally expensive. The flow field system offers a practical and performant solution for crowd-level navigation, making it well-suited for this type of swarm-based AI.

<p align="center">
  <img src="https://github.com/user-attachments/assets/e6724abb-a8d4-427f-b61d-054ae71bd1fe">
</p>

### (c) Boids Flocking Behavior
The Boids algorithm, created by Craig Reynolds, is often used to simulate the natural movement of groups like birds or fish. It’s based on three simple behaviours: _separation_ (to avoid crowding), _alignment_ (to match direction with neighbours), and _cohesion_ (to stay close to the group).

In this project, I have only used **separation** and **alignment**. Since the flow field already keeps the rats moving in the same general direction and close to each other, the cohesion behaviour isn’t necessary. The flow field handles the global movement toward the player, while the Boids logic helps manage how the rats behave in relation to each other locally.

By combining these two systems (Flowfield and Boids), the rats can move as a swarm—following the player while still avoiding collisions and adjusting to each other’s movement. This creates more natural and believable group behaviour without needing to calculate a full path or apply complex coordination rules for every individual rat.

In this project, the Boids system is integrated into the rat AI to simulate realistic surrounding of player, where it blends with flowfield at the same time have a swarm type behaviour of approaching the goal, in this case the player. 

<p align="center">
  <img src="https://github.com/user-attachments/assets/0c308f6d-9b8f-4031-83d0-2b03ebd0a6f6">
</p>


### (d) Light Avoidance Logic
To make the rat AI feel more reactive and believable, this project includes a light avoidance system inspired by the behaviour seen in _A Plague Tale: Innocence_.

Instead of treating light as a hard barrier, the system encourages rats to move away from it by modifying the directions in the flow field.

When a light source is active, the system finds all grid cells within a certain radius around the light, based on its range. It then calculates outward-facing vectors for those cells—essentially telling the rats to move away from the light. 

These repulsion vectors are combined with the normal flow field directions (which point toward the player), so the final direction for each rat is influenced by both the goal and the nearby light.

<p align="center">
  <img src="https://github.com/user-attachments/assets/15471cd6-67c7-44b4-a015-fa01274e0b0e">
</p>


