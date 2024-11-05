# Running the Model and Interpreting Results

## Running the Model

1. Ensure GAMS is installed on your system.
2. Open `transport_model.gms` in GAMS.
3. Run the model by pressing the **Run** button.

## Interpreting the Output

The model will display the following results:
- **x.l**: Optimal number of each transport type sent to each conflict zone.
- **total_risk.l**: The minimized total risk of the transportation plan.

These values tell you how many of each aircraft type should be deployed to each conflict zone to meet the demand while minimizing risk.

## Example Output (Hypothetical)

---- 10 VARIABLE x.L Number of transports per type per zone

mathematica
Copy code
          A         B         C         D         E
helicopter 3 5 4 0 3 light_aircraft 1 2 3 3 1 heavy_aircraft 1 0 2 0 1

---- 10 VARIABLE total_risk.L Total transportation risk

total_risk = 1540
