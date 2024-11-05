
---

#### 3. `transport_model.gms`

```GAMS
* transport_model.gms
* GAMS model for optimizing soldier transportation to conflict zones

Sets
    t          /helicopter, light_aircraft, heavy_aircraft/
    z          /A, B, C, D, E/;

Parameters
    demand(z)   Soldiers required at each conflict zone
              / A 150, B 200, C 250, D 200, E 200 /
    
    capacity(t) Soldiers capacity per transport type
              / helicopter 20, light_aircraft 40, heavy_aircraft 80 /
    
    max_units(t) Maximum number of units available per type
              / helicopter 15, light_aircraft 10, heavy_aircraft 5 /
    
    risk(t)     Risk factor per soldier per transport type
              / helicopter 1, light_aircraft 2, heavy_aircraft 3 /
    ;

Table connections(t, z) Possible connections between transport type and conflict zone (1=connection available, 0=not available)
              A    B    C    D    E
    helicopter  1    1    1    1    1
    light_aircraft  1    1    1    1    1
    heavy_aircraft  1    0    1    0    1
    ;

Variables
    x(t, z)   Number of transports of type t sent to zone z
    total_risk Total transportation risk;

Positive Variables x;

Equations
    obj       Objective function to minimize total risk
    supply    Total soldiers to be transported constraint
    zone_demand(z) Demand constraint for each conflict zone
    max_avail(t) Maximum availability constraint for each transport type
    ;

obj .. total_risk =e= sum((t, z), risk(t) * capacity(t) * x(t, z));

supply .. sum((t, z), capacity(t) * x(t, z)) =e= 1000;

zone_demand(z) .. sum(t$(connections(t,z)), capacity(t) * x(t, z)) =e= demand(z);

max_avail(t) .. sum(z, x(t, z)) =l= max_units(t);

Model transport_model /all/;
Solve transport_model using lp minimizing total_risk;

Display x.l, total_risk.l;
