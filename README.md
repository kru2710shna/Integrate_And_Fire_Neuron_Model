# Leaky Integrate-and-Fire Neuron Model

## Task

This project implements a **Leaky Integrate-and-Fire (LIF)** neuron model — one of the simplest and most biologically interpretable models of neuronal spiking. The project mathematically derives the equations governing the membrane potential dynamics, simulates them under both deterministic and noisy current inputs, and visualizes the resulting voltage traces, spike rasters, and inter-spike interval distributions.

### Mathematical Explanation

The membrane of a neuron behaves like a leaky capacitor with resistance \( R_m \) and capacitance \( C_m \). Using Kirchhoff’s Current Law (KCL), the sum of currents through the resistor and capacitor equals the input current:

\[
I(t) = I_C + I_R = C_m \frac{dV}{dt} + \frac{V - V_{rest}}{R_m}
\]

Rearranging:

\[
C_m \frac{dV}{dt} = -\frac{(V - V_{rest})}{R_m} + I(t)
\]

Defining the **membrane time constant** \( \tau_m = R_m C_m \):

\[
\frac{dV}{dt} = \frac{-(V - V_{rest}) + R_m I(t)}{\tau_m}
\]

A spike is generated when \( V(t) \geq V_{th} \), after which the potential resets to \( V_{reset} \) and enters a refractory period.

### Biological Explanation

Biologically, this model captures how neurons integrate incoming electrical signals (input currents) over time. The **membrane potential (V)** represents the voltage difference between the inside and outside of the neuron.

- **Sodium (Na⁺)** ions primarily drive depolarization — when the neuron’s membrane potential becomes more positive. Sodium channels open rapidly, allowing Na⁺ to flow into the cell.
- **Potassium (K⁺)** ions drive repolarization — when the membrane returns to its resting potential. K⁺ channels open after Na⁺ influx, allowing K⁺ to leave the cell, restoring the negative potential.
- The balance between Na⁺ and K⁺ movement, combined with the leak current, leads to repetitive spiking when the input current exceeds a threshold.

### What We Are Doing

1. Simulating the LIF model using **Euler’s method** for numerical integration.
2. Injecting two types of current:
   - **Deterministic current:** constant input resulting in periodic spikes.
   - **Noisy current:** fluctuating input (Gaussian noise) resulting in irregular, biologically realistic firing.
3. Exporting results as CSV files and visualizing:
   - Voltage traces
   - Spike rasters
   - Inter-spike interval histograms

### Approach

- Implemented the LIF differential equation.
- Used Python (NumPy + Matplotlib) for simulation and visualization.
- Simulated both regular and stochastic inputs.
- Collected and exported time-voltage and spike data for analysis.

### Trade-Offs

| Aspect | Simplicity | Biological Accuracy |
|--------|-------------|----------------------|
| **LIF Model** | Easy to compute, fast | Ignores ion channel dynamics |
| **Hodgkin-Huxley Model** | Detailed Na⁺/K⁺ ion behavior | Computationally intensive |

The LIF model is chosen as a **baseline** because it captures essential neuronal behavior (integration and firing) while being mathematically and computationally tractable.

---

## Model Information

### Parameters Used

| Parameter | Symbol | Value | Unit |
|------------|---------|--------|------|
| Resting Potential | \( V_{rest} \) | -65 | mV |
| Threshold Potential | \( V_{th} \) | -50 | mV |
| Reset Potential | \( V_{reset} \) | -65 | mV |
| Membrane Resistance | \( R_m \) | 100e6 | Ω |
| Membrane Capacitance | \( C_m \) | 0.1e-9 | F |
| Time Constant | \( \tau_m = R_m C_m \) | 0.01 | s |
| Input Current | \( I_{mean} \) | 2e-9 | A |
| Noise Std Dev | \( \sigma_I \) | 0.5e-9 | A |
| Refractory Period | \( t_{ref} \) | 5e-3 | s |

### Mathematical Proof Summary

The equation governing the LIF neuron is derived from Kirchhoff’s Law and simplified into:

\[
\frac{dV}{dt} = \frac{-(V - V_{rest}) + R_m I(t)}{\tau_m}
\]

Solving this using Euler’s method gives:

\[
V(t+\Delta t) = V(t) + \frac{\Delta t}{\tau_m} [-(V(t) - V_{rest}) + R_m I(t)]
\]

---

## Flow of Ions and Spike Generation

### Role of Na⁺ and K⁺

- **Depolarization:** Na⁺ channels open, sodium ions enter, and the voltage increases.
- **Repolarization:** K⁺ channels open after a short delay, potassium ions exit, bringing the voltage back down.
- **Afterhyperpolarization:** K⁺ efflux overshoots, causing a brief period below \( V_{rest} \).

### Exchange Mechanism and Spike Reason

The spike occurs because Na⁺ influx overwhelms the resting K⁺ efflux, rapidly increasing membrane voltage. Once Na⁺ channels inactivate and K⁺ channels activate, the neuron returns to its resting state — mimicking a biological action potential.

---

## Results

### CSV Files Generated

| File | Description |
|------|--------------|
| `lif_deterministic.csv` | Time vs. voltage (deterministic input) |
| `lif_noisy.csv` | Time vs. voltage (noisy input) |
| `spikes_deterministic.csv` | Spike times for deterministic neuron |
| `spikes_noisy.csv` | Spike times for noisy neuron |

### Observations

- Deterministic neuron fires **periodically** (~170 Hz).
- Noisy neuron fires **irregularly** with small ISI variability.
- Coefficient of variation (CV) increases with noise amplitude — indicating reduced regularity.

---

## Conclusion

This project successfully demonstrates the relationship between input current, membrane potential, and spike generation in a neuron.  
It shows how noise impacts neuronal precision and replicates biological spike variability with minimal computational complexity.

---

**Developed and Simulated by:** Krushna Thakkar  
**Environment:** Python 3.11 (NumPy, Matplotlib, Pandas)  
**Data Folder:** `/data` containing exported CSVs and analysis-ready results.
