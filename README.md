# Constrained Mixture Model & Constrained Mixture Model with Mechanical Feedback for stress analysis in various soft tissue deformation protocols

In this repository, you will find Python scripts for implementing constrained mixture models with different deformation protocols. The scripts are based on mathematical models of constrained mixture models and constrained mixture models with mechanical feedback.

## Installation

To run the scripts, you will need to have Python installed on your machine. You can download Python from the official website: [https://www.python.org/](https://www.python.org/)

You will also need to install the following Python libraries:

```
pip install numpy
pip install scipy
pip install matplotlib
```

## Usage

1. Clone the repository to your local machine:

```
git clone https://github.com/karinaurazova/constrained-mixture-models.git
```

2. Run the Python script for the desired model:

- `CMM_strech_constant.ipynb`: Implementation of the constrained mixture model with constant strech.
- `CMM_strech_cicle.ipynb`: Implementation of the constrained mixture model with cicle strech.
- `CMM_strech_increases_linearly.ipynb`: Implementation of the constrained mixture model with strech increases linearly.
- `CMM_with_mechanical_feedback.ipynb`: Implementation of the constrained mixture model with mechanical feedback, the following functions are written in this script constant strech, cicle strech, strech increases linearly.

3. Follow the instructions provided in the script for running simulations with different deformation protocols.

## Theory
These mathematical models are used to analyze the stress state of tendons and ligaments, but you can upgrade them for any soft tissue, not just unidirectional collagen fibers.
When writing the model scripts, I relied on the scientific works of Larry Taber  "Continuum Modeling in Mechanobiology" https://link.springer.com/book/10.1007/978-3-030-43209-6


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

### Strech increases linearly 
In script `CMM_strech_increases_linearly.ipynb` the following system of equations is implemented:

## Contributing

If you have any suggestions or improvements for the scripts, feel free to open a pull request (or you can email me: karina_urazova@icloud.com) or create an issue on the repository.

***
Thank you for your interest in the Constrained Mixture Model with/without mechanical feedback project. I hope this framework proves valuable for your research and applications.

