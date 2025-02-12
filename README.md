# Multi-Agent Autonomous Waste Collection System

This project was developed for the "Introduction to Intelligent Autonomous Systems" course and aims to **design and implement a decentralized waste collection system using Multi-Agent Systems (MAS) with SPADE**. The system will **simulate autonomous garbage trucks** (agents) that **collaborate to efficiently collect waste** from various locations within a city, **responding dynamically to changes in waste levels and traffic conditions**. First Semester of the Third Year of the Bachelor's Degree in Artificial Intelligence and Data Science.

<br>

## Programming Language:

<div style = "display: inline_block"><br/>
  <img align="center" alt="python" src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" />
</div><br/>

<br>

## Requirements:

	- python -> version 3.9.13
	- prosody
	- spade
	- pygame (for the interface)

To configure **Prosody**, locate and open the config file 'prosody.cfg.lua', you can just copy what's on the 'prosody.txt' file. 

<br>

## The Project
As you can see, this project is a decentralized waste collection system that uses Multi-Agent Systems (MAS) enabled by SPADE, in which we have to take into account the following:

1.  **Truck Agents:**  Each truck is represented by an agent responsible for collecting waste from assigned areas. Agents should be <u>capable of detecting the fill level of waste bins in their vicinity and making decisions on whether to collect waste based on their current capacity, battery/fuel level, and proximity</u>.
2.  **Bin Agents:**  Waste bins can also be represented by agents that <u>periodically report their fill levels to nearby truck agents</u>. They will trigger a collection request when they reach a specified threshold.
3.  **Decentralized Decision-Making:**  The system is decentralized, meaning <u>each truck agent makes its own decisions</u> about when to collect waste, where to go next, and how to optimize its route, without relying on a central controller. <u>Agents communicate with each other to avoid overlapping collection areas and ensure city-wide coverage</u>.
4.  **Dynamic Environment:**  The environment should include dynamic elements like <u>changing traffic conditions, roadblocks, and variable waste production levels</u>. Truck agents need to <u>adjust their routes in real time</u> based on these conditions.
5.  **Task Allocation and Collaboration:**  Implement a <u>negotiation or task allocation protocol</u> (e.g., Contract Net Protocol) that allows truck agents to share responsibilities, hand off tasks to nearby agents when overloaded, and ensure efficient coverage of all waste bins.
6.  **Resource Management:**  Each truck has <u>limited resources</u>, such as fuel or battery life and waste capacity. Agents need to plan efficient routes to minimize fuel consumption and maximize waste collected per trip. They also need to <u>return to a central depot to unload waste or recharge when needed</u>.
7.  **Optimization Metrics:**  The system should track the following metrics to evaluate performance:

-   Total waste collected
-   Average collection time for each bin
-   Total fuel consumption or battery usage
-   Distance traveled by each truck agent
-   Efficiency of collaboration and task allocation between agents

8.  **Fault Tolerance:**  The system should be able to <u>handle scenarios where some agents fail or go offline (e.g., a truck breaking down)</u>. Remaining agents should <u>redistribute tasks</u> to ensure uninterrupted waste collection.

<br>

### The Agents Implementations:

**Bin Agent**
- **Waste Monitoring:** Tracks and increases waste levels in bins.
- **Collection Request:** Sends a CFP to Truck Agents when bins are ≥70% full. 
-  **Proposal Evaluation:** Analyzes truck proposals to choose the best option based on cost, capacity, and availability. 
- **Problem Resolution:** Resends CFPs if no truck responds. If a responding truck breaks down, it notifies the bin to wait for reassignment. After a delay, the bin resends CFPs if there aren’t trucks available.

<br>

**Truck Agent**

- **Proposal Generation**  Responds to CFPs with cost, fuel, and capacity.
- **Route Planning:** Calculates the shortest path dynamically using Dijkstra’s algorithm, considering real-time traffic conditions. 
- **Waste Collection:** Navigates to bins, collects waste, and updates its load status. 
- **Resource Management:** Manages fuel, waste load, and capacity; returns to the depot when resources are low. 
- **Fault Tolerance:** Reallocates tasks to other trucks during breakdowns or emergencies 
- **Exploration:** A truck can choose to explore the environment and go to a bin

<br>

### Agents Communication:

