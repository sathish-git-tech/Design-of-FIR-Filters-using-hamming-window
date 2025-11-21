# Design-of-FIR-Filters-using-hamming-window

# DESIGN OF LOW PASS FIR DIGITAL FILTER 

# AIM: 
          
  To generate design of low pass FIR digital filter using SCILAB 

# APPARATUS REQUIRED: 

  PC Installed with SCILAB 

# PROGRAM 

## LOW PASS FILTER
```
clc;
clear;
close;

M = input('Enter the Odd Filter Length = ');
Wc = input('Enter the Digital Cut off frequency (in radians) = ');

alpha = (M - 1) / 2; // Center value

// Ideal Low Pass filter coefficients
for n = 1:M
    if (n == alpha + 1) then
        hd(n) = Wc / %pi;   // center tap
    else
        hd(n) = sin(Wc * ((n - 1) - alpha)) / (((n - 1) - alpha) * %pi);
    end
end

// Hamming Window
for n = 1:M
    W(n) = 0.54 - (0.46 * cos((2 * %pi * (n - 1)) / (M - 1)));
end

// Apply window to ideal filter
h = hd .* W;
disp(h, 'Filter Coefficients are:');

// Frequency response
[hzm, fr] = frmag(h, 256);

subplot(2, 1, 1);
plot(2 * fr, hzm);
xlabel('Normalized Digital Frequency w');
ylabel('Magnitude');
title('Frequency Response of FIR LPF using Hamming Window');

hzm_dB = 20 * log10(hzm);
subplot(2, 1, 2);
plot(2 * fr, hzm_dB);
xlabel('Normalized Digital Frequency w');
ylabel('Magnitude (dB)');
title('Frequency Response of FIR LPF using Hamming Window');
```
## HIGH PASS FILTER
```
clc;
clear;
close;

M = input('Enter the Odd Filter Length = ');
Wc = input('Enter the Digital Cut off frequency (in radians) = ');

alpha = (M - 1) / 2; // Center value

// Ideal Low Pass filter coefficients
for n = 1:M
    if (n == alpha + 1) then
        hd_lp(n) = Wc / %pi;   // center tap
    else
        hd_lp(n) = sin(Wc * ((n - 1) - alpha)) / (((n - 1) - alpha) * %pi);
    end
end

// Spectral inversion to get High Pass
for n = 1:M
    if (n == alpha + 1) then
        hd(n) = 1 - hd_lp(n);
    else
        hd(n) = -hd_lp(n);
    end
end

// Hamming Window
for n = 1:M
    W(n) = 0.54 - (0.46 * cos((2 * %pi * (n - 1)) / (M - 1)));
end

// Apply window to ideal high-pass filter
h = hd .* W;
disp(h, 'High Pass Filter Coefficients are:');

// Frequency response
[hzm, fr] = frmag(h, 256);

subplot(2, 1, 1);
plot(2 * fr, hzm);
xlabel('Normalized Digital Frequency w');
ylabel('Magnitude');
title('Frequency Response of FIR HPF using Hamming Window');

hzm_dB = 20 * log10(hzm);
subplot(2, 1, 2);
plot(2 * fr, hzm_dB);
xlabel('Normalized Digital Frequency w');
ylabel('Magnitude (dB)');
title('Frequency Response of FIR HPF using Hamming Window');

```

# OUTPUT

# LOW PASS FILTER

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/637ff821-c757-4a60-844a-cf128a297b86" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/4ac09ec5-145d-421c-9fcf-739e6dd6f203" />

# HIGH PASS FILTER

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/ed36d7ed-4959-4af2-a227-5571dc03b831" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/2125a87a-360b-4e84-9ab6-3bb33edf7b35" />


# RESULT
Thus design of FIR low pass and high pass filter is done.
