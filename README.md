**Ergodicity** in random processes refers to the property where **time averages** are equal to **ensemble averages**. It allows us to analyze a single realization of a process (e.g., a signal) instead of needing to analyze all possible outcomes (the ensemble).

There are two common types:

### 1. **Ergodicity in Mean**

A random process $X(t)$ is **ergodic in mean** if the **time average** of a single realization equals the **ensemble average (mean)** for all time:

$$
\lim_{T \to \infty} \frac{1}{2T} \int_{-T}^{T} X(t) \, dt = \mathbb{E}[X(t)]
$$

* **Time average:** computed from one realization over time.
* **Ensemble average:** expected value taken across all possible realizations at a fixed time $t$.

✅ If this condition holds, the mean can be estimated from a single realization.

### 2. **Ergodicity in Autocorrelation**

A random process $X(t)$ is **ergodic in autocorrelation** if the **time-averaged autocorrelation** equals the **ensemble autocorrelation**:

$$
\lim_{T \to \infty} \frac{1}{2T} \int_{-T}^{T} X(t) X(t+\tau) \, dt = \mathbb{E}[X(t) X(t+\tau)]
$$

Here, both sides give the **autocorrelation function** $R_X(\tau)$, but:

* The **left side** is computed from a single time-domain signal.
* The **right side** is the expected value over all sample functions (realizations).

✅ If this holds, the autocorrelation function can be determined from one realization.

---

A **stationary but not ergodic** process is one where the statistical properties (like mean and autocorrelation) do **not change with time** (i.e., the process is **stationary**), but the **time averages of individual realizations do not equal the ensemble averages** — thus, the process is **not ergodic**.


### ✅ **Counterexample: Random Constant Process**

Let $X(t) = A$, where $A$ is a random variable with a certain distribution (say, uniform over $[-1, 1]$).

So, every realization of the process is a **constant function** over time, but **different for each realization**:

$$
X(t) = A \quad \text{for all } t
$$

### ➤ Why It Is **Stationary**:

* The **mean**, **variance**, and **autocorrelation** of $X(t)$ do **not depend on time**.
* For example:



 $$
\mathbb{E}[X(t)] = \mathbb{E}[A] = 0 \quad (\text{since } A \sim U[-1, 1])
$$
  

  $$
  R_X(\tau) = \mathbb{E}[X(t) X(t+\tau)] = \mathbb{E}[A^2] = \frac{1}{3}
  $$



  (because the variance of $U[-1, 1]$ is $\frac{1}{3}$)

Hence, the process is **strictly stationary**.


### ➤ Why It Is **Not Ergodic**:

* In any **single realization**, the value of $X(t)$ is just the constant $A$.
* So, the **time average** of $X(t)$ over that realization is just $A$:

$$
\lim_{T \to \infty} \frac{1}{2T} \int_{-T}^{T} X(t) \, dt = A
$$
  
* But the **ensemble mean** is:

 $$
\mathbb{E}[X(t)] = \mathbb{E}[A] = 0
$$
  
  
* So, the **time average ≠ ensemble average** unless $A = 0$, which is not guaranteed.

Thus, the process is **not ergodic in mean**, even though it is stationary.

---
### ✅ 1. Condition for ergodicity in mean

A process $X(t)$ is **ergodic in mean** if:

$$
\lim_{T \to \infty} \mu_T = \mu_X \quad \text{(with probability 1)}
$$

### 🔹 Derivation

To derive the condition, consider the **mean square error** between the time average and ensemble average:

$$
\epsilon_T = \mathbb{E} \left[ \left( \mu_T - \mu_X \right)^2 \right]
$$

Substitute $\mu_T$:

$$
\epsilon_T = \mathbb{E} \left[ \left( \frac{1}{2T} \int_{-T}^{T} X(t) dt - \mu_X \right)^2 \right]
$$

Expanding:

$$
\epsilon_T = \frac{1}{(2T)^2} \mathbb{E} \left[ \left( \int_{-T}^{T} \left(X(t) - \mu_X\right) dt \right)^2 \right]
$$

This becomes:

$$
\epsilon_T = \frac{1}{(2T)^2} \int_{-T}^{T} \int_{-T}^{T} \mathbb{E}\left[ (X(t_1) - \mu_X)(X(t_2) - \mu_X) \right] dt_1 dt_2
$$

$$
= \frac{1}{(2T)^2} \int_{-T}^{T} \int_{-T}^{T} R_X(t_1 - t_2) dt_1 dt_2
$$

