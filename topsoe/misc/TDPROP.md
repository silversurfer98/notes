

CDAR3 can be used both **outside and inside** GHEMB, but this manual only describes the particular features inside GHEMB using stream properties directly and jumping around in the GHEMB operation list using conditional jumps. If CDAR3 is specified in GIPS joblist, it is **outside** GHEMB, and the dedicated GHEMB stream variables cannot be used. 

CDAR3 is simply executed by specifying 250003 as a GHEMB operation. 

A GHEMB **stream** variable in UDSTA is identified by its stream number followed by the property name in parentheses, and a GHEMB **operation** variable is identified by its data group name followed by the variable name in parentheses.

The following **stream variables** may be referred to:

| Property name                            | Property                |
|:-----------------------------------------|:------------------------|
| Negative Component Identification Number | Component flow (kmol/h) |
| T                                        | Temperature (Â°C)        |
| P                                        | Pressure (kg/cm$^2$ g)  |
| H                                        | Enthalpy (kcal/h)       |
| F                                        | Total flow (kmol/h)     |
| FNM                                      | Total flow (Nm$^3$/h)   |
| V                                        | Vapor fraction (0-1)    |

The total flow in Nm$^3$/h in stream 1234 is then fetched as:

``â€˜1234(FNM)â€™``

In addition to all operation data group input variables, the **operation output variables** in GHEMB can also be referred to. They are duties, works, and efficiencies, which have common names in all GHEMB operations. The most commonly used ones are duty and work, which have the names: &#36;DUTY, and $WORK, but all variables are found in the sections describing the unit operation. For example, the duty in a heat exchange operation E-204 is referred to as:

``	'E-204($DUTY)'``

An **arithmetric expression** in UDSTA can use the simple arithmetic operators for multiplication, division, addition, and subtraction: *,/,+,-, but also ** for exponential and () for parentheses. 

As an example it is desired to calculate the Space Time Yield (Nm$^3$/h/m$^3$ catalyst) in a reactor with 0.34 m$^3$ of catalyst. It is defined as the consumption of CO (identification No. 5) and CO$_2$ (identification No. 6) over the reactor with inlet stream 1024 and outlet stream 1025 divided by the catalyst volume. The conversion factor 22.414 is from kmol/h to Nm$^3$/h. The result is stored in a local variable called STY. The expression looks like this:

``	'STY = 22.414{}*(1024(-5)+1024(-6)-(1025(-5)+1025(-6)))/0.34{}'``

More advanced expressions are described in the UDSTA guide.
 
In a **conditional statement** it is possible to change the calculation order in the GHEMB operation list. An example would be:

	'IF(STY > 100.) JUMP R 501'

where the calculation order is changed to the GHEMB operation R 501 if the space-time yield is greater than 100. The relational operators <, <=, > and >= can be used. Note that the constant â€˜100.â€™ may have different interpretations depending on the selected UoM. In principle all such constants should have a UoM in agreement with the GIPS standard UoM system.

For **test printing** one could write for example:

	'WRITE STY Space Time Yield (Nm$^3$/h/m$^3$)'

where the explanation on the right side will also be included in the output.

Stream data groups can be **created and then printed** by use of the following statements in a CDAR3 data group (250003):

	'CREATE 1024'
	'OUTPUT STM01024'

where the CREATE statement creates a data group of type 400230 for stream number 1024, whereafter it is printed. It is important that between the 3 characters STM and the stream number, zeros are added such that the generated stream name will consist of 8 characters. If after the OUTPUT statement the following line is added

	'CALL STREAM2INPUT("STM00140")'

and also the â€œstreamdataâ€ copy item is included, the stream data group will be printed in ascii-format. The stream data group in ascii-format can be copied and pasted directly into a calculation, such as [TDYNCALC](../programs/tdyncalc/tdyncalc.md) to check thermodynamics.

Data can also be fetched from the project database by CDAR3 and transferred to a GHEMB stream or operation by use of the commands: 

	'DBSTART'
	'DBEND'

The actual text strings are located between them.

As an example:

	'STM06410 = M04.4610',

