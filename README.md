# RTK-UH-Optimization-Algorithms

**"Ensemble Optimization for Calibrating RTK Unit Hydrographs"**


## Description

This project provides the Python implementation of five metaheuristic algorithms used to calibrate the RTK unit hydrograph for a Rainfall derived inflow and infiltration assessment.

The algorithms implemented are:

* Differential Evolution (DE)
* Particle Swarm Optimization (PSO)
* Genetic Algorithm (GA)
* Simulated Annealing (SA)
* Covariance Matrix Adaptation Evolution Strategy (CMA-ES)

## Repository Structure

The repository is organized as follows:

```
├── README.md                                            # This explanation file                                  
├── Optimization_RTK_Functions.ipynb                     # A Python script containing shared code ( function for RDII calculation, Plotting , metrices calculations..)
│
├── Differential Evolution.ipynb                         # Notebook for the DE run
├── Particle swarm optimization.ipynb                    # Notebook for the PSO run
├── Genetic Algorithm.ipynb                              # Notebook for the GA run
├── Simulated annealing.ipynb                            # Notebook for the SA run
├── CMA-ES.ipynb                                         # Notebook for the CMA-ES run
│
├── Calibration Analysis.ipynb                          # To analyse the individual / Ensemble calibration perfromance
├── Validation Analysis.ipynb                           # To analyse the individual / Ensemble validation perfromance
```

## Methodology Workflow
It is implemented in three main stages:

Parameter Optimization: Running the algorithms to find the best RTK parameters for each storm event.
Performance Analysis: Analyzing how well the optimized parameters simulate a given event.
Cross-Validation: Testing the robustness of the parameters on events they were not trained on.


### Part 1: Initial Parameter Optimization
For each storm event, the goal is to find a set of optimal RTK parameters using the provided optimization algorithms.

Prepare Input Data: For each event, create an Excel file (.xlsx) containing three columns: Timesteps, Observed RDII, and Rainfall.

Set Initial Conditions: In the appropriate Jupyter Notebook (e.g., Differential Evolution.ipynb), configure the global parameters:

catchment_area_acres: The area of the sewershed.
time_step_seconds: The duration of each time step in seconds (e.g., 600 for 10 minutes).

Define the search range (minimum and maximum values) for the T and K parameters.

Run the Optimization: Execute the notebook cells. The chosen algorithm will run 20 times.

Export Results: Upon completion, save the results to an Excel file. 

RTK Parameters Sheet: The optimized R, T, and K values for each of the 20 runs.
Performance Metrics Sheet: The calculated R², NSE, RMSE, PBIAS, and Fitness scores for each run.

### Part 2: Performance Analysis of a Single Event
This stage involves analyzing the performance of an algorithm or an ensemble of parameters for a specific event.

Load Event Data: Start with the data for the event you wish to analyze (Rainfall, Observed RDII, Time step).
Select Configuration: Choose the algorithm or ensemble of parameters to be analyzed.
Generate and Save Plot: The analysis script will produce and save a figure that visualizes:
The observed flow.
The flow simulated using the optimized parameters.
A text box displaying the final performance metric scores.

### Part 3: Leave-One-Out Cross-Validation 
This is the final validation step to test how well the optimized parameters generalize to unseen data.

Select Validation Event: Choose one storm event to be the "validation" event.
Prepare Parameter Set: The analysis is performed using an ensemble of RTK parameters from all other events, deliberately excluding the parameters that were generated from the validation event itself.
Run Validation: The script uses this "leave-one-out" parameter set to simulate the flow for the validation event.
Generate and Save Plot: As in the performance analysis, a final plot is generated and saved, comparing the observed and simulated flows and displaying the corresponding performance metrics. This demonstrates the robustness and predictive power of the methodology.
