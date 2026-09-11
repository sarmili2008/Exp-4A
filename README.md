# Design-of-FIR-Filters-using-rectangular-window
#          DESIGN OF FIR DIGITAL FILTERS USING RECTANGULAR WINDOW
# AIM: 
          
  To generate design of low pass FIR digital filter using SCILAB 

# APPARATUS REQUIRED: 

  PC Installed with SCILAB 

# PROGRAM for LPF:
clc;
clear;
close;

// FIR LOW PASS FILTER USING RECTANGULAR WINDOW

// Input from user
N = evstr(input("Enter number of samples: ", "string"));
wc_value = evstr(input("Enter cutoff frequency in pi: ", "string"));

// Convert cutoff frequency
Wc = wc_value * %pi;

// Sample index
n = 0:N-1;

// Alpha
alpha = (N-1)/2;

// Initialize
hd = zeros(1,N);

// Ideal Low Pass Filter
for k = 1:N
    x = n(k) - alpha;

    if x == 0 then
        hd(k) = Wc/%pi;
    else
        hd(k) = sin(Wc*x)/(%pi*x);
    end
end

// Rectangular Window
w = ones(1,N);

// FIR coefficients
h = hd .* w;

// Display
disp("FIR LOW PASS FILTER COEFFICIENTS:");
disp(h);

// Impulse Response
subplot(2,1,1);
plot2d3(n,h);
xlabel("n");
ylabel("h(n)");
title("Impulse Response");

// Frequency Response
M = 500;
omega = linspace(0,%pi,M);
H = zeros(1,M);

for k = 1:M
    for m = 1:N
        H(k) = H(k) + h(m)*exp(-%i*omega(k)*n(m));
    end
end

// Magnitude
Hmag = abs(H);

// Frequency Response Plot
subplot(2,1,2);
plot(omega,Hmag);
xlabel("Frequency (rad/sample)");
ylabel("Magnitude");
title("FIR Low Pass Filter - Frequency Response");

HPF:
clc;
clear;
close;

// FIR HIGH PASS FILTER USING RECTANGULAR WINDOW

// Input
N = evstr(input("Enter number of samples N: ", "string"));
wc_pi = evstr(input("Enter cutoff frequency (Wc/pi): ", "string"));

// Convert cutoff frequency
Wc = wc_pi * %pi;

// Sample index
n = 0:N-1;

// Alpha
alpha = (N-1)/2;

// Initialize
h = zeros(1,N);

// Ideal High Pass Filter
for k = 1:N

    x = n(k) - alpha;

    if x == 0 then
        h(k) = 1 - Wc/%pi;
    else
        h(k) = (sin(%pi*x) - sin(Wc*x)) / (%pi*x);
    end

end

// Rectangular Window
w = ones(1,N);

// FIR coefficients
h = h .* w;

// Display
disp("FIR HIGH PASS FILTER COEFFICIENTS:");
disp(h);

// Impulse response
subplot(2,1,1);
plot2d3(n,h);
xlabel("n");
ylabel("h(n)");
title("FIR High Pass Filter - Rectangular Window");

// Frequency response
M = 500;
omega = linspace(0,%pi,M);
H = zeros(1,M);

for k = 1:M
    for m = 1:N
        H(k) = H(k) + h(m) * ...
        exp(-%i*omega(k)*n(m));
    end
end

// Magnitude response
subplot(2,1,2);
plot(omega,abs(H));
xlabel("Frequency (rad/sample)");
ylabel("Magnitude");
title("FIR High Pass Filter - Frequency Response");

BPF:
clc;
clear;
close;

// FIR BAND PASS FILTER USING RECTANGULAR WINDOW

// Input
N = evstr(input("Enter number of samples N: ", "string"));
wc1_pi = evstr(input("Enter lower cutoff frequency (Wc1/pi): ", "string"));
wc2_pi = evstr(input("Enter upper cutoff frequency (Wc2/pi): ", "string"));

