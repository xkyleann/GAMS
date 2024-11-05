# Soldier Transportation Optimization

This repository contains a GAMS model to optimize the transportation of soldiers to multiple conflict zones while minimizing transportation risk.

## Problem Overview

Two battalions of 500 soldiers each (totaling 1000 soldiers) need to be transported to 5 conflict zones (A-E). The available transportation options include:
- 15 helicopters, each carrying up to 20 soldiers.
- 10 light transportation aircraft, each carrying up to 40 soldiers.
- 5 heavy transportation aircraft, each carrying up to 80 soldiers.

The transportation risk varies by aircraft type:
- Helicopter: Risk per soldier = 1
- Light aircraft: Risk per soldier = 2
- Heavy aircraft: Risk per soldier = 3

The objective is to determine the optimal allocation of transportation resources to minimize the total transportation risk while meeting the soldier demand at each conflict zone.

## Repository Contents

- `model_description.md`: Detailed explanation of the GAMS model.
- `transport_model.gms`: GAMS code to solve the optimization problem.
- `results.md`: Instructions for running the model and interpreting results.

## Requirements

To run this model, you need GAMS software installed on your system.

## Getting Started

1. Clone this repository.
2. Open `transport_model.gms` in GAMS.
3. Run the model to generate the optimal transportation plan.

For more details, refer to `model_description.md`.
