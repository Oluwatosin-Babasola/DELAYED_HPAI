# HPAI Transmission Dynamics Model with Vaccination Delays

A compartmental model for simulating Highly Pathogenic Avian Influenza (HPAI) transmission dynamics in human populations, incorporating vaccination delays, behavioral groups, and intervention strategies.

## Overview

This repository implements a time-delayed compartmental model to analyze HPAI outbreak dynamics in a human population stratified by vaccination acceptance. The model captures critical epidemiological features such as:

- **Vaccination delays**: Pre-deployment delay ($\tau_P$) and vaccine-to-protection delay ($\tau_V$)
- **Incubation period**: Fixed delay between exposure and infectiousness ($\tau_E$)
- **Dual population groups**: Vaccine-accepting and vaccine-hesitant individuals
- **Partial vaccine efficacy**: Residual susceptibility ($\epsilon$) in vaccinated individuals
- **Non-pharmaceutical interventions**: Compliance with transmission-reducing measures ($c_n$)
- **Vaccination dynamics**: Rate ($\nu$) and compliance ($c_v$) parameters

## Model Structure

The model tracks 10 compartments across two population groups:

**Accepting Group**: $S_a$, $W_a$, $P_a$, $E_a$, $I_a$, $R_a$
- $S_a$: Susceptible individuals
- $W_a$: Vaccinated waiting class (no protection yet)
- $P_a$: Protected class (vaccine-induced immunity)
- $E_a$: Exposed (infected, not yet infectious)
- $I_a$: Infectious
- $R_a$: Recovered

**Hesitant Group**: $S_h$, $E_h$, $I_h$, $R_h$
- $S_h$: Susceptible individuals
- $E_h$: Exposed
- $I_h$: Infectious
- $R_h$: Recovered

The force of infection is given by:
$$\lambda(t) = \beta(1-c_n)\frac{I_a(t) + I_h(t)}{N(t)}$$

## Key Features

### 1. Time Delays
- **Incubation delay** ($\tau_E$): Time from exposure to infectiousness
- **Vaccine-to-protection delay** ($\tau_V$): Time from vaccination to protection
- **Pre-deployment delay** ($\tau_P$): Time before vaccination begins
- **Survival probability**: Accounts for infection during waiting period

### 2. Vaccination Dynamics
- Vaccination only administered to susceptible individuals
- Vaccinated individuals enter waiting class ($W_a$) with full susceptibility
- Survival probability calculation ensures only uninfected individuals gain protection
- Partial protection ($\epsilon$) for breakthrough infections

### 3. Population Stratification
- Two groups with identical biology but different vaccination behaviors
- Force of infection depends on total infectious population
- No cross-immunity between groups

## Parameter Definitions

| Parameter | Description | Baseline | Range |
|-----------|-------------|---------|-------|
| $\tau_E$ | Incubation delay | 2 days | 1-5 days |
| $\gamma$ | Recovery rate | 0.2 day⁻¹ | 0.1-0.3 day⁻¹ |
| $\tau_V$ | Vaccine-to-protection delay | 14 days | 7-35 days |
| $\tau_P$ | Pre-deployment delay | 120 days | 60-180 days |
| $R_0$ | Basic reproduction number | 1.7 | 0.8-2.5 |
| $c_n$ | NPI compliance | 0.40 | 0.0-0.7 |
| $\nu$ | Vaccination rate | 0.02 day⁻¹ | 0.005-0.05 day⁻¹ |
| $c_v$ | Vaccination compliance | 0.70 | 0.5-0.9 |
| $\epsilon$ | Residual susceptibility | 0.40 | 0.2-0.7 |
| $q_{accept}$ | Vaccination acceptance | 0.70 | 0.5-0.9 |


# Install required packages
pip install numpy matplotlib scipy
