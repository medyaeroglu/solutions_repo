# Problem 1
This project aims to explore the relationship between the range of a projectile and its angle of projection. Let's break it down into clear steps for both the theoretical and computational components, as well as the practical applications.

### 1. Theoretical Foundation

#### 1.1. Governing Equations

To derive the equations for projectile motion, we begin with Newton's second law in two dimensions, considering only the forces acting on the projectile (ignoring air resistance):

- The only force in the vertical direction is gravity, \( F_y = -mg \), where \( m \) is the mass of the projectile and \( g \) is the acceleration due to gravity.
- In the horizontal direction, there is no force acting, so \( F_x = 0 \).

We break down the motion into two components:
- **Horizontal motion**: The horizontal velocity remains constant throughout the flight since there is no horizontal acceleration. Thus:
  $$
  x(t) = v_0 \cos(\theta) t
  $$
  where \( v_0 \) is the initial velocity, \( \theta \) is the angle of projection, and \( t \) is time.

- **Vertical motion**: The vertical motion follows the equations of uniformly accelerated motion due to gravity:
  $$
  y(t) = v_0 \sin(\theta) t - \frac{1}{2} g t^2
  $$
  where \( v_0 \sin(\theta) \) is the initial vertical velocity.

#### 1.2. Time of Flight

To find the time it takes for the projectile to return to the ground, we set \( y(t) = 0 \) (i.e., when the projectile hits the ground). Solving the equation:
$$
0 = v_0 \sin(\theta) t - \frac{1}{2} g t^2
$$
gives the nontrivial solution:
$$
t = \frac{2v_0 \sin(\theta)}{g}
$$
This is the time of flight.

#### 1.3. Horizontal Range

The horizontal range \( R \) is the distance the projectile travels in the horizontal direction during its time of flight. Using the horizontal equation \( x(t) = v_0 \cos(\theta) t \) and substituting the time of flight:
$$
R = v_0 \cos(\theta) \left(\frac{2v_0 \sin(\theta)}{g}\right)
$$
Simplifying:
$$
R = \frac{v_0^2 \sin(2\theta)}{g}
$$
This equation describes the range of the projectile as a function of the initial velocity, gravitational acceleration, and angle of projection.

#### 1.4. Family of Solutions

By varying the parameters—initial velocity \( v_0 \), gravitational acceleration \( g \), and angle of projection \( \theta \)—we get a family of solutions for the range. For a fixed initial velocity, the range is maximized when \( \theta = 45^\circ \), since \( \sin(2\theta) \) achieves its maximum value of 1 at this angle.

### 2. Analysis of the Range

#### 2.1. Dependence on Angle of Projection

The equation \( R = \frac{v_0^2 \sin(2\theta)}{g} \) reveals that the range depends on the angle of projection through the function \( \sin(2\theta) \). This means:
- The range increases as the angle increases from 0° to 45°.
- Beyond 45°, the range decreases symmetrically, as \( \sin(2\theta) \) is symmetric about 45°.

#### 2.2. Influence of Initial Velocity and Gravitational Acceleration

- **Initial velocity**: The range increases quadratically with the initial velocity \( v_0 \). Doubling the initial velocity will quadruple the range, as \( R \propto v_0^2 \).
- **Gravitational acceleration**: The range is inversely proportional to the gravitational acceleration \( g \). A smaller gravitational acceleration (such as on the Moon) will result in a larger range.

### 3. Practical Applications

#### 3.1. Real-World Modifications

In real-world scenarios, air resistance, launch height, and terrain unevenness can significantly affect the trajectory:
- **Air resistance**: The drag force reduces the range. This would require solving the equations of motion with additional drag terms.
- **Launch height**: If the projectile is launched from an elevated position, the time of flight and range will both increase compared to a projectile launched from ground level.
- **Uneven terrain**: If the projectile lands on a surface that is not flat, the range calculation would need to account for the landing angle and height differences.

#### 3.2. Sports and Engineering

Projectile motion is frequently analyzed in sports (e.g., basketball, soccer) to optimize the trajectory for maximum distance or accuracy. In engineering, understanding projectile motion is crucial for designing missile trajectories or analyzing the behavior of fireworks.

### 4. Implementation

For the computational part, you can use Python with libraries such as `matplotlib` and `numpy` to simulate and visualize the projectile motion for different initial conditions.

#### 4.1. Python Script to Simulate Projectile Motion

```python
import numpy as np
import matplotlib.pyplot as plt

def projectile_motion(v0, angle, g=9.81):
    # Convert angle to radians
    angle_rad = np.radians(angle)
    
    # Time of flight
    t_flight = 2 * v0 * np.sin(angle_rad) / g
    
    # Time intervals
    t = np.linspace(0, t_flight, num=500)
    
    # Position equations
    x = v0 * np.cos(angle_rad) * t
    y = v0 * np.sin(angle_rad) * t - 0.5 * g * t**2
    
    return x, y, t_flight

def range_of_projectile(v0, g=9.81):
    # Maximum range occurs at 45 degrees
    angle = 45
    range = (v0**2 * np.sin(2 * np.radians(angle))) / g
    return range

# Parameters
v0 = 20  # initial velocity in m/s
angles = np.arange(0, 91, 5)  # angles from 0 to 90 degrees

# Plot range vs angle
ranges = [range_of_projectile(v0) for angle in angles]

plt.plot(angles, ranges)
plt.title('Range vs Angle of Projection')
plt.xlabel('Angle (degrees)')
plt.ylabel('Range (meters)')
plt.grid(True)
plt.show()
```

#### 4.2. Explanation of the Code
- The `projectile_motion` function simulates the trajectory of the projectile for a given initial velocity and angle.
- The `range_of_projectile` function calculates the range using the theoretical formula \( R = \frac{v_0^2 \sin(2\theta)}{g} \).
- We use `matplotlib` to visualize the range as a function of the launch angle.

### 5. Limitations and Future Improvements

This idealized model assumes no air resistance and flat terrain. For more accurate predictions:
- **Air resistance**: Implement drag force using the differential equation \( m \frac{d^2x}{dt^2} = -C_d A \frac{1}{2} \rho v^2 \), where \( C_d \) is the drag coefficient, \( A \) is the cross-sectional area, and \( \rho \) is the air density.
- **Variable terrain**: Simulate the effect of uneven terrain by introducing a height function for the ground.

### Deliverables:
- Python code for simulating projectile motion.
- Graph showing the range as a function of launch angle for various initial velocities.
- A discussion of real-world applications and suggestions for improving the model.

This project provides a clear understanding of the physics of projectile motion and allows for practical simulation and analysis.