copies the stream No. 4610 from module No. 4 in the actual project layout and case No. given in the COVER data group to the local stream data group =STM06410=.

This is further explained in the *[User Manual for Oracle Database Access in GIPS](../programs/dbaccess/dbaccess.md)* (DBACCESS).


## TDPROP functions
The TDPROP function is used to calculate thermodynamic properties of GHEMB streams. Note that it can only be used **inside** GHEMB.

They are invoked by the statement:

``TDPROP(N,PROP,-CN)``

on the right side of an UDSTA expression. 

* N is the stream number.
* PROP the name of the desired total or component property.
* CN is the component identification number for a specific component property, where this is allowed. 

Note that only a few values of PROP can calculate a component property. A warning will be given for illegal specifications.

As an example:

	'R17=TDPROP(1234,MW)'

calculates the mole weight of stream 1234 and assigns its value to a local variable, R17. 

If the printing of thermodynamic properties has been requested in 461562, a table with these data will appear in the output report. If the same property is calculated more than once for the same stream, **only** the last value will be printed.

A **complete list** of the names of all PROP property functions is found below. For many properties more names can be used. The reason is that the originally selected names are not identical to those used in the stream data group with type number 400230. The names from this data group can also be used.

The actual UoM system can here be selected by either

* Using fixed units. These variables can be used in any application program using UDSTA statements and are the most convenient and recommended ones.
Or:

* Using the GIPS global UoM as determined in the local data group, such as 250000-3. These variables are preceded by a #. Note that they cannot be used together with older CDAR3 data groups.

Note that, when the water decant method is used, the liquid TDPROP functions will be based on the combined water and hydrocarbon phase.

â€ƒ
**Basic stream properties in TDPROP functions**
**Component properties cannot be calculated**

| Name using fixed UoM   | Name using GIPS global UoM as selected in an UDSTA application   | Name in 400230     | Significance    |
|:-----------------------|:-----------------------------------------------------------------|:-------------------|:----------------|
| TEMP  [ Â°C]            | #TEMP                                                            | TEMP               | Temperature     |
| PRES  [kg/cm$^2$ g]    | #PRES                                                            | PRES               | Pressure        |
| NM3FL  [Nm$^3$/h]      |                                                                  |                    | Flow, Nm$^3$/h  |
| SM3FL                  |                                                                  |                    | Flow, Sm$^3$/h (standard liquid volume) |
| BARFL                  |                                                                  |                    | Flow, barrels/h |
| DRYMOLFL [kmol/h]      | #DRYMOLF                                                         |                    | Dry mole flow   |
| TOTVOL  [m$^3$/h]      | #TOTVOL                                                          | TOTVOL             | Volume flow     |
| VFLVL  [m$^3$3/h]      | #VFLVL                                                           | Vapor volume flow  |                 |
| LFLVL  [m$^3$3/h]      | #LFLVL                                                           | Liquid volume flow |                 |
| PHAS  [%]              | PHAS                                                             | Vapor mole %       |                 |
| LIQPHAS  [%]           | Liquid mole %                                                    |                    |                 |
| VMASSFR  [%]           | Vapor mass fraction                                              |                    |                 |
| ENTH  [kcal/h]         | #ENTH                                                            | ENTH               | Stream enthalpy |

 
â€ƒ
**Basic properties in TDPROP functions**
**Properties where only component properties can be calculated**

