
Calculation type for outlet stream temperature on first side
Calculation types for second side may be given below in TYPE2.
Note duty is positive when added to stream and
negative when subtracted from stream.

TYPE=1:  Outlet temperature
TYPE=2:  Duty
TYPE=4:  Dew point temperature plus increment
TYPE=5:  Bubble point temperature plus increment
TYPE=6:  Temperature increment 
TYPE=7:  Temperature and pressure already given in outlet stream
TYPE=8:  Temperature increment relative to temperature 
         in stream specified below
TYPE=9:  Duty fetched as sum of one or more operations
         as specified below, but with sign reversed
TYPE=10: Outlet temperature and duty specified. Feed flow
         on first side is scaled. 
TYPE=11: Evaporation of feed stream (boiler and chiller case)
         Conditions and duty type are specified in the 
         boiler and condenser section
TYPE=12: Condensation of the feed stream
         Conditions and duty type are specified in the
         boiler and condenser section
TYPE=13: Duty and temperature. Used when supplier
         data are transferred to IES. Will result in a GHEMB
         heat balance error due to over specification
TYPE=14: Second side is specified. Outlet temperature 
         on first side is determined from approach to inlet 
         temperature on second side.
         Outlet temperature on second side given in TYPE2 below.
         Note only valid for counter-current flow.
TYPE=15: Duty is fetched from another exchanger using DTTYP>=5
         Outlet temperature is determined from temperature 
         approach relative to inlet temperature on fetched side.
         Feed flow is scaled to give the fetched duty. 