# SIRS Model with Waning Immunity - README

## Overview
This code implements a network-based SIRS (Susceptible-Infected-Recovered-Susceptible) epidemiological model with waning immunity to explore disease seasonality patterns. The model simulates disease spread through a population connected in a network structure.

## Model Description

### Core Components

1. **Agent-based Architecture**: Each individual in the population is represented as an `Agent` object with:
   - Status: 'S' (Susceptible), 'I' (Infected), or 'R' (Recovered)
   - Network connections to other agents
   - Time tracking since last infection

2. **Network Structure**: 
   - Population of 1000 agents
   - Average of 5 connections per agent (2500 total connections randomly distributed)
   - Represents social contact patterns

3. **Disease Dynamics**:
   - **R0 (Basic Reproduction Number)**: 1.8
   - **D (Infectious Period)**: 5 days
   - **Immunity Duration**: Wanes linearly from 100% protection at recovery to 0% protection after 730 days (2 years)

### Key Parameters

- `time_step_length`: 0.01 days (simulation granularity)
- `immunity_time`: 0 days (when 100% immunity ends)
- `immunity_tail`: 730 days (duration of waning immunity)

## Simulation Experiments

### Part 1: Basic SIRS Dynamics
Demonstrates cyclical epidemic patterns emerging from waning immunity alone, without external seasonal forcing.

### Part 2: Multiple Strain Model
Incorporates 10 different strains with varying R0 values (normally distributed around 1.28) and infectious periods, more closely mimicking influenza dynamics.

### Part 3: Seasonal R0 Variation
Adds sinusoidal variation to R0 to model seasonal transmission changes (e.g., increased indoor contact in winter).

## Key Functions

- **`update_network()`**: Core simulation step that:
  - Processes infection transmission based on network connections
  - Handles recovery with probability 1/D per timestep
  - Implements waning immunity for recovered individuals
  
- **Transmission Probability**:
P(transmission) = R0 / (connections × D) × time_step_length

- **Waning Immunity**:
 P(becoming susceptible) = (time_since_infected - immunity_time) / immunity_tail

## Output
The simulation generates time series plots showing the number of active infections over time, demonstrating:
- Epidemic waves
- Seasonal patterns
- Impact of waning immunity on disease persistence

## Scientific Context
This model explores how waning immunity alone can generate seasonal-like patterns in disease incidence, even without external seasonal drivers. This is relevant for understanding respiratory diseases like influenza where both immunity waning and seasonal factors contribute to annual epidemics.

## Usage Notes
- Run times can be long for extended simulations (1000+ days)
- Multiple runs may be needed due to stochastic variation
- The model assumes homogeneous mixing within the network structure
- Does not account for spatial structure, age stratification, or behavioral changes

## Limitations
- Simplified network structure (random connections)
- No vital dynamics (births/deaths)
- Uniform immunity waning across all individuals
- No cross-immunity between strains in the multi-strain version



