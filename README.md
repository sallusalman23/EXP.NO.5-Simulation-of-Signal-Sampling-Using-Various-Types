# EXP.NO.5-Simulation-of-Signal-Sampling-Using-Various-Types

# AIM
 i) Ideal Sampling
ii) Natural Sampling
iii) Flat Top Sampling

# SOFTWARE REQUIRED
Google Collab

# ALGORITHMS

1. Generate a sine wave signal
2. Create impulse train for ideal sampling
3. Create rectangular pulse train for natural and flat-top sampling
4. Multiply the signal with sampling pulses
5. Plot original and sampled signals
   
# PROGRAM
```
import numpy as np
import matplotlib.pyplot as plt

# === Signal & Sampling Parameters ===
fs = 10000                   # High-resolution time base (Hz)
t = np.linspace(0, 1, fs)    # Time vector (0 to 1 sec)
f = 7                       # NEW: Frequency of sine wave (Hz)
x = np.sin(2 * np.pi * f * t)  # Original sine wave

fs_sample = 80              # NEW: Sampling frequency (Hz)
Ts = 1 / fs_sample          # Sampling period
pulse_width = 0.005         # Width of sampling pulse (5 ms)

# === Output Arrays ===
ideal_output = np.zeros_like(t)
natural_output = np.zeros_like(t)
flattop_output = np.zeros_like(t)

# === Sampling Simulation ===
for i in np.arange(0, 1, Ts):
    idx_start = int(i * fs)
    idx_end = int((i + pulse_width) * fs)
    if idx_end > len(t):
        idx_end = len(t)

    sample_val = np.sin(2 * np.pi * f * i)  # Value of x at sample point

    # Ideal Sampling
    ideal_output[idx_start] = sample_val

    # Natural Sampling
    natural_output[idx_start:idx_end] = x[idx_start:idx_end]

    # Flat-Top Sampling
    flattop_output[idx_start:idx_end] = sample_val

# === Plotting ===
plt.figure(figsize=(14, 10))

# 1. Ideal Sampling
plt.subplot(3, 1, 1)
plt.plot(t, x, label="Input Sine Wave", color='lightgray')
plt.stem(t, ideal_output, linefmt='green', markerfmt='go', basefmt=' ')  # FIXED
plt.title("Ideal Sampling")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)
plt.legend(["Input Sine", "Ideal Sampled"])

# 2. Natural Sampling
plt.subplot(3, 1, 2)
plt.plot(t, x, label="Input Sine Wave", color='lightgray')
plt.plot(t, natural_output, color='orange', label="Natural Sampled")
plt.title("Natural Sampling")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)
plt.legend()

# 3. Flat-Top Sampling
plt.subplot(3, 1, 3)
plt.plot(t, x, label="Input Sine Wave", color='lightgray')
plt.plot(t, flattop_output, color='red', label="Flat-Top Sampled")
plt.title("Flat-Top Sampling")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)
plt.legend()

plt.tight_layout()
plt.show()
```
# OUTPUT
![WhatsApp Image 2025-04-08 at 23 07 45_fa69b411](https://github.com/user-attachments/assets/44ddc448-04a2-41e3-aee5-099ce0ad5872)

 
# RESULT / CONCLUSIONS
To simulate and visualize signal sampling using three techniques: Ideal Sampling,
Natural Sampling, and Flat-Top Sampling, and compare the sampled output for a given
analog signal (sine wave) was verified successfully
