
# Closed-Loop Speed Control of a DC Motor using PID Controller

## 1\. Overview

This project implements a closed-loop speed control system for a separately excited DC motor using a PID controller in MATLAB/Simulink. The model is built using Simscape Electrical components to simulate the motor's dynamics accurately.

The primary goal is to **tune the PID controller** to achieve a robust and efficient response. The controller must:

  * Track a reference speed setpoint (1750 rad/s).
  * Reject a constant load torque (10 Nm).
  * Maintain stability despite a sinusoidal disturbance added to the error signal.

## 2\. Simulink Model

The Simulink model consists of a DC motor block, a PID controller, and various signal inputs.

  * **DC Motor:** A separately excited DC motor model from the Simscape library.
  * **PID Controller:** A continuous-time `PID(s)` block that regulates the armature voltage based on the speed error.
  * **Inputs:**
      * **Reference Speed:** A constant block set to `1750` rad/s.
      * **Load Torque (TL):** A constant block set to `10` Nm, applied to the motor shaft.
      * **Disturbance:** A sine wave generator adds noise to the error signal before it enters the PID, testing the controller's robustness.
  * **Feedback:** The motor's angular velocity (`wm` in rad/s) is fed back and compared with the reference speed to generate the error signal.

-----

## 3\. Controller Tuning and Performance

The Simulink PID Tuner tool was used to optimize the controller's gains. The "Block" response refers to the initial, untuned parameters, while the "Tuned" response refers to the optimized parameters.

### Controller Parameters

| Parameter | Block (Initial) | Tuned (Optimized) |
| :--- | :--- | :--- |
| **P** | 1 | 0.2146 |
| **I** | 1 | 5.2665 |
| **D** | 0 | 0.0021659 |
| **N** | 100 | 5488.4368 |

### Performance and Robustness

The tuning resulted in a significant improvement in the system's dynamic response.

| Metric | Block (Initial) | Tuned (Optimized) |
| :--- | :--- | :--- |
| **Rise time** | 0.0116 s | 0.034 s |
| **Settling time** | 1.69 s | **0.153 s** |
| **Overshoot** | 37.1% | **5.41%** |
| **Phase margin** | 26.1 deg | **64.5 deg** |

-----

## 4\. Simulation Results and Waveforms

### Step Plot: Reference Tracking

This plot compares the step response of the initial (dashed) and tuned (solid) controllers. The tuned controller clearly eliminates the high overshoot and settles much faster.

### Final Simulation Output

This scope plot shows the final performance of the **tuned controller** in the main simulation. The blue line (motor speed) successfully tracks the white line (reference speed of 1750 rad/s), quickly stabilizing despite the constant load and signal disturbances.

## 5\. Conclusion

The tuned PID controller (P=0.2146, I=5.2665, D=0.0021659) successfully controls the DC motor's speed. It demonstrates excellent reference tracking and disturbance rejection, reducing **overshoot from 37.1% to 5.41%** and **settling time from 1.69s to 0.153s**. The high phase margin (64.5°) confirms the system is highly stable and robust.# DC-Motor-Speed-Control-using-PID-Controller
