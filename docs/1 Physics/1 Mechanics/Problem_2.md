# Problem 2
The **forced damped pendulum** provides a fascinating example of nonlinear dynamics, showcasing behaviors such as resonance, chaotic motion, and quasiperiodicity. This is especially important for understanding systems that experience periodic driving forces, damping, and restoring forces. Let's break down the task into clear steps, covering both theoretical foundations and computational analysis.

### 1. Theoretical Foundation

#### 1.1. Differential Equation of the Forced Damped Pendulum

The motion of a forced damped pendulum is described by the second-order differential equation:
$$
\frac{d^2 \theta}{dt^2} + 2\zeta \frac{d\theta}{dt} + \omega_0^2 \sin(\theta) = A \cos(\omega t)
$$
Where:
- \( \theta(t) \) is the angular displacement of the pendulum.
- \( \zeta \) is the damping coefficient.
- \( \omega_0 \) is the natural frequency of the undamped system.
- \( A \) is the amplitude of the external driving force.
- \( \omega \) is the frequency of the external driving force.

For small angles, \( \sin(\theta) \approx \theta \), and the equation simplifies to:
$$
\frac{d^2 \theta}{dt^2} + 2\zeta \frac{d\theta}{dt} + \omega_0^2 \theta = A \cos(\omega t)
$$

This is a second-order linear differential equation describing damped harmonic motion with an external periodic driving force. The parameters \( \zeta \), \( \omega_0 \), and \( \omega \) significantly influence the system's behavior.

#### 1.2. Small-Angle Approximation and Solutions

For small angles, we approximate the pendulum's motion as a linear oscillator. The solution to this differential equation can be found using standard methods for forced damped oscillators. For example, the general solution for the displacement \( \theta(t) \) is:
$$
\theta(t) = \theta_{\text{steady}} + \theta_{\text{transient}}
$$
Where:
- \( \theta_{\text{steady}} \) is the steady-state solution, which is the solution to the forced term.
- \( \theta_{\text{transient}} \) decays over time due to damping.

The steady-state solution is given by:
$$
\theta_{\text{steady}} = \frac{A}{\sqrt{(\omega_0^2 - \omega^2)^2 + (2\zeta \omega)^2}} \cos(\omega t - \delta)
$$
Where \( \delta \) is the phase shift and depends on \( \omega \), \( \omega_0 \), and \( \zeta \).

#### 1.3. Resonance Conditions

Resonance occurs when the driving frequency \( \omega \) is equal to the natural frequency of the pendulum \( \omega_0 \). At resonance, the amplitude of oscillation can grow without bound, leading to large oscillations. This phenomenon happens when the damping is small enough to allow for energy accumulation from the driving force.

### 2. Analysis of Dynamics

#### 2.1. Effect of Damping, Amplitude, and Frequency

The behavior of the pendulum depends on the values of the damping coefficient \( \zeta \), the amplitude of the driving force \( A \), and the driving frequency \( \omega \):
- **Damping**: If the damping coefficient \( \zeta \) is small, the pendulum will oscillate for a long time. As \( \zeta \) increases, the oscillations decay more quickly.
- **Driving Amplitude**: A larger driving amplitude \( A \) leads to larger oscillations at resonance.
- **Driving Frequency**: The frequency \( \omega \) determines whether the system is in resonance. When \( \omega \) matches \( \omega_0 \), resonance occurs, leading to large oscillations. For \( \omega \) far from \( \omega_0 \), the system oscillates with smaller amplitudes.

#### 2.2. Transition to Chaos

When the driving frequency or amplitude exceeds certain thresholds, the system may exhibit chaotic behavior. This can be analyzed by plotting phase portraits, Poincaré sections, and bifurcation diagrams to visualize the transition from periodic to chaotic motion.

### 3. Practical Applications

