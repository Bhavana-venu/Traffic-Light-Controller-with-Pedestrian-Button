#  Traffic Light Controller with Pedestrian Button (Verilog HDL)

##  Project Overview

This project implements a **Traffic Light Controller** using **Verilog HDL**.  
The system controls vehicle traffic signals and includes a pedestrian request button for safe road crossing.

The controller is designed as a **Moore Finite State Machine (FSM)** and verified through simulation using EDA Playground and GTKWave.

---

## System Architecture

The design consists of:

- Clock input  
- Reset input  
- Pedestrian button input  
- FSM-based control logic  
- Timer counter  
- Vehicle light outputs (Green / Yellow / Red)  
- Pedestrian light output (Red / Green)  

---

## FSM Design

This controller is implemented as a **Moore FSM**  
(Outputs depend only on the current state).

### State Encoding

| State | Encoding | Vehicle Light | Pedestrian Light |
|-------|----------|---------------|------------------|
| S0    | 00       | GREEN         | RED              |
| S1    | 01       | YELLOW        | RED              |
| S2    | 10       | RED           | RED              |
| S3    | 11       | RED           | GREEN            |

---

##  State Transitions

- **S0 → S1** : After `GREEN_TIME` expires  
- **S1 → S2** : After `YELLOW_TIME` expires  
- **S2 → S3** : If pedestrian request = 1  
- **S2 → S0** : If pedestrian request = 0  
- **S3 → S0** : After `PED_TIME` expires  

---

## Timing Parameters

```verilog
parameter GREEN_TIME  = 10;
parameter YELLOW_TIME = 5;
parameter RED_TIME    = 5;
parameter PED_TIME    = 8;
```

The timer resets whenever the state changes.

---

##  Pedestrian Request Handling

- When the pedestrian button is pressed, a `ped_request` signal is latched.
- The request is served during the RED state of vehicles.
- After pedestrian crossing (S3), the request is automatically cleared.
- This ensures even short button presses are not missed.

---

##  Testbench & Simulation

The testbench:

- Generates clock signal  
- Applies reset  
- Simulates pedestrian button press  
- Generates waveform file (`.vcd`)  
- Verifies correct state transitions  

###  Simulation Waveform

Add your waveform image in the repository and use:

```markdown
![Waveform](waveform.png)
```

---

## Block Diagram

Add your block diagram image in the repository and use:

```markdown
![Block Diagram](block_diagram.png)
```

---
---

##  State Diagram

![State Diagram](state_diagram.png)



##  Tools Used

- Verilog HDL  
- EDA Playground  
- GTKWave  

---

##  Learning Outcomes

- Moore FSM design  
- Timer-based control logic  
- Synchronous state machine implementation  
- Testbench development  
- Waveform analysis  

---

##  Future Improvements

- Add 7-segment countdown display  
- Add emergency vehicle override  
- Parameterize timing values  
- Implement on FPGA board  

---

## Repository Structure

```
traffic_light_controller.v
tb_traffic_light_controller.v
README.md
waveform.png
block_diagram.png
```

---

##  Author

**Bhavana A**  
Electronics and Communication Engineering  

---

 This project demonstrates practical implementation of an FSM-based control system using Verilog HDL.