| Name using fixed UoM           | Name using  GIPS global UoM as selected in an UDSTA application | Name in 400230          |   Significance |
|:-------------------------------|:----------------------------------------------------------------|:------------------------|---------------:|
| MOLFR [absolute]               |                                                                 |                         | Component mole fraction|
| MOLPCT  [%]                    |                                                                 | MOLE                    | Component mole % |
| MOLPPM  [ppm]                  |                                                                 |                         | Component mole ppm |
| DRYPCT  [%]                    |                                                                 |                         | Component dry mole % |
| Example:                       |                                                                 |                         |             |
| TDPROP(10,DRYPCT,-1)           |                                                                 |                         | Dry mole % H$_2$ in stream 10             |
| DRYPPM  [ppm]                  |                                                                 |                         | Component dry mole ppm |
| WTPCT  [%]                     |                                                                 |                         | Component weight % |
| Example:                       |                                                                 |                         |             |
| TDPROP(10,WTPCT,-78)           |                                                                 |                         | Weight % H$_2$SO$_4$ in stream 10             |
| WTPPM  [ppm]                   |                                                                 |                         | Component weight ppm |
| DWTPPM  [ppm]                  |                                                                 |                         | Component dry weight ppm| 
| VMOLPCT  [%]                   |                                                                 |                         | Vapor mole %|
| VWTPCT  [%]                    |                                                                 | VMOLE                   | Vapor weight %|
| LMOLPCT  [%]                   | Liquid mole %                                                     |                         |             |
| LWTPCT  [%]                    | LMOLE                                                             | Liquid weight %         |             |
| GASDIF  [m$^2$/h]              |                                                                   |                         |             |
| Gas bulk diffusion coefficient |                                                                   |                         |             |
| PARTPRS [atm.abs]              | Component partial pressure                                        |                         |             |
| COMPINDX                       | COMPINDX                                                          | Component index in list |             |
| NCOMP                          | NCOMP                                                             | Number of components    |             |


â€ƒ
**Basic properties in TDPROP functions**
**Properties where total or component property can be calculated using the same name**

