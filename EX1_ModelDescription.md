# Model Description

This document provides a detailed breakdown of the GAMS model used to solve the soldier transportation optimization problem.

## Sets

- `t`: Represents the types of transportation options (helicopter, light aircraft, heavy aircraft).
- `z`: Represents the conflict zones (A-E).

## Parameters

- `demand(z)`: Specifies the number of soldiers required at each conflict zone.
- `capacity(t)`: The carrying capacity of each transport type.
- `max_units(t)`: Maximum availability for each type of transport.
- `risk(t)`: The risk factor associated with each type of transport.

## Table

The `connections(t, z)` table indicates which transport types can reach each conflict zone. 

| Transport Type       | A | B | C | D | E |
|----------------------|---|---|---|---|---|
| Helicopter           | 1 | 1 | 1 | 1 | 1 |
| Light Aircraft       | 1 | 1 | 1 | 1 | 1 |
| Heavy Aircraft       | 1 | 0 | 1 | 0 | 1 |

A value of `1` indicates that the transport type can access the zone, while `0` means it cannot.

## Variables

- `x(t, z)`: Decision variable representing the number of each transport type `t` sent to each zone `z`.
- `total_risk`: Total risk of the transportation plan, which is the objective to minimize.

## Equations

- **Objective (obj)**: Minimize total transportation risk based on the risk per soldier.
  
  ```GAMS
  obj .. total_risk =e= sum((t, z), risk(t) * capacity(t) * x(t, z));
