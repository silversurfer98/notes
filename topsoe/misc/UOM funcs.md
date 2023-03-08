
# Unit of Measurement Functions
    
| DimLess |        |
|:-------|:-------|
| Purpose | To return the argument as a dimensionless number. |
| Syntax | DimLess(x) |
|        | Where x is a floating point value without a UoM. |
| Return value | DimLess (x) returns the x as a dimension less number. |
| Example | X = DimLess(2)<br>Y = 1.5{m}<br>Z = X\*Y<br>\* Z will now have the value 3m |

$~~$

| GetUnit |        |
|:-------|:-------|
| Purpose | To return the UoM name. |
| Syntax | GetUnit(x) |
|        | Where x is a floating point value. |
| Return value | GetUnit(x) returns the name of the UoM for expression x. |

$~~$

| GetUnitType |        |
|:-------|:-------|
| Purpose | To return the type of UoM. |
| Syntax | GetUnitType(x) |
|        | Where x is a floating point value. |
| Return value | GetUnitType(x) returns the type of UoM for expression x. |

$~~$

| GetUnitSymbol |        |
|:-------|:-------|
| Purpose | To return the UoM symbol. |
| Syntax | GetUnitSymbol(x) |
|        | Where x is a floating point value. |
| Return value | GetUnitSymbol(x) returns the symbol of the UoM for expression x. |

$~~$

| SetUnit |        |
|:-------|:-------|
| Purpose | To set the UoM for a floating point value. |
| Syntax | SetUnit(x,y,z) |
|        | Where x is a floating point value without a UoM, y is the type and z is the name of the UoM to be used. |
| Return value | SetUnit(x) returns the value of x with the specified UoM. |

$~~$

| UnitConv |        |
|:-------|:-------|
| Purpose | To convert a floating point value. |
| Syntax | UnitConv(x,y) |
|        | Where x is a floating point value and y is the name of the UoM to convert x to. |
| Return value | UnitConv(x) returns the converted value of x. |