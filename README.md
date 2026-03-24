# IIR-FILTER-DESIGN

# EXP 3 B: DESIGN OF LOW PASS CHEBYSHEV IIR FILTER USING BILINEAR TRANSFORMATION

# AIM: 

# To a design of low pass Chebyshev IIR filter using Bilinear Transformation.

# APPARATUS REQUIRED: 
PC installed with SCILAB. 

# PROGRAM: 
```
clc ; 
close ; 
wp=input('Enter the pass band frequency (Radians )= ' ); 
ws=input('Enter the stop band frequency (Radians )= ' ); 
alphap=input( ' Enter the pass band attenuation (dB)=' ); 
alphas=input( ' Enter the stop band attenuation(dB)=' ); 
T=input('Enter the Value of sampling Time='); 
 
//Pre warping- Bilinear Transformation 
omegap=(2/T)*tan(wp/2); 
disp(omegap,'omegap='); 
omegas=(2/T)*tan(ws/2); 
disp(omegas,'omegas=');

//Order of the filter  
N=acosh(sqrt(((10^(0.1*alphas))-1)/((10^(0.1*alphap))-1)))/(acosh(omegas/omegap)); 
disp(N,'N='); 
N=ceil(N); 
disp(N,'Round off value of N=');
 
//Cut off frequency 
omegac=omegap/(((10^(0.1*alphap)) -1)^(1/(2* N))); 
disp(omegac,'omegac=');
Epsilon = sqrt ((10^(0.1*alphap))-1);
disp(Epsilon,'Epsilon='); 
[pols ,gn] = zpch1(N, Epsilon,omegap ); 
disp(gn,'Gain'); 
disp(pols,'Poles'); 
hs=poly(gn,'s','coeff')/real(poly(pols,'s')); 
disp(hs,'Analog Low pass Chebyshev Filter Transfer function');
z=poly(0,'z');//Defining variable z 
Hz=horner(hs,(2/ T)*((z -1)/(z+1)))// Bilinear Transformation 
disp(Hz,'Digital LPF Transfer function H(Z)='); 
HW=frmag(Hz,512); // Frequency response 
w=0:%pi/511:%pi ; 
plot(w/%pi,abs(HW)); 
xlabel(' Normalized Digital Frequency w'); 
ylabel('Magnitude '); 
title(' Frequency Response of Chebyshev IIR LPF');
```
# CALCULATION:
![Chebyshev manual cal 1](https://github.com/user-attachments/assets/78ebe430-a9dd-4bd9-acd5-40b498320cfc)
![Chebyshev manual cal 2](https://github.com/user-attachments/assets/47de66b2-a223-4b36-805d-295bf73e5196)
![chebysev manual cal 3](https://github.com/user-attachments/assets/9437ff14-2f69-4df4-a74d-1322e10eeb57)
![Chebysev manual cal 4](https://github.com/user-attachments/assets/c42c2659-abd6-4b59-adff-f67b255bebb6)

# OUTPUT: 
CONSOLE WINDOW

<img width="826" height="995" alt="Chebysev calculation" src="https://github.com/user-attachments/assets/5f68cbe0-c8e6-4814-af05-63cf4569cd6b" />

GRAPH

<img width="757" height="706" alt="Chebysev Graph" src="https://github.com/user-attachments/assets/0cfa1b3c-4768-4088-9470-357a1b680c18" />

# RESULT: 
Thus design of Chebyshev Low pass IIR filter waveforms were plotted and output was
verified.
