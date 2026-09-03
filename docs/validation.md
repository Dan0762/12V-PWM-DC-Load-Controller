# Rev.A Validation and Test Results

## 1. Test Setup

Supply voltage: 12 V nominal

Test equipment:
- bench power supply
- digital multimeter
- oscilloscope
- resistive load
- 12 V DC motor

The controller was tested at several duty-cycle settings from the minimum
usable setting up to approximately 95%.

---

## 2. No-Load Test

| Duty setting, % | Vin, V | Iin, mA | PWM frequency, kHz |
|---:|---:|---:|---:|
| 10 | 12.02 | 15 | 24.31 |
| 25 | 12.02 | 13 | 24.00 |
| 50 | 12.02 | 10 | 23.96 |
| 75 | 12.02 | 7 | 23.22 |
| 95 | 12.02 | 3 | 20.33 |

The PWM frequency remained close to 24 kHz through most of the control
range and decreased near the upper end of the adjustment range.

---

## 3. Resistive Load Test

| Duty setting, % | Vin, V | Iin, A | Pin, W | PWM frequency, kHz |
|---:|---:|---:|---:|---:|
| 15 | 11.92 | 0.382 | 4.553 | 24.00 |
| 25 | 11.88 | 0.563 | 6.688 | 24.30 |
| 50 | 11.77 | 0.950 | 11.240 | 24.23 |
| 75 | 11.68 | 1.322 | 15.441 | 23.53 |
| 95 | 11.61 | 1.580 | 18.343 | 20.67 |

---

## 4. Inductive Load Test

A 12 V brushed DC motor was used as the inductive load.

| Duty setting, % | Vin, V | Iin, A | Pin, W | PWM frequency, kHz | Motor behavior |
|---:|---:|---:|---:|---:|---|
| 15 | 12.00 | 0.035 | 0.420 | 24.46 | Did not start |
| 25 | 12.00 | 0.040 | 0.480 | 24.45 | Running |
| 50 | 12.00 | 0.050 | 0.600 | 24.35 | Running |
| 75 | 11.99 | 0.088 | 1.055 | 23.53 | Running |
| 95 | 11.99 | 0.113 | 1.355 | 20.70 | Running |

The motor did not start at the lowest tested duty setting but operated
normally from approximately 25% duty cycle and above.

---

## 5. Oscilloscope Measurements

### 5.1 PWM waveform

PWM waveform at 50% duty:

![PWM waveform at 50% duty](images/validation/pwm-50.png)

Measured frequency: XX.XX kHz  
Measured duty cycle: XX.X %

### 5.2 MOSFET gate waveform

![MOSFET gate waveform](images/validation/gate-50.png)

Gate drive amplitude: XX.X V  
Frequency: XX.XX kHz

### 5.3 MOSFET drain waveform

![MOSFET drain waveform](images/validation/drain-50.png)

The drain waveform was checked for switching behavior and excessive
voltage spikes.

---

## 6. Thermal Observation

During the performed load tests, no significant heating of the MOSFET
or flyback diode was observed.

Because the component temperatures remained low under the tested
conditions, no separate extended thermal test was performed.

---

## 7. Conclusion

Rev.A operated correctly with both resistive and inductive loads.

The PWM controller remained functional across the tested adjustment
range, with the switching frequency remaining near 24 kHz through most
of the range and decreasing near maximum duty.

No abnormal MOSFET or flyback-diode heating was observed during the
performed tests.
