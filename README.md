# GAMS
This repository provides an introduction to using GAMS (General Algebraic Modeling System) for mathematical programming and optimization. We’ll go over GAMS syntax, modeling steps, and create a basic example to demonstrate how GAMS works.

- GAMS, or the General Algebraic Modeling System, is a high-level modeling system for mathematical programming and optimization. It’s particularly useful for large-scale problems and is widely used in fields like economics, engineering, and operations research. In GAMS, you can model linear, nonlinear, and mixed-integer optimization problems.
  
#### Understanding GAMS (General Algebraic Modeling System) Workflow
1. **Define Sets** : Represent collections of items (like products, locations, or time periods).
2. **Define the Parameters and Data:** Declare constants and input data.
3. **Define Variables:** Specify the decision variables in the problem.
4. **Set Up Equations:** Define the constraints and objective function for the problem.
5. **Solve:** Use one of GAMS's built-in solvers to find the optimal solution.
6. **Analyze Output:** Check the values of the variables to interpret the solution.

### GAMS Basics
- A GAMS file typically ends with the extension **.gms**, and it consists of declarations, definitions, and commands. Let’s go through these components.

#### Declaring Sets
- Sets are fundamental in GAMS, as they represent indexes for parameters and variables.

```GAMS 
Sets
    i /1*3/    ! Represents items 1 through 3
    j /A, B, C/;  ! Represents items A, B, and C

```

#### Defining Parameters
- Parameters represent data that the model uses, such as costs, demand, or supply.
```GAMS 
Parameters
    a(i)   Cost for each item
    b(j)   Demand for each location
    c(i,j) Transportation cost from item i to location j;

a(i) = 10;   ! Assigning cost of 10 for all items in set i
b("A") = 30; ! Assigning demand of 30 to location A
c(i,j) = uniform(10,50);  ! Assign random values between 10 and 50 for transportation costs
```

#### Defining Variables
- Variables are the values you want to determine through optimization.
```GAMS 
Variables
    x(i,j)  Quantity transported from i to j
    z       Total cost;

Positive Variables x;  ! Declaring x as a positive variable (non-negative)
```
#### Defining Equations 
- Equations in GAMS specify the objective function and constraints.
```GAMS 
Equations
    cost         Define objective function
    supply(i)    Supply constraint for each item
    demand(j)    Demand constraint for each location;

cost .. z =e= sum((i,j), c(i,j) * x(i,j));   ! Objective function: minimize total cost

supply(i) .. sum(j, x(i,j)) =l= a(i);        ! Supply constraint: cannot exceed available amount
demand(j) .. sum(i, x(i,j)) =g= b(j);        ! Demand constraint: must meet demand
```

#### Solve Statement
- This is where you specify the type of optimization (e.g., linear programming, LP) and the objective function.
```GAMS 
Model transport /all/;  ! Create model including all equations
Solve transport using LP minimizing z;  ! Solve model using linear programming
```

#### Displaying Results
- Use **display** to print results.
- Here, **.l** refers to the level value (the solution value) of the variable.
```GAMS 
Display x.l, z.l;
```

----

### Complete Example
-  In a simple transportation model. Suppose we have:
  - 2 suppliers (1 and 2)
  - 2 consumers (A and B)
  - Costs associated with transporting goods from each supplier to each consumer

```GAMS 
Sets
    i /1, 2/
    j /A, B/;

Parameters
    supply(i) /1 100, 2 150/    ! Supply at each supplier
    demand(j) /A 80, B 120/     ! Demand at each consumer
    cost(i,j) /1.A 20, 1.B 40, 2.A 30, 2.B 10/;  ! Transport cost per unit

Variables
    x(i,j)  Quantity transported from supplier i to consumer j
    z       Total transportation cost;

Positive Variables x;

Equations
    total_cost   Objective function
    supply_limit(i) Supply constraint
    demand_satisfaction(j) Demand constraint;

total_cost .. z =e= sum((i,j), cost(i,j) * x(i,j));

supply_limit(i) .. sum(j, x(i,j)) =l= supply(i);

demand_satisfaction(j) .. sum(i, x(i,j)) =g= demand(j);

Model transport /all/;
Solve transport using LP minimizing z;

Display x.l, z.l;
```
- The sets of suppliers and consumers.
- Supply and demand parameters.
- Costs of transporting from each supplier to each consumer.
- Constraints to ensure supply isn’t exceeded and demand is met.
- An objective to minimize transportation costs.

#### Running the Model 
To run this model:

Save it as a .gms file, like transport_model.gms.
Open GAMS, load the file, and run it.
GAMS will solve the optimization and display the results in the output.

#### Analyzing the Output
- The output should show the values of x(i,j).l (the transport quantities) and z.l (total cost), helping you understand the optimal shipping plan to minimize costs.
