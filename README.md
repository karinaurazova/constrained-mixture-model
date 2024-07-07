# Constrained Mixture Model (CMM) & Constrained Mixture Model with Mechanical Feedback for stress analysis in various soft tissue deformation protocols

In this repository you will find Python scripts for implementing constrained mixture model for soft tissue with different deformation protocols. The scripts are based on mathematical model of constrained mixture model and constrained mixture model with mechanical feedback.

## Installation

To run the scripts, you will need to have Python installed on your machine. You can download Python from the official website: [https://www.python.org/](https://www.python.org/)

You will also need to install the following Python libraries:

```
pip install numpy
pip install scipy
pip install matplotlib
```

## Usage

1. Copy the repository to your local machine:

```
git clone https://github.com/karinaurazova/constrained-mixture-model.git
```

2. Run the Python script for the desired model:

- `CMM_strech_constant.ipynb`: Implementation of the constrained mixture model with constant strech.
- `CMM_strech_cicle.ipynb`: Implementation of the constrained mixture model with cicle strech.
- `CMM_strech_increases_linearly.ipynb`: Implementation of the constrained mixture model with strech increases linearly.
- `CMM_with_mechanical_feedback.ipynb`: Implementation of the constrained mixture model with mechanical feedback, the following functions are written in this script constant strech, cicle strech, strech increases linearly.

3. Follow the instructions provided in the script for running simulations with different deformation protocols.

## Theory
These mathematical models are used to analyze the stress state of tendons and ligaments, but you can upgrade them for any soft tissue, not just unidirectional collagen fibers.
Writing the model scripts, I relied on the scientific works of Larry Taber  "Continuum Modeling in Mechanobiology" https://link.springer.com/book/10.1007/978-3-030-43209-6


### Strech constant
In script `CMM_strech_constant.ipynb` the following system of equations is implemented:
```math
\begin{align}
    \begin{cases}
        &\boldsymbol{\sigma} = \boldsymbol{\sigma}_x^c + \boldsymbol{\sigma}_x^e + \boldsymbol{\sigma}_x^g,\\
        &\displaystyle \boldsymbol{\sigma}_x^c(t) =  \frac{J^c(0)}{J(0)}\bar{\boldsymbol{\sigma}_x^c}(\lambda_x^{c*}(t, 0))q^c(t, 0) + \frac{j^{c+}}{J(t)} \int\limits_0^t \bar{\boldsymbol{\sigma}_x^c}(\lambda_x^{c*}(t, \tau))q^c(t, \tau) d\tau,\\
       &\displaystyle \boldsymbol{\sigma}_x^e(t) = \frac{J^e(0)}{J(0)}\bar{\boldsymbol{\sigma}_x^e}(\lambda_x^{e*}(t, 0))q^e(t, 0) + \frac{j^{e+}}{J(t)} \int\limits_0^t \bar{\boldsymbol{\sigma}_x^e}(\lambda_x^{e*}(t, \tau))q^e(t, \tau) d\tau,\\
       &\displaystyle \boldsymbol{\sigma}_x^g(t) = 2\phi^g c_g\left(\hat{\lambda}^2 - \frac{1}{\hat{\lambda}}\right),\\
       &\displaystyle \bar{\boldsymbol{\sigma}}_x^c = 4c_c(\lambda_x^{c*})^2[(\lambda_x^{c*})^2 - 1]e^{\alpha_c [(\lambda_x^{c*})^2 - 1]^2},\\
       &\displaystyle \bar{\boldsymbol{\sigma}}_x^e = 4c_e(\lambda_x^{e*})^2[(\lambda_x^{e*})^2 - 1],\\
       %&\bar{\sigma}_x^g = 2c_g\lambda_i^2, \text{$i = x, y, z$}
       &\lambda_x^{c*}(t, \tau) = \lambda_{0}^c \frac{G_x^c(t)}{G_x^c(\tau)},\\
       &\lambda_x^{c*}(t, \tau) = \lambda_{0}^c \frac{G_x^c(t)}{G_x^c(\tau)}
    \end{cases}
\end{align}
```
As a result of executing the script, "stress-time" graphs are displayed, however, you can upgrade the script and output any dependencies for the specified functions.

![strech_const](https://drive.google.com/uc?id=1aHdDiN7VW6J3sWlN_qVVtX7whx-ceLpB)

For example, you can display a graph of the change in mass over time

![change_mass](https://drive.google.com/uc?id=1aUyRcap6wdv5etUiHnT83zwLbNTLVqBE)

### Strech cicle
In script `CMM_strech_cicle.ipynb` the following system of equations is implemented:
```math
\begin{equation}
    \begin{cases}
        &\displaystyle \boldsymbol{\sigma} = \boldsymbol{\sigma}_x^c + \boldsymbol{\sigma}_x^e + \boldsymbol{\sigma}_x^g,\\
        &\displaystyle \boldsymbol{\sigma}_x^c(t) = \frac{J^c(0)}{J(0)}\bar{\boldsymbol{\sigma}_x^c}(\lambda_x^{c*}(t, 0))q^c(t, 0) + \frac{j^{c+}}{J(t)} \int\limits_0^t \bar{\boldsymbol{\sigma}_x^c}(\lambda_x^{c*}(t, \tau))q^c(t, \tau) d\tau,\\
       &\displaystyle \boldsymbol{\sigma}_x^e(t) = \frac{J^e(0)}{J(0)}\bar{\boldsymbol{\sigma}_x^e}(\lambda_x^{e*}(t, 0))q^e(t, 0) + \frac{j^{e+}}{J(t)} \int\limits_0^t \bar{\sigma_x^e}(\lambda_x^{e*}(t, \tau))q^e(t, \tau) d\tau,\\
       &\displaystyle \boldsymbol{\sigma}_x^g(t) = 2\phi^g c_g\left((\hat{\lambda}((1 + a\sin{(\pi t)}^2)))^2 - \frac{1}{\hat{\lambda}(1 + a\sin{(\pi t)}^2)}\right),\\
       &\displaystyle \bar{\boldsymbol{\sigma}}_x^c = 4c_c(\lambda_x^{c*})^2[(\lambda_x^{c*})^2 - 1]e^{\alpha_c [(\lambda_x^{c*})^2 - 1]^2},\\
       &\displaystyle \bar{\boldsymbol{\sigma}}_x^e = 4c_e(\lambda_x^{e*})^2[(\lambda_x^{e*})^2 - 1],\\
       &\displaystyle \lambda_x^{c*}(t, \tau) = \lambda_{0}^c \frac{(1 + a\sin{(\pi t)}^2)}{(1 + a\sin{(\pi \tau)}^2)}\frac{G_x^c(t)}{G_x^c(\tau)},\\
       &\displaystyle \lambda_x^{e*}(t, \tau) = \lambda_{0}^e \frac{(1 + a\sin{(\pi t)}^2)}{(1 + a\sin{(\pi \tau)}^2)}\frac{G_x^e(t)}{G_x^e(\tau)} \\
    \end{cases}
\end{equation}
```
As a result of executing the script, "stress-time" graphs are displayed, however, you can upgrade the script and output any dependencies for the specified functions.

![strech_cicle](https://drive.google.com/uc?id=16xCtKoHl38UuSnyKi7uUokulHPV95v9-)
### Strech increases linearly 
In script `CMM_strech_increases_linearly.ipynb` the following system of equations is implemented:
```math
\begin{equation} 
    \begin{cases}
        &\boldsymbol{\sigma} = \boldsymbol{\sigma}_x^c + \boldsymbol{\sigma}_x^e + \boldsymbol{\sigma}_x^g,\\
        &\displaystyle \boldsymbol{\sigma}_x^c(t) = \frac{J^c(0)}{J(0)}\bar{\boldsymbol{\sigma}_x^c}(\lambda_x^{c*}(t, 0))q^c(t, 0) + \frac{j^{c+}}{J(t)} \int\limits_0^t \bar{\boldsymbol{\sigma}_x^c}(\lambda_x^{c*}(t, \tau))q^c(t, \tau) d\tau,\\
       &\displaystyle \boldsymbol{\sigma}_x^e(t) = \frac{J^e(0)}{J(0)}\bar{\boldsymbol{\sigma}_x^e}(\lambda_x^{e*}(t, 0))q^e(t, 0) + \frac{j^{e+}}{J(t)} \int\limits_0^t \bar{\boldsymbol{\sigma}_x^e}(\lambda_x^{e*}(t, \tau))q^e(t, \tau) d\tau,\\
       &\displaystyle \boldsymbol{\sigma}_x^g(t) = 2\phi^g c_g\left((\hat{\lambda}(1 + at))^2 - \frac{1}{\hat{\lambda}(1 + at)}\right),\\
       &\displaystyle \bar{\boldsymbol{\sigma}}_x^c = 4c_c(\lambda_x^{c*})^2[(\lambda_x^{c*})^2 - 1]e^{\alpha_c [(\lambda_x^{c*})^2 - 1]^2},\\
       &\displaystyle \bar{\boldsymbol{\sigma}}_x^e = 4c_e(\lambda_x^{e*})^2[(\lambda_x^{e*})^2 - 1],\\
       &\lambda_x^{c*}(t, \tau) = \lambda_{0}^c \frac{(1 + at)}{(1 + a\tau)}\frac{G_x^c(t)}{G_x^c(\tau)},\\
       &\lambda_x^{e*}(t, \tau) = \lambda_{0}^e \frac{(1 + at)}{(1 + a\tau)}\frac{G_x^e(t)}{G_x^e(\tau)}.
    \end{cases} 
\end{equation}
```
As a result of executing the script, "stress-time" graphs are displayed, however, you can upgrade the script and output any dependencies for the specified functions.
![strech_increases_linearly](https://drive.google.com/uc?id=1aHdDiN7VW6J3sWlN_qVVtX7whx-ceLpB)
***
You can upgrade the squeaks and compare different deformation protocols on the same graph.
### CMM with mechanical feedback and the deformation protocols are the same as in CMM 
Before that, I believed that the rate of production of new fibers depends only on time, but in life, the processes of growth and remodeling are controlled by the internal stress of the system. 
According to a number of experimental data, collagen synthesis increases with increasing applied loads. 
As a phenomenological law of remodeling, taking into account this fact, I will use the following ratio for the rate of fiber production:
```math
\begin{align}
    j^{n+}(t)=\frac{J^n(t)}{J^n(0)}  j_0^{n+}[1+K^{n+}\cdot(\hat{\boldsymbol{\sigma}}-1)]
\end{align}
```
where
```math
\begin{align}
    \hat{\boldsymbol{\sigma}} = \frac{\boldsymbol{\sigma}^n}{\boldsymbol{\sigma}_0^n},   
\end{align}
```
and $\sigma_0^n$ a kind of homeostatic tension for $n$ fiber families, $j_0^{n+}$ a positive constant.

Taking into account the new law for the rate of production of new fibers, I obtain the following system of Volterra integral equations of the second kind for fiber tension and partial volume of collagen:
```math
\begin{equation}
    \begin{cases}
       &\displaystyle \boldsymbol{\sigma}_x^c(t) = \frac{J^c(0)}{J(0)}\bar{\boldsymbol{\sigma}_x^c}(\lambda_x^{c*}(0, 0))q^c(0, 0) +
       \frac{1}{J(t)} \int\limits_0^t J^c(\tau) k^{c+}[1 + K^{c+}(\hat{\boldsymbol{\sigma}} - 1)]\bar{\boldsymbol{\sigma}_x^c}(\lambda_x^{c*}(t, \tau))q(t, \tau) d\tau, \\
       &\displaystyle J^c(t) = J^c(0)q^c(0, 0) +  \int\limits_0^t J^c(\tau) k^{c+}[1 + K^{c+}(\hat{\boldsymbol{\sigma}} - 1)]q(t, \tau) d\tau.
    \end{cases}
\end{equation}
```
At the same time, I will assume that only collagen synthesis obeys the feedback law, the law of growth and remodeling for elastin remains unchanged.

I transform the system by replacing integrals by a sum using the trapezoid method and the formula of the iterative method:
```math
\begin{equation}
    \begin{cases}
       &\displaystyle \boldsymbol{\sigma}_{x[k+1]}^c(t_{i}) = \frac{J^c(0)}{J(0)}\bar{\boldsymbol{\sigma}_x^c}(\lambda_x^{c*}(0, 0))q^c(0, 0) +
       \frac{1}{J_{[k]}(t_i)} \cdot \frac{h}{2} \sum_{j=1}^{N}[ J_{[k]}^c(t_i) k^{c+}[1 + K^{c+}(\hat{\boldsymbol{\sigma}} - 1)]\bar{\boldsymbol{\sigma}_x^c}(\lambda_x^{c*}(t_i, t_j))q^c(t_i, t_j) + 
       J_{[k-1]}^c(t_i) k^{c+}[1 + K^{c+}(\hat{\boldsymbol{\sigma}} - 1)]\bar{\boldsymbol{\sigma}_x^c}(\lambda_x^{c*}(t_i, t_{j-1}))q^c(t_i, t_{j-1})],\\
       &J_{[k+1]}^c(t_i) = J^c(0)q^c(0, 0) + \frac{h}{2} \sum_{j=1}^{N}[ J_{[k]}^c(t_i) k^{c+}[1 + K^{c+}(\hat{\boldsymbol{\sigma}} - 1)]q^c(t_i, t_j) + 
       J_{[k-1]}^c(t_i) k^{c+}[1 + K^{c+}(\hat{\boldsymbol{\sigma}} - 1)]q^c(t_i, t_{j-1})],
    \end{cases}
\end{equation}
```
where $k$ - iteration number, $h$ - integration step, $t_j = jh$ for $j = 0, 1, 2, ..., N$.
As a homeostatic stress, I take
```math
\begin{align}
    &\boldsymbol{\sigma}^c_0 \equiv \boldsymbol{\sigma}_x^c(0) =  \frac{J^c(0)}{J(0)}\bar{\boldsymbol{\sigma}_x^c}(\lambda_x^{c*}(0, 0))q^c(0, 0)\\
    %&J^c(0) = J^c(0)q^c(0, 0)
\end{align}
```
where $J^c(0) = \phi_0^c$
At each time step, the value is calculated using a simple iteration method $\sigma_x^c$ и $J^c(t)$, and after the calculation, the norm of the difference of values is considered $\|\sigma_{x[k]}^c(t_i) - \sigma_{x[k-1]}^c(t_i)\|$ и $\|J_{[k]}^c(t_i) - J_{[k-1]}^c(t_i)\|$ and if both of these values are less than the specified epsilon $(\epsilon = 10^{-4})$, then the obtained values for this time step are stored in an array and the transition to the next time step is performed and the iterative procedure is repeated, but for $t_{i+1}$. If the condition is not met, the iterative procedure is repeated until the condition is met:
```math
\begin{align}
\begin{cases}
   \|\boldsymbol{\sigma}_{x[k]}^c(t_i) - \boldsymbol{\sigma}_{x[k-1]}^c(t_i)\| \textless \epsilon \\
    \|J_{[k]}^c(t_i) - J_{[k-1]}^c(t_i)\|  \textless \epsilon 
\end{cases}
\end{align}
```
As a result, by analogy with the CMM, I obtain such systems of equations:
#### Strech constant
```math
\begin{equation}
    \begin{cases}
        &\displaystyle \boldsymbol{\sigma} = \boldsymbol{\sigma}_x^c + \boldsymbol{\sigma}_x^e + \boldsymbol{\sigma}_x^g,\\
        &\displaystyle \boldsymbol{\sigma}_x^c(t_{k+1}) = \frac{J^c(0)}{J(0)}\bar{\boldsymbol{\sigma}_x^c}(\lambda_x^{c*}(0, 0))q^c(0, 0) + 
        \frac{1}{J(t_k)} \cdot \frac{h}{2} \sum_{k=1}^{N}[ J^c(t_k) k^{c+}[1 + K^{c+}(\hat{\boldsymbol{\sigma}} - 1)]\bar{\boldsymbol{\sigma}_x^c}(\lambda_x^{c*}(t, t_k))q^c(t, t_k) + 
        J^c(t_{k-1}) k^{c+}[1 + K^{c+}(\hat{\boldsymbol{\sigma}} - 1)]\bar{\boldsymbol{\sigma}_x^c}(\lambda_x^{c*}(t, t_{k-1}))q^c(t, t_{k-1})],\\
       &\displaystyle J^c(t_{k+1}) = J^c(0)q(0, 0) + \frac{h}{2} \sum_{k=1}^{N}[ J^c(t_k) k^{c+}[1 + K^{c+}(\hat{\boldsymbol{\sigma}} - 1)]q^c(t, t_k) + 
       J^c(t_{k-1}) k^{c+}[1 + K^{c+}(\hat{\boldsymbol{\sigma}} - 1)]q^c(t, t_{k-1})],\\
       &\displaystyle \boldsymbol{\sigma}_x^e(t) = \frac{J^e(0)}{J(0)}\bar{\boldsymbol{\sigma}_x^e}(\lambda_x^{e*}(t, 0))q^e(t, 0) + \frac{j^{e+}}{J(t)} \int\limits_0^t \bar{\boldsymbol{\sigma}_x^e}(\lambda_x^{e*}(t, \tau))q^e(t, \tau) d\tau,\\
       &\displaystyle \boldsymbol{\sigma}_x^g(t) = 2\phi^g c_g\left(\hat{\lambda}^2 - \frac{1}{\hat{\lambda}}\right),\\
       &\displaystyle \bar{\boldsymbol{\sigma}}_x^c = 4c_c(\lambda_x^{c*})^2[(\lambda_x^{c*})^2 - 1]e^{\alpha_c [(\lambda_x^{c*})^2 - 1]^2},\\
       &\displaystyle \bar{\boldsymbol{\sigma}}_x^e = 4c_e(\lambda_x^{e*})^2[(\lambda_x^{e*})^2 - 1],\\
       &\displaystyle \lambda_x^{c*}(t, \tau) = \lambda_{0}^c \frac{G_x^c(t)}{G_x^c(\tau)},\\
       &\displaystyle \lambda_x^{c*}(t, \tau) = \lambda_{0}^c \frac{G_x^c(t)}{G_x^c(\tau)}.
    \end{cases}
\end{equation}
```

#### Strech cicle
```math
\begin{equation}
    \begin{cases}
        &\displaystyle \boldsymbol{\sigma} = \boldsymbol{\sigma}_x^c + \boldsymbol{\sigma}_x^e + \boldsymbol{\sigma}_x^g,\\
        &\displaystyle \boldsymbol{\sigma}_x^c(t_{k+1}) = \frac{J^c(0)}{J(0)}\bar{\boldsymbol{\sigma}_x^c}(\lambda_x^{c*}(0, 0))q^c(0, 0) + 
        \frac{1}{J(t_k)} \cdot \frac{h}{2} \sum_{k=1}^{N}[ J^c(t_k) k^{c+}[1 + K^{c+}(\hat{\boldsymbol{\sigma}} - 1)]\bar{\boldsymbol{\sigma}_x^c}(\lambda_x^{c*}(t, t_k))q^c(t, t_k) +
        J^c(t_{k-1}) k^{c+}[1 + K^{c+}(\hat{\boldsymbol{\sigma}} - 1)]\bar{\boldsymbol{\sigma}_x^c}(\lambda_x^{c*}(t, t_{k-1}))q^c(t, t_{k-1})],\\
       &\displaystyle J^c(t_{k+1}) = J^c(0)q^c(0, 0) + \frac{h}{2} \sum_{k=1}^{N}[ J^c(t_k) k^{c+}[1 + K^{c+}(\hat{\boldsymbol{\sigma}} - 1)]q^c(t, t_k) + 
       J^c(t_{k-1}) k^{c+}[1 + K^{c+}(\hat{\boldsymbol{\sigma}} - 1)]q^c(t, t_{k-1})],\\
       &\displaystyle \boldsymbol{\sigma}_x^e(t) = \frac{J^e(0)}{J(0)}\bar{\boldsymbol{\sigma}_x^e}(\lambda_x^{e*}(t, 0))q^e(t, 0) + \frac{j^{e+}}{J(t)} \int\limits_0^t \bar{\boldsymbol{\sigma}_x^e}(\lambda_x^{e*}(t, \tau))q^e(t, \tau) d\tau,\\
       &\displaystyle \boldsymbol{\sigma}_x^g(t) = 2\phi^g c_g\left(\hat{\lambda}((1 + a\sin{(\pi t)}^2))^2 - \frac{1}{\hat{\lambda}(1 + a\sin{(\pi t)}^2)}\right),\\
       &\displaystyle \bar{\boldsymbol{\sigma}}_x^c = 4c_c(\lambda_x^{c*})^2[(\lambda_x^{c*})^2 - 1]e^{\alpha_c [(\lambda_x^{c*})^2 - 1]^2}, \\
       &\displaystyle\bar{\boldsymbol{\sigma}}_x^e = 4c_e(\lambda_x^{e*})^2[(\lambda_x^{e*})^2 - 1], \\
       &\displaystyle \lambda_x^{c*}(t, \tau) = \lambda_{0}^c \frac{(1 + a\sin{(\pi t)}^2)}{(1 + a\sin{(\pi \tau)}^2)}\frac{G_x^c(t)}{G_x^c(\tau)}, \\
       &\displaystyle \lambda_x^{e*}(t, \tau) = \lambda_{0}^e \frac{(1 + a\sin{(\pi t)}^2)}{(1 + a\sin{(\pi \tau)}^2)}\frac{G_x^e(t)}{G_x^e(\tau)}.
    \end{cases}
\end{equation}
```

#### Strech increases linearly
```math
\begin{align}
    \begin{cases}
        &\displaystyle \boldsymbol{\sigma} = \boldsymbol{\sigma}_x^c + \boldsymbol{\sigma}_x^e + \boldsymbol{\sigma}_x^g,\\
        &\displaystyle \boldsymbol{\sigma}_x^c(t_{k+1}) = \frac{J^c(0)}{J(0)}\bar{\boldsymbol{\sigma}_x^c}(\lambda_x^{c*}(0, 0))q^c(0, 0) +
        \frac{1}{J(t_k)} \cdot \frac{h}{2} \sum_{k=1}^{N}[ J^c(t_k) k^{c+}[1 + K^{c+}(\hat{\boldsymbol{\sigma}} - 1)]\bar{\boldsymbol{\sigma}_x^c}(\lambda_x^{c*}(t, t_k))q^c(t, t_k) + 
        J^c(t_{k-1}) k^{c+}[1 + K^{c+}(\hat{\boldsymbol{\sigma}} - 1)]\bar{\boldsymbol{\sigma}_x^c}(\lambda_x^{c*}(t, t_{k-1}))q^c(t, t_{k-1})],\\
       &\displaystyle J^c(t_{k+1}) = J^c(0)q^c(0, 0) + \frac{h}{2} \sum_{k=1}^{N}[ J^c(t_k) k^{c+}[1 + K^{c+}(\hat{\boldsymbol{\sigma}} - 1)]q^c(t, t_k) + 
       J^c(t_{k-1}) k^{c+}[1 + K^{c+}(\hat{\boldsymbol{\sigma}} - 1)]q^c(t, t_{k-1})],\\
       &\displaystyle \boldsymbol{\sigma}_x^e(t) = \frac{J^e(0)}{J(0)}\bar{\boldsymbol{\sigma}_x^e}(\lambda_x^{e*}(t, 0))q^e(t, 0) + \frac{j^{e+}}{J(t)} \int\limits_0^t \bar{\boldsymbol{\sigma}_x^e}(\lambda_x^{e*}(t, \tau))q^e(t, \tau) d\tau,\\
       &\displaystyle \boldsymbol{\sigma}_x^g(t) = 2\phi^g c_g(\hat{\lambda}(1 + at)^2 - \frac{1}{\hat{\lambda}(1 + at)}),\\
       &\displaystyle \bar{\boldsymbol{\sigma}}_x^c = 4c_c(\lambda_x^{c*})^2[(\lambda_x^{c*})^2 - 1]e^{\alpha_c [(\lambda_x^{c*})^2 - 1]^2},\\
       &\displaystyle \bar{\boldsymbol{\sigma}}_x^e = 4c_e(\lambda_x^{e*})^2[(\lambda_x^{e*})^2 - 1], \\
       &\displaystyle \lambda_x^{c*}(t, \tau) = \lambda_{0}^c \frac{(1 + at)}{(1 + a\tau)}\frac{G_x^c(t)}{G_x^c(\tau)},\\
       &\displaystyle \lambda_x^{e*}(t, \tau) = \lambda_{0}^e \frac{(1 + at)}{(1 + a\tau)}\frac{G_x^e(t)}{G_x^e(\tau)}.
    \end{cases}
\end{align}
``` 
*** 
In this script, all the deformation protocols I am interested in are implemented at once and graphs of all three are displayed at once, however, you can upgrade the script and output only the information that interests you.


## Contributing

If you have any suggestions or improvements for the scripts, feel free to open a pull request (or you can email me: karina_urazova@icloud.com) or create an issue on the repository.

***
**Thank you for your interest in the Constrained Mixture Model with/without mechanical feedback project. I hope this framework proves valuable for your research and applications.**

