[//]: # (Image References)
[image_0]: img/img1.jpg
[image_1]: img/output_figure1.png
[image_2]: img/img2.png
[image_3]: img/img3.png
[image_4]: img/img4.png

[eqn1]: img/eqn1.png
[eqn2]: img/eqn2.png

# Control Engineering Lab Report II

The goal of the lab is to design full state feedback control of Spring-Mass-Damper System using **linear quadratic regulator (LQR)** and symmetric root locus.

![alt text][image_0]

## State Space Equations

State space equations of the Spring Mass Damper System is as follows:

![alt text][eqn1]

![alt text][eqn2]

## Step Response of Open loop Control

From the previous assignment, we can see our system step response of open loop control.

![alt text][image_1]

## Symmetric Root Locus

To find the symmetric root locus of the system, we must first calculate the transfer function of the system from state space equations. We can easily do this by using Matlab built-in functions as follows:

```
% initializing random constant values
F = 1;
m = 10;
k = 5;
b = 2;

% assigning matrices to variables A,B,C and D
A = [0 1; -k/m -b/m];
B = [0 ; F/m];
C = [1 0];
D = 0;

% creating state-space object
sys = ss(A,B,C,D);

% changing state-space eqns to transfer function
G = tf(sys);
```
Then we can use the Matlab statements to generate the SRL.

```
numerator = 0.1;
denominator = conv([1 0.2 0.5],[1 -0.2 0.5]);
sysGG = tf(numerator,denominator);
rlocus(sysGG)
```
![alt text][image_2]

Then, from the SRL, we choose K = [0.957 0.985] and N = 2.967. Then calculate the new system matrices:

```
A = A-B*K;
B = B*N;
```

After that, we'll check the response of the system from the block diagrams.

![alt text][image_3]

We can see that the response of the system is better than the open loop control.

![alt text][image_4]

## Conclusion

However, I randomly choose the constants of the system so the system is very non-linear and have many oscillations. In the output response, there are some overshoots and oscillations. We can improve this design by adding better controllers and compensators.