(where $R_X(\tau)$ is the **autocovariance** function: $R_X(\tau) = \mathbb{E}[(X(t+\tau)-\mu_X)(X(t)-\mu_X)]$, and WSS implies it's only a function of $\tau$).

Change variables:

Let $u = t_1 - t_2$, then:

$$
\epsilon_T = \frac{1}{(2T)^2} \int_{-2T}^{2T} R_X(u)(2T - |u|) \, du
$$

So finally:

$$
\epsilon_T = \frac{1}{2T} \int_{-2T}^{2T} R_X(u)\left(1 - \frac{|u|}{2T}\right) du
$$

### 🔹 Necessary and Sufficient Condition

$$
\lim_{T \to \infty} \epsilon_T = 0 \iff \lim_{T \to \infty} \frac{1}{2T} \int_{-2T}^{2T} R_X(u)\left(1 - \frac{|u|}{2T}\right) du = 0
$$

So, for **ergodicity in mean**, we need:

> $$
> \boxed{ \lim_{T \to \infty} \frac{1}{2T} \int_{-2T}^{2T} R_X(u)\left(1 - \frac{|u|}{2T}\right) du = 0 }
> $$

If $R_X(u) \to 0$ as $|u| \to \infty$ fast enough (e.g., absolutely integrable), this condition is satisfied.


## ✅ 2. Condition for ergodicity in autocorrelation

Process is **ergodic in autocorrelation** if:

$$
\lim_{T \to \infty} R_T(\tau) = R_X(\tau) \quad \text{(with probability 1)}
$$

### 🔹 Derivation

Define mean square error:

$$
\epsilon_T(\tau) = \mathbb{E} \left[ \left( R_T(\tau) - R_X(\tau) \right)^2 \right]
$$

Substitute $R_T(\tau)$:

$$
\epsilon_T(\tau) = \mathbb{E} \left[ \left( \frac{1}{2T} \int_{-T}^{T} X(t)X(t+\tau) dt - R_X(\tau) \right)^2 \right]
$$

Following a similar derivation as before, one obtains a condition:

> $$
> \boxed{ \lim_{T \to \infty} \epsilon_T(\tau) = 0 \quad \forall \tau }
> $$

This implies that for **ergodicity in autocorrelation**, the **variance of the time average of the product $X(t)X(t+\tau)$** must go to zero.

---

### ✅ **Importance of Ergodicity in Signal Processing**

Ergodicity plays a **crucial role** in signal processing, particularly when working with **random (stochastic) signals**. Here's a breakdown of **why ergodicity matters**:


## 1. **Bridges Theory and Practice**

In theory, signals are often modeled as **random processes** with statistical properties like mean, variance, and autocorrelation defined using **ensemble averages** (across many possible realizations).

But in practice:

* We often have **only one realization** of a signal (e.g., one audio recording or one ECG trace).
* **Ergodicity ensures** that analyzing **just one long-enough realization** is sufficient to estimate the statistical properties of the entire process.

👉 So, **ergodicity makes theoretical statistical analysis practically usable**.


## 2. **Statistical Estimation from Single Realization**

If a process is **ergodic in mean**:

* The **time average** of a signal over a single realization gives its **expected value**.

If it's **ergodic in autocorrelation**:

* The **autocorrelation function** can be estimated from a single signal trace.

📌 **Without ergodicity**, one realization may not reflect the overall behavior of the signal.


## 3. **Simplifies System Design and Analysis**

Signal processing systems (like filters, detectors, and estimators) often rely on statistical properties:

* Designing an optimal filter may require the **power spectral density**, which depends on autocorrelation.
* If a signal is **ergodic**, we can compute autocorrelation from a single signal, avoiding complex ensemble modeling.


## 4. **Foundational in Power Spectral Estimation**

Power spectral density (PSD) is a key tool in signal processing:

* PSD is the **Fourier transform of the autocorrelation function**.
* If the process is **ergodic in autocorrelation**, PSD can be estimated from a single time-domain sample.

Thus, **ergodicity enables spectral analysis from a single observed signal**.

## 5. **Useful in Detection and Estimation Problems**

In tasks like:

* Signal detection in noise
* System identification
* Modulation classification

Ergodicity ensures that **reliable performance metrics** (like false alarm rate, SNR, etc.) can be **measured from real data** — not just theoretical models.

## 🔷 6. **Justifies Use of Time-Averaging Filters**

* Many practical digital filters (e.g., moving average filters) rely on **time-domain statistics**.
* Their performance depends on **ergodicity** — if the process is not ergodic, filtering may produce misleading results.

---
A **stationary process** is a random process whose statistical properties do not change with time.

There are two main types:

## ✅ **1. Strict-Sense Stationarity (SSS)**

### 🔹 Definition:

A random process $X(t)$ is **strict-sense stationary** if **all joint probability distributions** are invariant under time shifts.

That is, for any $n \in \mathbb{N}$, any $t_1, t_2, \dots, t_n$, and any time shift $\tau$:

$$
F_{X(t_1), X(t_2), \dots, X(t_n)}(x_1, x_2, \dots, x_n) = F_{X(t_1 + \tau), X(t_2 + \tau), \dots, X(t_n + \tau)}(x_1, x_2, \dots, x_n)
$$

So **all statistical properties** (mean, variance, higher moments, and distributions) remain unchanged over time.


### 🔸 Example: **Uniformly distributed cosine**

Let:

$$
X(t) = A \cos(\omega_c t + \theta)
$$

Where:

* $A$, $\omega_c$ are constants,
* $\theta \sim U(0, 2\pi)$, uniformly distributed.

Then:

* $X(t)$ is **strict-sense stationary**.
* The distribution of $X(t)$ is time-invariant because $\theta$ randomizes the phase over all time.


## ✅ **2. Wide-Sense Stationarity (WSS)**

### 🔹 Definition:

A random process $X(t)$ is **wide-sense stationary** if:

1. **Mean is constant**:
   

   $$
   \mu_X(t) = \mathbb{E}[X(t)] = \mu, \quad \forall t
   $$
---
2. **Autocorrelation depends only on time difference** $\tau$:

   **$$
   R_X(t_1, t_2) = \mathbb{E}[X(t_1) X(t_2)] = R_X(t_1 - t_2)
   $$**

Only **first and second-order** statistics are considered. It’s a weaker condition than SSS.


### 🔸 Example: **Zero-mean Gaussian white noise**

Let $X(t)$ be zero-mean white noise:

* $\mathbb{E}[X(t)] = 0$
* $R_X(\tau) = N_0 \delta(\tau)$

It satisfies:

* Constant mean,
* Autocorrelation depends only on $\tau$,
* Hence **WSS**.

---
### ✅ **Applications Where Ergodic Assumption is Valid **

In many real-world systems, we **assume ergodicity** (usually wide-sense ergodicity) **because we only have one signal realization** but still want to estimate meaningful statistics like mean, variance, or power spectral density. Here's where that assumption holds well:

## 🔷 1. **Speech Signal Processing**

* Speech signals over short frames (10–30 ms) are **assumed stationary and ergodic**.
* This allows estimation of:

  * **Short-time energy**, **zero-crossing rate**
  * **Formants**, **pitch**, **MFCCs**
* Essential in **speech recognition**, **compression**, and **synthesis**.

## 🔷 2. **Audio and Music Signal Analysis**

* Short segments of music (like a sustained note or beat) are modeled as **wide-sense stationary and ergodic**.
* Enables spectral analysis using FFT or PSD estimation from single recordings.

## 🔷 3. **Wireless Communication Channels (Narrowband, Slow-Fading)**

* In slowly varying or **quasi-static fading channels**, the signal can be treated as **ergodic** over long periods.
* Ergodicity allows estimation of average **SNR**, **bit error rates**, or **channel capacity** from one realization.

## 🔷 4. **Biomedical Signal Processing (e.g., ECG, EEG)**

* Over short intervals, **heartbeats** or **brain waves** are treated as stationary and ergodic.
* Enables estimation of:

  * **Heart rate variability**
  * **Power in EEG frequency bands (alpha, beta, etc.)**
  * Useful in **diagnostics**, **monitoring**, and **BCIs**.

## 🔷 5. **Radar and Sonar Signal Processing**

* Reflected signals from targets (after removing Doppler) are modeled as **ergodic WSS processes**.
* Allows detection, ranging, and target classification from **a single observation** over time.

## 🔷 6. **Vibration Analysis in Mechanical Systems**

* The vibration signal from a rotating machine (e.g., motor or turbine) is often assumed **ergodic and stationary** under steady-state.
* Used for **fault detection**, **condition monitoring**, and **predictive maintenance**.

## 🔷 7. **Stock Market Data (Locally Ergodic Models)**

* While not globally stationary, over **short time windows**, financial return processes are modeled as **ergodic** for volatility estimation or risk modeling.

## 🔷 8. **Image Processing (2D Signals)**

* **Texture** and **natural image regions** (e.g., sky, foliage) are modeled as **2D stationary and ergodic** processes.
* Enables estimation of second-order statistics from a **single image** window.

---
### ✅ **Definition: Spectral Shaping**

**Spectral shaping** refers to the **modification or design of the frequency spectrum** of a signal to achieve a desired power distribution across frequencies.

In simple terms, it means **controlling how a signal's energy is spread in the frequency domain**, often to meet certain performance, regulatory, or hardware requirements.


### 🔷 **Why is Spectral Shaping Used?**

* To **fit within bandwidth** limits (e.g., in communication channels)
* To **reduce interference** with adjacent channels
* To **optimize signal power** where the channel is strongest (e.g., water-filling in fading channels)
* To **shape noise** or signal spectrum for better detection or processing


### 🔷 **Methods of Spectral Shaping**

1. **Filtering**:

   * Applying bandpass, low-pass, or custom filters to emphasize or suppress certain frequency components.
   * Example: Using a raised cosine filter to shape transmitted symbols in digital communications.

2. **Pulse Shaping**:

   * In digital communications, modifying the shape of the transmitted pulse (e.g., sinc, Gaussian) to control spectral bandwidth and avoid intersymbol interference.

3. **Modulation Techniques**:

   * Changing the baseband signal's frequency structure by using modulation schemes that naturally shape the spectrum.

4. **Spectral Masking**:

   * Adjusting signal spectrum to meet spectral mask requirements imposed by communication standards (e.g., in Wi-Fi, LTE).

### 🔷 **Mathematical Insight**

If a signal $x(t)$ has a Fourier transform $X(f)$, spectral shaping modifies $X(f)$ to a desired form $X_s(f)$ using a shaping function or filter $H(f)$:

$$
X_s(f) = H(f) \cdot X(f)
$$

---
### ✅ **How Signal Bandwidth Is Altered by Modulation**

**Modulation** is the process of varying a carrier signal’s parameters (amplitude, frequency, or phase) based on the input baseband signal. When a signal is modulated, **its bandwidth is typically altered (increased)** compared to the original baseband signal.

## 🔷 1. **Baseband Bandwidth (W)**

Let the original message or baseband signal $m(t)$ have a bandwidth $W$, meaning its spectrum $M(f)$ is mostly confined to $|f| \leq W$.

## 🔷 2. **Modulation Types and Their Effect on Bandwidth**

### ▶ **Amplitude Modulation (AM)**

In standard AM:

$$
x(t) = [1 + m(t)] \cos(2\pi f_c t)
$$

* Bandwidth of AM signal = **2W**
* Sidebands appear at $f_c \pm W$

➡️ **Double-sideband** modulation (DSB) doubles the bandwidth:

$$
B_{\text{AM}} = 2W
$$

### ▶ **DSB-SC (Double Sideband - Suppressed Carrier)**

$$
x(t) = m(t)\cos(2\pi f_c t)
$$

* Bandwidth = **2W** (same as AM), but no carrier component.

### ▶ **SSB (Single Sideband Modulation)**

Only **one sideband** (upper or lower) is transmitted.

* Bandwidth = **W**

➡️ Very bandwidth-efficient.

### ▶ **Frequency Modulation (FM)**

$$
x(t) = A_c \cos\left(2\pi f_c t + 2\pi k_f \int m(t) dt\right)
$$

* FM bandwidth depends on:

  * Frequency deviation $\Delta f$
  * Message bandwidth $W$

Using **Carson's Rule**:

$$
B_{\text{FM}} \approx 2(\Delta f + W)
$$

➡️ FM typically **increases bandwidth significantly**, especially for high-fidelity signals.

### ▶ **Phase Modulation (PM)**

Similar to FM, and has comparable bandwidth requirements:

$$
x(t) = A_c \cos\left(2\pi f_c t + k_p m(t)\right)
$$

* Also results in a **broadened spectrum**.

## 🔷 3. **Why Modulation Alters Bandwidth**

* Modulation **shifts the baseband spectrum** to a higher frequency (centered at carrier $f_c$), often **replicating it** (e.g., sidebands).
* Some schemes **compress** the spectrum (SSB), while others **expand** it (FM, PM).

> **Modulation typically increases bandwidth**, except in optimized schemes like SSB.

---
### ✅ **Importance of Power Spectral Density (PSD) in Communication Systems**

**Power Spectral Density (PSD)** describes **how the power of a signal is distributed across different frequencies**. In communication systems, PSD is fundamental for analyzing, designing, and optimizing the transmission and reception of signals.


## 🔷 1. **Understanding Frequency Content of Signals**

PSD helps engineers understand:

* **Which frequency components carry energy**
* **How signal power is spread over the spectrum**

This is essential for:

* Designing filters
* Allocating frequency bands
* Avoiding spectral overlap and interference



## 🔷 2. **Bandwidth Estimation and Spectral Efficiency**

* PSD shows the **occupied bandwidth** of a signal (region where most power lies).
* It helps evaluate **spectral efficiency**: how efficiently a system uses the spectrum (e.g., bits/s/Hz).
* Essential for bandwidth-limited systems like mobile networks and satellite links.



## 🔷 3. **Channel Capacity and Noise Analysis**

* Noise is often characterized by its PSD (e.g., white noise has flat PSD).
* Channel capacity (Shannon’s formula) depends on the **signal PSD and noise PSD**:

 **$$
  C = \int_{B} \log_2\left(1 + \frac{S(f)}{N(f)}\right) df
  $$**
  > where $S(f)$: signal PSD, $N(f)$: noise PSD.

✅ PSD directly influences **data rate** and **system design**.



## 🔷 4. **Filter and Modulation Design**

* Knowing PSD allows proper **filter design** (matched filters, low-pass, bandpass).
* Helps in **modulation scheme selection** (e.g., designing spectrally efficient modulation like OFDM, QAM, PSK).
* PSD reveals how modulation **spreads** or **shapes** the spectrum.



## 🔷 5. **Regulatory Compliance**

* Communication systems must **conform to spectral masks** imposed by standards (e.g., Wi-Fi, LTE, 5G).
* PSD analysis ensures **transmitted signals stay within allowed bands** to avoid interfering with others.



## 🔷 6. **Interference and Crosstalk Analysis**

* PSD helps evaluate **interference** between adjacent channels.
* Allows prediction and mitigation of **inter-symbol interference (ISI)** and **inter-carrier interference (ICI)**.

## 🔷 7. **Signal Detection and Estimation**

* Receivers often use PSD estimates for:

  * **Carrier frequency recovery**
  * **Timing synchronization**
  * **Noise power estimation**
---
### ✅ **Derivation: Output PSD of an LTI System from Input PSD**

Let a **wide-sense stationary (WSS)** random process $X(t)$ pass through a **linear time-invariant (LTI)** system with **impulse response** $h(t)$. The output is $Y(t)$.

We aim to derive the **power spectral density (PSD)** of $Y(t)$, denoted $S_Y(f)$, in terms of:

* Input PSD $S_X(f)$
* System frequency response $H(f)$ (Fourier Transform of $h(t)$)



## 🔷 1. **System Model**

Given:

$$
Y(t) = (h * X)(t) = \int_{-\infty}^{\infty} h(\tau) X(t - \tau) \, d\tau
$$



## 🔷 2. **Assumptions**

* $X(t)$ is **wide-sense stationary (WSS)**
* The LTI system is **stable** and has a **finite-energy** impulse response $h(t)$



## 🔷 3. **Autocorrelation of Output**

The output autocorrelation function $R_Y(\tau) = \mathbb{E}[Y(t)Y(t+\tau)]$

We express $Y(t)$ and $Y(t+\tau)$ in terms of $X(t)$:

$$
Y(t) = \int h(\alpha) X(t - \alpha) \, d\alpha
$$

$$
Y(t+\tau) = \int h(\beta) X(t + \tau - \beta) \, d\beta
$$

Then:

$$
R_Y(\tau) = \mathbb{E}[Y(t)Y(t+\tau)] = \int\int h(\alpha) h(\beta) \mathbb{E}[X(t - \alpha) X(t + \tau - \beta)] \, d\alpha d\beta
$$

Because $X(t)$ is WSS:

$$
\mathbb{E}[X(t - \alpha) X(t + \tau - \beta)] = R_X(\tau + \alpha - \beta)
$$

So:

$$
R_Y(\tau) = \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} h(\alpha) h(\beta) R_X(\tau + \alpha - \beta) \, d\alpha d\beta
$$



## 🔷 4. **Take Fourier Transform to Get PSD**

Recall:

* PSD is the Fourier transform of autocorrelation:



  $$
  S_Y(f) = mathbb{F}\{R_Y(\tau)\}
  $$


* Use **Convolution Theorem** in frequency domain:

  * Convolution in time → Multiplication in frequency

Thus:

$$
S_Y(f) = |H(f)|^2 \cdot S_X(f)
$$



## ✅ **Final Result:**

$$
\boxed{S_Y(f) = |H(f)|^2 \cdot S_X(f)}
$$



### 🔷 **Interpretation:**

* The **output PSD** is the **input PSD scaled by the magnitude squared of the system's frequency response**.
* The system **shapes** the spectrum of the input signal.



### 🔷 Example:

If $H(f)$ is a **low-pass filter**, then high-frequency components in $S_X(f)$ are suppressed in $S_Y(f)$.



Let me know if you'd like a numerical example or MATLAB/Python code to visualize this.