| Name using fixed UoM        | Name using GIPS global UoM as selected in an UDSTA application   | Name in 400230   | Significance                         |
|:----------------------------|:-----------------------------------------------------------------|:-----------------|:-------------------------------------|
| KGFL  [kg/h]                | #MASSFL                                                          | TOTKG            |                                      |
| CFLM                        | Total or component mass flow                                     |                  |                                      |
| E.g.: TDPROP(10,KGFL,-2)     |                                                                  |                  |                                      |
| Kg flow of H2O in stream 10 |                                                                  |                  |                                      |
| MOLFL [kmol/h]              | #MOLFL                                                           | TOTFL            |                                      |
| CFLW                        | Total or component molar flow                                    |                  |                                      |
| E.g.: TDPROP(10,#MOLFL)       |                                                                  |                  |                                      |
| Mole flow in stream 10      |                                                                  |                  |                                      |
| TDPROP(10,MOLFL,-2)         |                                                                  |                  |                                      |
| Kmol/h of H2O in stream 10  |                                                                  |                  |                                      |
| MW [kg/kmol]                | #MW                                                              | AVM              | Total or component molecular weight  |
| E.g.: TDPROP(10,MW,-2)        |                                                                  |                  |                                      |
| Mole weight of H2O          |                                                                  |                  |                                      |
| VFLOW  [kmol/h]             | #VFLOW                                                           | VCFLW            | Total or component vapor molar flow  |
| VFLKG  [kg/h]               | #VFLKG                                                           | VMFLW            | Total or component vapor mass flow   |
| LFLOW  [kmol/h]             | #LFLOW                                                           | LCFLW            | Total or component liquid molar flow |
| LFLKG [kmol/h]              | #LFLKG                                                           | LMFLW            | Total or component liquid mass flow  |


â€ƒ
**Thermodynamic and transport properties in TDPROP functions**
**Component properties cannot be calculated**

| Name using fixed UoM   | Name using GIPS global UoM as selected in an UDSTA application   | Name in 400230                                                                             | Significance                                                                               |
|:-----------------------|:-----------------------------------------------------------------|:-------------------------------------------------------------------------------------------|:-------------------------------------------------------------------------------------------|
| LHV  [kcal/Nm$^3$]     | #LHV                                                             | LHV                                                                                        | Lower heating value                                                                        |
| HHV [kcal/Nm$^3$]      | #HHV                                                             | HHV                                                                                        | Higher heating value                                                                       |
| WOBLHV [kcal/Nm$^3$]   | #WOBLHV                                                          | WOBBE                                                                                      | Wobbe number. As LHV, but divided by the square root of the specific gravity, also at 25Â°C |
| WOBHHV [kcal/Nm$^3$]   | #WOBHHV                                                          | Wobbe number. As HHV, but divided by the square root of the specific gravity, also at 25Â°C |                                                                                            |
| DEN  [kg/m$^3$]        | #DEN                                                             | DENS                                                                                       | Mixture density                                                                            |
| LDEN [kg/m$^3$]        | #LDEN                                                            | LDENS                                                                                      | Liquid density                                                                             |
| VDEN [kg/m$^3$]        | #VDEN                                                            | VDENS                                                                                      | Vapor density                                                                              |
| ZV                     | ZV                                                               | Vapor phase compressibility factor                                                         |                                                                                            |
| ZL                     | Liquid phase compressibility factor                              |                                                                                            |                                                                                            |
| SG                     | Specific gravity of either a pure vapor or a pure liquid phase   |                                                                                            |                                                                                            |
| SGVAP                  | SGVAP                                                            | Specific gravity of vapor fraction                                                         |                                                                                            |
| SGLIQ                  | SGLIQ                                                            | Specific gravity of liquid fraction                                                        |                                                                                            |
| MW  [kg/kmol]          | #MW                                                              | AMW                                                                                        | Molecular weight                                                                           |
| LMW [kg/kmol]          | #LMW                                                             | LAVM                                                                                       | Molecular weight of liquid fraction                                                        |
| VMW  [kg/kmol]         | #VMW                                                             | Molecular weight of vapor fraction                                                         |                                                                                            |
| MY  [kg/m/h]           | #MY                                                              | Viscosity of either a pure vapor or a pure liquid phase                                    |                                                                                            |
| LMY  [kg/m/h]          | #LMY                                                             | Viscosity of liquid fraction                                                               |                                                                                            |
| VMY  [kg/m/h]          | #VMY                                                             | MYV                                                                                        | Viscosity of vapor fraction                                                                |
| KT  [kcal/m/h/Â°C]      | #KT                                                              | Thermal conductivity of either a pure vapor or a pure liquid phase                         |                                                                                            |
| LKT [kcal/m/h/Â°C]      | #LKT                                                             | KTL                                                                                        | Thermal conductivity of liquid fraction                                                    |
| VKT [kcal/m/h/Â°C]      | #VKT                                                             | KTV                                                                                        | Thermal conductivity of vapor fraction                                                     |
| STL [dyn/cm]           | #STL                                                             | STL                                                                                        | Liquid surface tension                                                                     |
| CP [kcal/kmol/Â°C]      | #CP                                                              | Molar heat capacity of mixture                                                             |                                                                                            |
| LCP [kcal/kmol/Â°C]     | #LCP                                                             | CL                                                                                         | Molar heat capacity of liquid fraction                                                     |
| VCP [kcal/kmol/Â°C]     | #VCP                                                             | CV                                                                                         | Molar heat capacity of vapor fraction                                                      |
| MASSCP [kcal/kg/Â°C]    | #MASSCP                                                          | Specific heat capacity of mixture                                                          |                                                                                            |
| LMASSCP [kcal/kg/Â°C]   | #LMASSCP                                                         | CLKG                                                                                       | Specific heat capacity of liquid fraction                                                  |
| VMASSCP [kcal/kg/Â°C]   | #VMASSCP                                                         | CVKG                                                                                       | Specific heat capacity of vapor fraction                                                   |
| CPRATIO                | CPRAT                                                            | Specific heat capacities ratio. (Ratio between Cp and Cv)                                  |                                                                                            |
| VENTH [kcal/kmol]      | #VENTH                                                           | VENTH                                                                                      | Molar enthalpy of vapor phase                                                              |
| LENTH [kcal/kmol]      | #LENTH                                                           | LENTH                                                                                      | Molar enthalpy of liquid phase                                                             |
| ENTV [kcal/kmol/K]     | #ENTV                                                            | ENTV                                                                                       | Molar entropy of vapor phase                                                               |
| ENTL [kcal/kmol/K]     | #ENTL                                                            | ENTL                                                                                       | Molar entropy of liquid phase                                                              |
| HEVAP [kcal/kg]        | #HEVAP                                                           | HEVAP                                                                                      | Heat of evaporation. Only valid for a pure component                                       |
| EXERGY [kcal/kmol]     | #EXERGY                                                          | EXERGY                                                                                     | Molar exergy                                                                               |
| BICARB [%]             | BICARB                                                           | Ion mole percent of bicarbonate ion (TDP20)                                                |                                                                                            |
| CARBAM [%]             | CARBAM                                                           | Ion mole percent of carbamate ion (TDP20)                                                  |                                                                                            |
| ACIDPH                 | PHH                                                              | pH (TDP20)                                                                                 |                                                                                            |
| HHCMOLPCT [%]          | HHCMOLPCT [%]                                                    | Mole percent of higher hydrocarbons                                                        |                                                                                            |


â€ƒ
**Dew and bubble points in TDPROP functions**

| Name using fixed UoM   | Name using  GIPS global UoM as selected in an UDSTA application   | Name in 400230                                                     | Significance             |
|:-----------------------|:------------------------------------------------------------------|:-------------------------------------------------------------------|:-------------------------|
| TDEW  [Â°C]             | #TDEW                                                             | TDEW                                                               | Dew point temperature    |
| TBUB [Â°C]              | #TBUB                                                             | TBUB                                                               | Bubble point temperature |
| PDEWBAR [bar abs]      | #PDEW                                                             | PDEW                                                               | Dew point pressure       |
| PDEWPSIA [psia]        | Dew point pressure                                                |                                                                    |                          |
| PBUBBAR [bar abs]      | #PBUB                                                             | PBUB                                                               | Bubble point pressure    |
| PBUBPSIA [psia]        | Bubble point pressure                                             |                                                                    |                          |
| RVPBAR [bar abs]       | #RVP                                                              | Reid vapor pressure                                                |                          |
| RVPPSIA  [psia]        | Reid vapor pressure                                               |                                                                    |                          |
| TDH2SO4 [Â°C]           | #TDH2SO4                                                          | Dew point using sulfuric ac-id thermodynamics. SO3 must be present |                          |


**Flows and atomic ratios (only fixed UoM) in TDPROP functions**
**No component properties can be calculated**

| Generic and name with fixed UoM   | Significance                                                 |
|:----------------------------------|:-------------------------------------------------------------|
| S/C                               | Steam to total carbon atomic ratio                           |
| SCD/CCD                           | (Steam+CO2)/(Carbon-CO2) atomic ratio                        |
| CFL                               | Carbon flow, (kmol of total atomic C)/h                      |
| OFL                               | Oxygen flow, (kmol of total atomic O)/h                      |
| HFL                               | Hydrogen flow, (kmol of total atomic H)/h                    |
| O/C                               | Oxygen to total carbon atomic ratio                          |
| H/C                               | Hydrogen to total carbon atomic ratio                        |
| S/HYDC                            | Steam to hydrocarbon carbon ratio                            |
| S/HHYDC                           | Steam to higher hydrocarbon carbon ratio                     |
| H2/HYDC                           | Hydrogen to carbon from hydrocarbon ratio Nm3/kg hydrocarbon |
| AROMATIC                          | Flow of aromatic components, kmol/h                          |
| S/DRYGAS                          | Steam to dry gas ratio                                       |
| COMBO2                            | Required oxygen flow to combust a stream, kmol/h             |
| H2/CO                             | Hydrogen to carbon monoxide atomic ratio                     |
| METH/MOD                          | Methanol synthesis module:                                   |
|                                |$ METH/MOD=\frac{H_2-CO_2}{CO+CO_2}   $                         |
| H2/N2                             | Hydrogen to nitrogen atomic ratio                            |
| SOXTOT                            | Flow of SO2, SO3 and H2SO4 calculated as SO2, kg/h.          |
| Also available as #SOXTOT         |                                                              |
| NOXTOT                            | Flow of NO and NO2 calculated as NO2, kg/h                   |
| Also available as #NOXTOT         |                                                              |
| OXPOT                             | The oxidation potential:                                     |
|                                | $OXPOT=\frac{H_2O+CO_2}{H_2+CO+CO_2+H_2O}\cdot100 $            |
| REDPOT                            | The reduction potential:                                     |
|                                | $REDPOT=\frac{H_2+CO}{CO_2+H_2O}$                              |
  

**Equilibrium temperatures in TDPROP functions**
**No component value can be calculated**

| Generic name using fixed UoM   | Name using GIPS global UoM as selected in an UDSTA application   | Significance                                    |
|:-------------------------------|:-----------------------------------------------------------------|:------------------------------------------------|
| TEQBOUD [Â°C]                   | #TEQBOUD                                                         | Boudouard equilibrium temperature (to graphite) |
| TEQMETH [Â°C]                   | #TEQMETH                                                         | Methane decomposition temperature (to graphite) |
| TEQREF [Â°C]                    | #TEQREF                                                          | Reforming equilibrium temperature               |
| TEQSH [Â°C]                     | #TEQSH                                                           | Shift equilibrium temperature                   |
| TEQNH3 [Â°C]                    | #TEQNH3                                                          | Ammonia equilibrium temperature                 |
| TEQMEOH [Â°C]                   | #TEQMEOH                                                         | Methanol equilibrium temperature                |
| TEQSO2 [Â°C]                    | #TEQSO2                                                          | SO2 oxidation equilibrium temperature           |
| TEQCORED [Â°C]                  | CO reduction to carbon equilibrium temp. (to graphite)           |                                                 |


â€ƒ
**Reaction properties (only fixed UoM) in TDPROP functions**
**No component value can be calculated**

| Generic and name with fixed UoM   | Significance                                                                                                                                                                                                                                                     |
|:----------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| H2SKEQ                            | Equilibrium constant for the reaction H2S + ZnO â†” H2O + ZnS                                                                                                                                                                                                      |
| H2SSHFEQ                          | Calculates the concentration in ppb of H2S using the ZnO equilibrium constant after establishment of the shift equilibrium                                                                                                                                       |
| DH2SSHEQ                          | Calculates the concentration in dry ppb of H2S using the ZnO equilibrium constant after establishment of the shift equilibrium                                                                                                                                   |
| H2SEQ                             | Calculates the concentration in ppb of H2S using the ZnO equilibrium constant using the actual amount of water                                                                                                                                                   |
| DH2SEQ                            | Calculates the concentration in dry ppb of H2S using the ZnO equilibrium constant using the actual amount of water                                                                                                                                               |
| QCARBID                           | Calculates the ratio Q between the equilibrium at actual conditions Kp, and the theoretical equilibrium constant Kc for the risk of formation of carbide on a catalyst after establishment of the shift equilibrium. The reaction is: 5Fe3O4+32CO = 3Fe5C2+26CO2 |
| The ratio printed is:             |                                                                                                                                                                                                                                                                  |
| Q = (Kp/Kc)**(1/32)               |                                                                                                                                                                                                                                                                  |

## Steam table TDPROP functions
Properties of steam and water streams are often compared with those in the International steam tables, IAPWS-IF97, but due to the different reference states the values cannot be compared directly. 

A TDPROP function to calculate some of those steam table values can be used for this purpose to obtain the enthalpy of steam and water. The reference state for the enthalpy is the triple point of liquid water, where the enthalpy will be zero, which is also used in the steam tables.

The function is TDPROP(STRNO,HSTMTAB) 

Temperature and pressure are given in the stream STRNO and the stream must only contain water. If the saturation temperature or pressure value is required, specify vapor fraction and pressure or temperature as a ? in STRNO. The default UoM is kcal per kg, but if #HSTMTAB is specified, the UoM in the variable HOTM in #UNIT is used. 

The steam table formulation in IAPWS-IF97 is the relevant one (and the one found on the Internet) and can be specified in most thermodynamic packages. The old method in VDI tables should be considered obsolete. The difference between the two formulations is marginal in most cases. It should, however, be noted that if the UoM is in kJ/kg we use the default conversion between kcal and kJ equal to 4.184, whereas the steam table value is converted using 4.1868. A comparison between the steam table values using IAPWS-IF97 must take this conversion into consideration. 

An example is shown in the GHEMB calculation 862, where the values from both formulations are shown. The stream data group shows all other steam table properties.