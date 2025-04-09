** EXP.NO.7-Simulation-of-Digital-Modulation-Techniques**
7. Simulation of Digital Modulation Techniques Such as
   i) Amplitude Shift Keying (ASK)
   ii) Frequency Shift Keying (FSK)
   iii) Phase Shift Keying (PSK)

# AIM
To study the Python simulation for digital modulation techniques.

# SOFTWARE REQUIRED

python using colab.
# ALGORITHMS
1. Digital Modulation Function: The function digital_modulation takes in binary data, modulation type, carrier frequency, sampling rate, and symbol rate.

2. Modulation Types: The function supports ASK (Amplitude Shift Keying), FSK (Frequency Shift Keying), and PSK (Phase Shift Keying) modulation types.

3. Modulated Signal Generation: The function generates the modulated signal based on the chosen modulation type and returns the modulated signal and time vector.

4. Error Handling: The code includes a try-except block to catch the ValueError that occurs when an incorrect modulation type is passed to the function.

5. Alternative Data Generation: The code demonstrates how to generate random binary data using numpy.random.randint() for testing with different data patterns
# PROGRAM
**1)ASK**
import numpy as np 
import matplotlib.pyplot as plt 

data = [1, 0, 1, 0, 1, 1, 0, 1]  # Binary data to be transmitted 
bit_duration = 1  # Duration of each bit in seconds 
fc = 10  # Carrier frequency in Hz 
amplitude = 2  # Carrier amplitude 
sampling_rate = 1000  # Number of samples per second 

t = np.arange(0, bit_duration * len(data), 1/sampling_rate) 

message_signal = np.repeat(data, sampling_rate * bit_duration) 

carrier_signal = amplitude * np.sin(2 * np.pi * fc * t) 

ask_signal = amplitude * message_signal * np.sin(2 * np.pi * fc * t) 
plt.figure(figsize=(12, 8)) 
plt.subplot(3, 1, 1) 
plt.plot(t, message_signal) 
plt.title('Message Signal') 
plt.xlabel('Time') 
plt.ylabel('Amplitude') 
plt.subplot(3, 1, 2) 
plt.plot(t, carrier_signal) 
plt.title('Carrier Signal') 
plt.xlabel('Time') 
plt.ylabel('Amplitude') 
plt.subplot(3, 1, 3) 
plt.plot(t, ask_signal) 
plt.title('ASK Signal') 
plt.xlabel('Time') 
plt.ylabel('Amplitude') 
plt.tight_layout() 
plt.show()

# OUTPUT
![image](https://github.com/user-attachments/assets/4f092945-227d-4a57-8eb3-10cbf902e3ee)

**2)FSK**
import numpy as np
import matplotlib.pyplot as plt

data = [1, 0, 1, 0, 1, 1, 0, 1]  # Binary data to be transmitted
bit_duration = 1  # Duration of each bit in seconds
fc1 = 15  # Frequency for binary 1 in Hz
fc0 = 10  # Frequency for binary 0 in Hz
amplitude = 2  # Carrier amplitude
sampling_rate = 1000  # Number of samples per second

total_time = bit_duration * len(data)
t = np.linspace(0, total_time, int(total_time * sampling_rate), endpoint=False)

message_signal = np.repeat(data, int(sampling_rate * bit_duration))

fsk_signal = np.zeros_like(t)
for i, bit in enumerate(data):
    start_time = i * bit_duration
    end_time = (i + 1) * bit_duration
    indices = (t >= start_time) & (t < end_time)
    time_within_bit = t[indices] - start_time  # Time within the current bit duration
    if bit == 1:
        fsk_signal[indices] = amplitude * np.sin(2 * np.pi * fc1 * time_within_bit)
    else:
        fsk_signal[indices] = amplitude * np.sin(2 * np.pi * fc0 * time_within_bit)

plt.figure(figsize=(12, 8))

plt.subplot(3, 1, 1)
plt.plot(t, message_signal)
plt.title('Message Signal')
plt.xlabel('Time')
plt.ylabel('Amplitude')
plt.yticks([0, 1])  # Set y ticks to 0 and 1

plt.subplot(3, 1, 2)
plt.plot(t, amplitude * np.sin(2 * np.pi * fc1 * t), label='Carrier for 1')
plt.plot(t, amplitude * np.sin(2 * np.pi * fc0 * t), label='Carrier for 0')
plt.title('Carrier Signals')
plt.xlabel('Time')
plt.ylabel('Amplitude')
plt.legend()

plt.subplot(3, 1, 3)
plt.plot(t, fsk_signal)
plt.title('FSK Signal')
plt.xlabel('Time')
plt.ylabel('Amplitude')

plt.tight_layout()
plt.show()

**OUTPUT**
![image](https://github.com/user-attachments/assets/2f75acf4-feaa-47f3-ad47-90da5a29ce2d)

**3)PSK**
import numpy as np
import matplotlib.pyplot as plt


data = [1, 0, 1, 0, 1, 1, 0, 1]  # Binary data to be transmitted
bit_duration = 1  # Duration of each bit in seconds
fc = 10  # Carrier frequency in Hz
amplitude = 2  # Carrier amplitude
sampling_rate = 1000  # Number of samples per second

total_time = bit_duration * len(data)
t = np.linspace(0, total_time, int(total_time * sampling_rate), endpoint=False)

message_signal = np.repeat(data, int(sampling_rate * bit_duration))

psk_signal = np.zeros_like(t)
for i, bit in enumerate(data):
    start_time = i * bit_duration
    end_time = (i + 1) * bit_duration
    indices = (t >= start_time) & (t < end_time)
    time_within_bit = t[indices] - start_time  # Time within the current bit duration
    if bit == 1:
        psk_signal[indices] = amplitude * np.sin(2 * np.pi * fc * time_within_bit)
    else:
        psk_signal[indices] = amplitude * np.sin(2 * np.pi * fc * time_within_bit + np.pi)

plt.figure(figsize=(12, 8))

plt.subplot(3, 1, 1)
plt.plot(t, message_signal)
plt.title('Message Signal')
plt.xlabel('Time')
plt.ylabel('Amplitude')
plt.yticks([0, 1])  # Set y ticks to 0 and 1

plt.subplot(3, 1, 2)
plt.plot(t, amplitude * np.sin(2 * np.pi * fc * t))
plt.title('Carrier Signal')
plt.xlabel('Time')
plt.ylabel('Amplitude')

plt.subplot(3, 1, 3)
plt.plot(t, psk_signal)
plt.title('PSK Signal')
plt.xlabel('Time')
plt.ylabel('Amplitude')

plt.tight_layout()
plt.show()

**OUTPUT**
![image](https://github.com/user-attachments/assets/96f47905-bf1c-4f22-9a03-5e3ea385d8d1)

# RESULT / CONCLUSIONS
Thus the digital modulation schemes such as ASK, FSK and PSK are studied via simulation. 