The forced damped pendulum model applies to a variety of real-world systems:
- **Energy Harvesting**: The concept of resonance can be exploited in energy harvesting devices, where the system is tuned to vibrate at the frequency of an external periodic force (e.g., wind or human motion).
- **Vibration Isolation**: Suspension systems in vehicles or buildings are designed to avoid resonant frequencies that could amplify oscillations.
- **Oscillating Circuits**: In electrical circuits, driven RLC circuits behave similarly to forced damped pendulums, with resonance leading to high currents and potential damage.

### 4. Implementation

We will now implement a computational model to simulate the forced damped pendulum's motion, explore its behavior under various conditions, and visualize the results.

#### 4.1. Python Code Implementation

We'll use the Runge-Kutta method to solve the differential equation numerically. Here's an implementation using Python:

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp

# Parameters
omega_0 = 2.0       # Natural frequency (rad/s)
zeta = 0.1         # Damping coefficient
A = 1.0            # Driving amplitude
omega = 2.0        # Driving frequency
theta_0 = 0.1      # Initial angle (rad)
theta_dot_0 = 0    # Initial angular velocity (rad/s)

# Differential equation for the forced damped pendulum
def damped_pendulum(t, y):
    theta, theta_dot = y
    dtheta_dt = theta_dot
    dtheta_dot_dt = -2 * zeta * omega_0 * theta_dot - omega_0**2 * theta + A * np.cos(omega * t)
    return [dtheta_dt, dtheta_dot_dt]

# Time array
t_span = (0, 100)  # Time span for simulation
t_eval = np.linspace(t_span[0], t_span[1], 10000)

# Initial conditions: [theta_0, theta_dot_0]
y0 = [theta_0, theta_dot_0]

# Solve the differential equation
sol = solve_ivp(damped_pendulum, t_span, y0, t_eval=t_eval)

# Plot the angular displacement vs time
plt.figure(figsize=(10, 6))
plt.plot(sol.t, sol.y[0], label='Theta(t)', color='b')
plt.title('Forced Damped Pendulum - Angular Displacement vs Time')
plt.xlabel('Time (s)')
plt.ylabel('Angular Displacement (rad)')
plt.grid(True)
plt.legend()
plt.show()

# Phase plot (theta vs theta_dot)
plt.figure(figsize=(10, 6))
plt.plot(sol.y[0], sol.y[1], label='Phase plot', color='r')
plt.title('Phase Portrait of Forced Damped Pendulum')
plt.xlabel('Theta (rad)')
plt.ylabel('Theta dot (rad/s)')
plt.grid(True)
plt.legend()
plt.show()
```

#### 4.2. Explanation of the Code

- The `damped_pendulum` function defines the system of differential equations for the forced damped pendulum.
- The `solve_ivp` function from `scipy.integrate` is used to numerically solve the system.
- The results are plotted as:
  - **Angular displacement vs time** to observe the time evolution of the pendulum.
  - **Phase portrait** (theta vs. theta-dot) to explore the motion's dynamics.

#### 4.3. Additional Visualizations

You can generate **Poincaré sections**, **bifurcation diagrams**, and **phase portraits** by modifying the code and examining the system's behavior for different values of \( \zeta \), \( A \), and \( \omega \).

### 5. Limitations and Extensions

- **Nonlinear Damping**: A more realistic model could include nonlinear damping, where the damping force depends on the velocity in a nonlinear way (e.g., \( F_{\text{damp}} = -b \cdot v^n \)).
- **Non-periodic Forcing**: Introducing non-periodic forces, such as random noise or impulses, would further diversify the system's behavior and could simulate real-world environments better.
- **Higher-Dimensional Systems**: Coupling the pendulum with other systems or adding more degrees of freedom could lead to even more complex behaviors (e.g., multiple pendulums, nonlinear coupled oscillators).

### Deliverables:
- Python script simulating the forced damped pendulum.
- Plots of the pendulum’s motion and phase diagrams for different parameters.
- Discussion of resonance, chaotic behavior, and applications of the model in engineering.

This investigation gives you a deep understanding of forced damped oscillations and provides a platform for exploring complex dynamics in physical systems.