**Between Trucks:**
1. **Allocation of other trucks:** If truck1 was on its way to collect the trash from a CFP and in the middle of the path it breaks down, the truck1 communicates with other trucks and they decide wich one should go, if they have availability to do so. 
2. **Claims:** When a truck shows interess to go to one bin, the truck sends a Claim to every other truck and he gets an answer from them to check if he is indeed the best truck to complete the collection. The winning truck claims the bin for himself. 
3. **Decline Claim:** A truck can deny the acessability of other trucks when they want to claim a bin. 
4. **Release Bin:** A truck can indicate to other trucks, after he collects the trash or if the truck for some reason was not able to reach the bin as he planned, that he released the bin that he once claimed .

<br>

**Between Trucks and Bins:**
<p align="center">
  <img width="850" height="400" src="https://github.com/user-attachments/assets/9fb738a8-bb29-4e7f-94b6-c292090f5ac3">
</p>

<br>

## Tests:
We realized 3 tests beeing them:
- **Test 1:** Basic Environment with Constant Waste Accumulation
- **Test 2:** Basic Environment with Different Waste Accumulation
- **Test 3:** Dynamic Environment with Different Waste Accumulation
In all tests the trucks could break down at anytime. With Dynamic Environment we mean that traffic conditions and road blocks were used. You can see the results of the test on the pdf file.

These were the two layouts we tested on:

<p align="center">
  <img width="850" height="400" src="https://github.com/user-attachments/assets/2adcc256-7f31-454d-a52d-d3048a5a2b64">
</p>

<br>

## The Interface:
When running 'interface.py' you will get to choose the size of the environment. Then you can do the following by pressing the controls:
B + Click -> You create a **bin** on the square you clicked;
T + Click -> You create a **truck** on the square you clicked;
R + Click -> You create a **roadblock** on the square you clicked;
1 -> You set traffict level to 1;
2 -> You set traffict level to 2;
3 -> You set traffict level to 3;
4 -> You set traffict level to 4;
5 -> You set traffict level to 5;
0 -> You set traffict level to 0 (clear all traffic);
S -> You **START** the program

**Notes:** 
- When you create traffic you only define how much traffic is going to be created, you can't choose where as it is generated randomly.
- Traffic is represented as an orange line
- Roadblocks are red squares
-  The truck with a semi red square on top of it is broken by a random time, when it is operational again the square will disappear. 
- Trucks can break down at any time and randomly, you can't controle it. 
- The blue square is the central
- On the right side you have the status were you can see de capacity of each bin (the color changes accordingly) and the capacity of trucks and its fuel

<br>

<p align="center">
  <img width="850" height="400" src="https://github.com/user-attachments/assets/4a73e465-0e3f-4f76-9eaa-ce93dcd89b8b">


<br>

## About the repository:

- Assignment.pdf ➡️Project statement
- bin_agent.py ➡️ The code of the bin agent;
- truck_agent.py ➡️ The code of the truck agent;
- environment.py ➡️ The code of the environment;
- interface.py ➡️ The code of the interface;
- prosody.txt ➡️ How your 'prosody.cfg.lua' should be;
- Multi-Agent-Autonomous-Waste-Collection-System.pdf ➡️ The tests and its results and more info about what was done.

<br>

## Link to the course: 

This course is part of the **<u>first semester</u>** of the **<u>third year</u>** of the **<u>Bachelor's Degree in Artificial Intelligence and Data Science</u>** at **<u>FCUP</u>** and **<u>FEUP</u>** in the academic year 2024/2025. You can find more information about this course at the following link:

<div style="display: flex; flex-direction: column; align-items: center; gap: 10px;">
  <a href="https://sigarra.up.pt/fcup/pt/ucurr_geral.ficha_uc_view?pv_ocorrencia_id=529876">
    <img alt="Link to Course" src="https://img.shields.io/badge/Link_to_Course-0077B5?style=for-the-badge&logo=logoColor=white" />
  </a>

  <div style="display: flex; gap: 10px; justify-content: center;">
    <a href="https://sigarra.up.pt/fcup/pt/web_page.inicial">
      <img alt="FCUP" src="https://img.shields.io/badge/FCUP-808080?style=for-the-badge&logo=logoColor=grey" />
    </a>
    <a href="https://sigarra.up.pt/feup/pt/web_page.inicial">
      <img alt="FEUP" src="https://img.shields.io/badge/FEUP-808080?style=for-the-badge&logo=logoColor=grey" />
    </a>
  </div>
</div>
