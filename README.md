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
When writing the model scripts, I relied on the scientific works of Larry Taber ""

## Contributing

If you have any suggestions or improvements for the scripts, feel free to open a pull request (or you can email me: karina_urazova@icloud.com) or create an issue on the repository.


