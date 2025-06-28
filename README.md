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
  \lim_{T \to \infty} \frac{1}{2T} \int_{-T}^T X(t)\,dt = A
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

