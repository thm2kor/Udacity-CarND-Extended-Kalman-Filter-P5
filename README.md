# Extended Kalman Filter Project

[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

The objective of this project is to estimate the state of a moving object with noisy measurements from lidar and radar sensors. The state of the moving object is represented by two dimensional position p<sub>x</sub>, p<sub>y</sub> and two dimensional velocity v<sub>x</sub>, v<sub>y</sub>. The **state vector** <img src="https://latex.codecogs.com/gif.latex?\mathit{x}"/> is therefore:
<img src="https://latex.codecogs.com/gif.latex?\begin{pmatrix}p_x\\p_y\\v_x\\v_y\end{pmatrix}"/>

**Process Noise:** The uncertainty in the *prediction step*, represented as <img src="https://latex.codecogs.com/gif.latex?\mathit{\nu}"/>, is a gaussian distribution with mean 0 and covariance Q  <img src="https://latex.codecogs.com/gif.latex?\[\nu\sim&space;N(0,Q)\]"/>

**Measurement Noise:** The uncertainty in *sensor measurement*, represented as <img src="https://latex.codecogs.com/gif.latex?\mathit{\omega}"/>, is a gaussian distribution with mean zero and covariance R  <img src="https://latex.codecogs.com/gif.latex?\[\omega\sim&space;N(0,R)\]"/>



**Process covariance matrix - Q**

**State transition matrix - F**

Based on the **kinematics equations** of an object in motion, the new 2D position and 2D velocity can be estimated with the following equations:<br>
<img src="https://latex.codecogs.com/gif.latex?\acute{p_x}={p_x}&plus;{v_x}\Delta&space;t&plus;\frac{a_{x}\Delta&space;t&space;^2}{2}"/><br>
<img src="https://latex.codecogs.com/gif.latex?\acute{p_y}={p_y}&plus;{v_y}\Delta&space;t&plus;\frac{a_{y}\Delta&space;t&space;^2}{2}"/><br>
The velocity along x and y directions remains the same. <br>
<img src="https://latex.codecogs.com/gif.latex?\acute{v_x}={v_x}&plus;{a_x}\Delta&space;t"/><br>
<img src="https://latex.codecogs.com/gif.latex?\acute{v_y}={v_y}&plus;{a_y}\Delta&space;t"/><br>

where <img src="https://latex.codecogs.com/gif.latex?\\{a_x}"/> and <img src="https://latex.codecogs.com/gif.latex?\\{a_y}"/> are random acceleration vectors with mean 0 and standard deviations  <img src="https://latex.codecogs.com/gif.latex?\sigma_{a_x}^{2}"/> and <img src="https://latex.codecogs.com/gif.latex?\sigma_{a_y}^{2}"/> respectively.

Based on the above noise vector, the complete noise variance matrix Q is :

<img src="https://latex.codecogs.com/gif.latex?Q=\begin{pmatrix}\frac{\Delta&space;t&space;^2}{4}\sigma_{a_x}^{2}&space;&&space;0&space;&&space;\frac{\Delta&space;t&space;^3}{2}\sigma_{a_x}^{2}&space;&&space;0&space;\\&space;0&space;&&space;\frac{\Delta&space;t&space;^2}{4}\sigma_{a_y}^{2}&space;&&space;0&space;&&space;\frac{\Delta&space;t&space;^3}{2}\sigma_{a_y}^{2}\\&space;\frac{\Delta&space;t&space;^3}{2}\sigma_{a_x}^{2}&space;&&space;0&space;&&space;{\Delta&space;t&space;^2}\sigma_{a_x}^{2}&space;&&space;0\\&space;0&space;&&space;\frac{\Delta&space;t&space;^3}{2}\sigma_{a_y}^{2}&space;&&space;0&space;&&space;{\Delta&space;t^2}\sigma_{a_y}^{2}&space;\end{pmatrix}"/>

**H matrix** projects the belief about the object's current state into the measurement space of the sensor.

**Measurement Noise Covariance Matrix R** represents the uncertainty in our sensor measurements.

For every new measurement from a radar or lidar sensor, the following two steps are carried out:
- Estimation function is triggered.
  - At the first iteration of measurement, state transition matrix and covariance matrix are initialized
