# Mathematical Models
## Robot Model (Simulink)
<p align="center">
  <img src="Robot%20Model.jpeg" alt="Robot Model (Simulink)"style="width:90%; max-width:600px, height:90%;">
</p>

### Assembly and Movement


<p align="center">
  <img src="Robot%20Tree.jpeg" alt="Robot Tree (MATLAB)"style="width:40%; max-width:600px, height:40%;">
</p>
<p align="center">
  <img src="Robot%20Movement.png" alt="Robot Tree (MATLAB)"style="width:70%; max-width:600px, height:70%;">
</p>



## Forward Kinematics
### Simulink

<p align="center">
  <img src="Forward%20Kinematics%20Simulink.jpeg" alt="Forward Kinematics (Simulink)"style="width:90%; max-width:600px, height:90%;">
</p>

### MATLAB

```
% Forward Kinematics
% General DH Transformation Matrix
function T = DHTransformationMat(a, alpha, d, theta)
    T = [cos(theta) -sin(theta)*cos(alpha) sin(theta)*sin(alpha) a*cos(theta);
        sin(theta) cos(theta)*cos(alpha) -cos(theta)*sin(alpha) a*sin(theta);
        0 sin(alpha) cos(alpha) d;
        0 0 0 1];
end

syms theta1 theta2 theta3 ;
syms L1 L2 L3 L4 L5 L6;

% Robot DH Table
DH_table = [0,      0,      L1,     0;
            L3,     0,      L2,     theta1;
            0,      pi/2,   L4,     theta2;
            0,      pi/2,   L5,     theta3;
            0,      0,      L6,     0];

T01 = DHTransformationMat(DH_table(1, 1), DH_table(1, 2), DH_table(1, 3), DH_table(1, 4));
T12 = DHTransformationMat(DH_table(2, 1), DH_table(2, 2), DH_table(2, 3), DH_table(2, 4));
T23 = DHTransformationMat(DH_table(3, 1), DH_table(3, 2), DH_table(3, 3), DH_table(3, 4));
T34 = DHTransformationMat(DH_table(4, 1), DH_table(4, 2), DH_table(4, 3), DH_table(4, 4));
T45 = DHTransformationMat(DH_table(5, 1), DH_table(5, 2), DH_table(5, 3), DH_table(5, 4));

% Cumulative transformation matrices
T1 = T01;                  % Joint 1
T2 = T1 * T12;             % Joint 2
T3 = T2 * T23;             % Joint 3
T4 = T3 * T34;             % Joint 4
T5 = T4 * T45              % Joint 5 (End Effector)

T5 = simplify(T5)
```


## Inverse Kinematics (Simulink)

<p align="center">
  <img src="Inverse%20Kinematics%20Simulink.jpeg" alt="Inverse Kinematics (Simulink)"style="width:90%; max-width:600px, height:90%;">
</p>

## Jacobian

<p align="center">
  <img src="Jacobian%20Simulink.jpeg" alt="Inverse Kinematics (Simulink)"style="width:50%; max-width:600px, height:50%;">
</p>

## Trayectory
<p align="center">
  <img src="Trayectory%20Simulink.jpeg" alt="Inverse Kinematics (Simulink)"style="width:50%; max-width:600px, height:50%;">
</p>

## Robot's Reach / Range of Motion
The range of motion of the end effector, also known as robot's reach, can be found analytically but also demonstrated using software such as MATLAB:
<p align="center">
  <img src="Robot%20Reach.png" alt="Inverse Kinematics (Simulink)"style="width:70%; max-width:600px, height:70%;">
</p>
For this demonstration a sample of 10000 random robot configurations has been used to plot the end effector position at each of these configurations.
