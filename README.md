# Pulse-Code-Modulation
# Aim
Write a simple Python program for the modulation and demodulation of PCM.
# Tools required

Python IDE with numpy and scipy libraries or colab.

# Program
```
import numpy as np
import matplotlib.pyplot as plt

frequency = 2       
amplitude = 1
duration = 2       

analog_rate = 1000  
sample_rate = 10    
num_levels = 8     
 
t = np.linspace(0, duration, int(analog_rate * duration), endpoint=False)
analog_signal = amplitude * np.sin(2 * np.pi * frequency * t)
plt.figure(figsize=(8,4))
plt.plot(t, analog_signal)
plt.title("Original Analog Signal")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)
plt.show()

t_samp = np.linspace(0, duration, int(sample_rate * duration), endpoint=False)
sampled_signal = amplitude * np.sin(2 * np.pi * frequency * t_samp)
plt.figure(figsize=(8,4))
plt.stem(t_samp, sampled_signal, linefmt='r-', markerfmt='ro', basefmt=' ')
plt.title("Sampled Signal")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)
plt.show()

max_amp = np.max(np.abs(sampled_signal))
step = 2 * max_amp / num_levels
indices = np.round((sampled_signal + max_amp) / step)
indices = np.clip(indices, 0, num_levels-1).astype(int)
quantized_signal = (indices * step) - max_amp
plt.figure(figsize=(8,4))
plt.step(t_samp, quantized_signal, where='mid', color='g')
plt.title("Quantized Signal")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)
plt.show()

num_bits = int(np.log2(num_levels))
binary_codes = [np.binary_repr(idx, width=num_bits) for idx in indices]
print("Binary Codes for Samples:", binary_codes)

transmitted_codes = binary_codes.copy()

decoded_indices = np.array([int(code, 2) for code in transmitted_codes])
decoded_signal = (decoded_indices * step) - max_amp
plt.figure(figsize=(8,4))
plt.step(t_samp, decoded_signal, where='mid', color='purple')
plt.stem(t_samp, decoded_signal, linefmt='g:', markerfmt='go', basefmt=' ')
plt.title("Reconstructed PCM Signal (Demodulated)")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)
plt.show()

plt.figure(figsize=(8,4))
plt.plot(t, analog_signal, label='Original Analog', alpha=0.5)
plt.step(t_samp, decoded_signal, where='mid', color='purple', label='Reconstructed PCM')
plt.title("Original vs Reconstructed PCM Signal")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)
plt.legend()
plt.show()

```
# Output Waveform

<img width="711" height="393" alt="image" src="https://github.com/user-attachments/assets/e2ebc5a1-ba27-4be3-b048-2d23ca53e962" />

<img width="711" height="393" alt="image" src="https://github.com/user-attachments/assets/f40f9f00-2b60-4f0b-ae20-e1775279774f" />

<img width="711" height="393" alt="image" src="https://github.com/user-attachments/assets/8182a07e-304a-437f-9ebb-2ed234fcd289" />

Binary Codes for Samples: ['100', '111', '110', '010', '000', '100', '111', '110', '010', '000', '100', '111', '110', '010', '000', '100', '111', '110', '010', '000']

<img width="711" height="393" alt="image" src="https://github.com/user-attachments/assets/4a1c2378-7962-4d56-899c-a9e5b06f9f05" />

<img width="711" height="393" alt="image" src="https://github.com/user-attachments/assets/38f0109b-c761-404a-b2e0-e63013b55162" />

# Results

Thus, the program for pulse code modulation  have been executed and the waveforms have been verified successfully.
