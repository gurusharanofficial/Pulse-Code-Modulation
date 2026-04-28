# Pulse-Code-Modulation
# Aim
Write a simple Python program for the modulation and demodulation of PCM,DM.
# Tools required

Python IDE with numpy and scipy libraries or colab.

# Program
```
import numpy as np
import matplotlib.pyplot as plt



fm = 2                  
fs = 20                 
duration = 2            
n_bits = 3              

t = np.linspace(0, duration, 1000)    
ts = np.arange(0, duration, 1/fs)     


x = np.sin(2 * np.pi * fm * t)

xs = np.sin(2 * np.pi * fm * ts)



L = 2 ** n_bits         
x_min = -1
x_max = 1

delta = (x_max - x_min) / L


xq = np.round((xs - x_min) / delta) * delta + x_min
xq = np.clip(xq, x_min, x_max)



indices = ((xq - x_min) / delta).astype(int)
indices = np.clip(indices, 0, L - 1)

binary_codes = [format(i, f'0{n_bits}b') for i in indices]

print("Sampled Value\tQuantized Value\tPCM Code")
print("------------------------------------------------")
for i in range(len(xs)):
    print(f"{xs[i]:.3f}\t\t{xq[i]:.3f}\t\t{binary_codes[i]}")



pcm_bits = ""

for code in binary_codes:
    pcm_bits += code

pcm_wave = [int(bit) for bit in pcm_bits]

bit_time = np.arange(len(pcm_wave))



decoded_indices = np.array([int(code, 2) for code in binary_codes])
decoded_signal = decoded_indices * delta + x_min


plt.figure(figsize=(12, 14))

plt.subplot(5, 1, 1)
plt.plot(t, x)
plt.title("Original Analog Signal")
plt.xlabel("Time")
plt.ylabel("Amplitude")
plt.grid(True)

plt.subplot(5, 1, 2)
plt.stem(ts, xs, basefmt=" ")
plt.title("Sampled Signal")
plt.xlabel("Time")
plt.ylabel("Amplitude")
plt.grid(True)


plt.subplot(5, 1, 3)
plt.stem(ts, xq, basefmt=" ")
plt.title("Quantized Signal")
plt.xlabel("Time")
plt.ylabel("Amplitude")
plt.grid(True)


plt.subplot(5, 1, 4)
plt.step(bit_time, pcm_wave, where='post')
plt.ylim(-0.2, 1.2)
plt.title("PCM Output Waveform (Binary Pulse Train)")
plt.xlabel("Bit Position")
plt.ylabel("Binary Level")
plt.grid(True)


plt.subplot(5, 1, 5)
plt.step(ts, decoded_signal, where='mid')
plt.title("PCM Demodulated (Reconstructed) Signal")
plt.xlabel("Time")
plt.ylabel("Amplitude")
plt.grid(True)

plt.tight_layout()
plt.show()

```
# Output Waveform

Sampled Value	Quantized Value	PCM Code
------------------------------------------------
0.000		0.000		100
0.588		0.500		110
0.951		1.000		111
0.951		1.000		111
0.588		0.500		110
0.000		0.000		100
-0.588		-0.500		010
-0.951		-1.000		000
-0.951		-1.000		000
-0.588		-0.500		010
-0.000		0.000		100
0.588		0.500		110
0.951		1.000		111
0.951		1.000		111
0.588		0.500		110
0.000		0.000		100
-0.588		-0.500		010
-0.951		-1.000		000
-0.951		-1.000		000
-0.588		-0.500		010
-0.000		0.000		100
0.588		0.500		110
0.951		1.000		111
0.951		1.000		111
0.588		0.500		110
0.000		0.000		100
-0.588		-0.500		010
-0.951		-1.000		000
-0.951		-1.000		000
-0.588		-0.500		010
-0.000		0.000		100
0.588		0.500		110
0.951		1.000		111
0.951		1.000		111
0.588		0.500		110
0.000		0.000		100
-0.588		-0.500		010
-0.951		-1.000		000
-0.951		-1.000		000
-0.588		-0.500		010

<img width="1189" height="1389" alt="image" src="https://github.com/user-attachments/assets/4b1205c4-d6a0-492f-bdb1-4d549e06fd18" />




# Results

Thus, the program for pulse code modulation and Delta modulation have been executed and the waveforms have been verified successfully.
