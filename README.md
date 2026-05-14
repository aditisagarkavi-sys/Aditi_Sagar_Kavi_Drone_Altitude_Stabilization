# Aditi_Sagar_Kavi_Drone_Altitude_Stabilization
This project focuses on the design and simulation of a Drone Altitude Stabilization System using both MATLAB and Simulink.
The objective is to maintain the drone at a desired altitude using a PID Controller and analyze the performance of both the open-loop and closed-loop control systems.


MATLAB Code:
% Drone Altitude Stabilization - PID Design
clc; clear; close all;

% Open-loop transfer function
num = [1];
den = [1 2 5];
G = tf(num, den);

% Display open-loop properties
disp('=== OPEN-LOOP SYSTEM ===');
figure;
step(G);
title('Open-Loop Step Response');
grid on;
info_open = stepinfo(G);
disp(info_open);
disp('Poles:');
disp(pole(G));

% Desired specs
zeta = 0.7;
wn = 2.5;

% PID gains
Kp = 4.5;
Ki = 2.0;
Kd = 1.8;

C = pid(Kp, Ki, Kd);

% Closed-loop transfer function
T = feedback(C*G, 1);

% Display closed-loop performance
disp('=== CLOSED-LOOP SYSTEM WITH PID ===');
figure;
step(T);
title('Closed-Loop Step Response with PID');
grid on;

info_closed = stepinfo(T);
disp('Step Info:');
disp(info_closed);

% Steady-state error
t = 0:0.01:10;
[y, t] = step(T, t);
ess = 1 - y(end);
disp(['Steady-state error: ', num2str(ess)]);

disp('PID Parameters:');
disp(struct('Kp',Kp,'Ki',Ki,'Kd',Kd));

% -----------------------------
% EXTRA: BOTH PLOTS TOGETHER
% -----------------------------
figure;
step(G, 'b', T, 'r', 10);
grid on;
title('Open-loop vs Closed-loop Response');
legend('Open Loop','Closed Loop');