// Convert to radians
Wc1 = wc1_pi * %pi;
Wc2 = wc2_pi * %pi;

// Sample index
n = 0:N-1;

// Alpha
alpha = (N-1)/2;

// Initialize
h = zeros(1,N);

// Ideal Band Pass Filter
for k = 1:N

    x = n(k) - alpha;

    if x == 0 then
        h(k) = (Wc2-Wc1)/%pi;
    else
        h(k) = (sin(Wc2*x)-sin(Wc1*x)) / (%pi*x);
    end

end

// Rectangular Window
w = ones(1,N);

// FIR coefficients
h = h .* w;

// Display coefficients
disp("FIR BAND PASS FILTER COEFFICIENTS:");
disp(h);

// Impulse response
subplot(2,1,1);
plot2d3(n,h);
xlabel("n");
ylabel("h(n)");
title("FIR Band Pass Filter - Rectangular Window");

// Frequency response
M = 500;
omega = linspace(0,%pi,M);
H = zeros(1,M);

for k = 1:M
    for m = 1:N
        H(k) = H(k) + h(m) * ...
        exp(-%i*omega(k)*n(m));
    end
end

// Magnitude response
subplot(2,1,2);
plot(omega,abs(H));
xlabel("Frequency (rad/sample)");
ylabel("Magnitude");
title("FIR Band Pass Filter - Frequency Response");

BSF:
clc;
clear;
close;

// FIR BAND STOP FILTER USING RECTANGULAR WINDOW

// Input
N = evstr(input("Enter number of samples N: ", "string"));
wc1_pi = evstr(input("Enter lower cutoff frequency (Wc1/pi): ", "string"));
wc2_pi = evstr(input("Enter upper cutoff frequency (Wc2/pi): ", "string"));

// Convert cutoff frequencies to radians
Wc1 = wc1_pi * %pi;
Wc2 = wc2_pi * %pi;

// Sample index
n = 0:N-1;

// Alpha
alpha = (N-1)/2;

// Initialize
h = zeros(1,N);

// Ideal Band Stop Filter
for k = 1:N
    
    x = n(k) - alpha;
    
    if x == 0 then
        h(k) = 1 - (Wc2-Wc1)/%pi;
    else
        h(k) = (sin(Wc1*x) - sin(Wc2*x)) / (%pi*x);
    end
    
end

// Rectangular Window
w = ones(1,N);

// Final FIR coefficients
h = h .* w;

// Display coefficients
disp("FIR BAND STOP FILTER COEFFICIENTS:");
disp(h);

// Impulse response
subplot(2,1,1);
plot2d3(n,h);
xlabel("n");
ylabel("h(n)");
title("FIR Band Stop Filter - Rectangular Window");

// Frequency response
M = 500;
omega = linspace(0,%pi,M);
H = zeros(1,M);

for k = 1:M
    for m = 1:N
        H(k) = H(k) + h(m)*exp(-%i*omega(k)*n(m));
    end
end

// Magnitude response
subplot(2,1,2);
plot(omega,abs(H));
xlabel("Frequency (rad/sample)");
ylabel("Magnitude");
title("FIR Band Stop Filter - Frequency Response");



# OUTPUT for LPF:
<img width="1246" height="582" alt="image" src="https://github.com/user-attachments/assets/0e701bb0-da0e-4551-b855-feb718452c70" />

HPF:
<img width="1235" height="578" alt="image" src="https://github.com/user-attachments/assets/375d626c-b2e2-443e-b30c-b018bb3adfee" />
BPF:
<img width="1223" height="570" alt="image" src="https://github.com/user-attachments/assets/47944a4f-2611-46c1-a214-0dc34af5c39e" />

BSF:
<img width="1227" height="577" alt="image" src="https://github.com/user-attachments/assets/9074b7fc-3ad0-4cc4-8b37-9d0402c277ef" />


# RESULT
Thus , The rectangular window was run successfully for the FIR filter
