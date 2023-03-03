Parameters we worry abt : 



| 1  | Calctype        | 4      | Number                 | 1/1 (Dimless) | sizing =1, simulating fouling=4                             |
| -- | --------------- | ------ | ---------------------- | ------------- | ----------------------------------------------------------- |
| 2  | Vesselposition  | 1      | Number                 | 1/1 (Dimless) | Vertical =1 ,  Horizontal =2                                |
| 3  | TubeIDdrilled   | 28.96  | Length                 | mm            | Boiler tube ID bayonet part (if drilled)                    |
| 4  | TubeID          | 28.96  | Length                 | mm            | Boiler tube ID U-Tube part                                  |
| 5  | TubePitch       | 49     | Length                 | mm            | Tube pitch                                                  |
| 6  | TubeOD          | 38.1   | Length                 | mm            | Boiler tube OD                                              |
| 7  | IBID            | 21     | Length                 | mm            | Inner Bayonet ID                                            |
| 8  | IBDO            | 23     | Length                 | mm            | INNER Bayonet OD                                            |
| 9  | OBDI            | 25     | Length                 | mm            | OUTER Bayonet ID                                            |
| 10 | OBOD            | 27     | Length                 | mm            | OUTER Bayonet OD                                            |
| 11 | TubeNumber      | 315    | Number                 | 1/1 (Dimless) | Number of U-tubes                                           |
| 12 | Tube_L          | 6.3    | Length                 | m             | U-tube length including bayonet                             |
| 13 | BayonetLength   | 0.6    | Length                 | m             | Effictive length of bayonet tubes                           |
| 14 | Psteam          | 11.5   | Pressure               | MPa g         | Steam pressure                                              |
| 15 | TBFW            | 255    | Temperature            | °C            | Temperature of BFW (for vertical only)                      |
| 16 | DP              | 0.4    | DeltaPressure          | kg/cm²        | Adjust no tubes to achieve pressure drop tube side          |
| 17 | FoulingShell    | 0.0001 | HeatTransferResistance | m²·h·K/kcal   | Fouling factor shell side                                   |
| 18 | FoulingTube     | 0.0002 | HeatTransferResistance | m²·h·K/kcal   | Fouling factor tube side                                    |
| 19 | TSthickness     | 200    | Length                 | mm            | Tubesheet thickness                                         |
| 20 | Dummylength     | 200    | Length                 | mm            | Length of bayonet from dummy tubesheet to tubesheet         |
| 21 | FractionAnnulus | 10.1   | Fraction               | %             | Fraction of feed in annulus                                 |
| 22 | ThermalConbayo  | 0.4    | ThermalConductivity    | kcal/m/h/K    | Conductivity of double bayonet tube                         |
| 23 | ThermalConTube  | 31     | ThermalConductivity    | kcal/m/h/K    | Conductivity of boiler tube                                 |
| 24 | RoughnessPipe   | 0.04   | Length                 | mm            | Roughness of pipes (annulus part)                           |
| 25 | Tmix            | 1      | DeltaTemperature       | °C            | T outlet U-Tube DTbelow mix temperature                    |
| 26 |                 | ?      |                        |               | Calculated values                                           |
| 27 | WHBID           | ?      | Length                 | mm            | WHB ID, ?=calculate                                         |
| 28 | ShroudID        | 1460   | Length                 | mm            | Shroud ID, ?=calculate                                      |
| 29 | SteamDrumID     | ?      | Length                 | mm            | Steam drum ID, ?=calculate                                  |
| 30 |                 | ?      |                        |               | Additional input                                            |
| 31 | SteamDrumHead   | 1      | Nounit                 |               | Steam drum head type, 1=spherical, 2=ellipsoidal            |
| 32 | HeatLossPFD     | 1      | Percent                | %             | Heat loss specified in PFD                                  |
| 33 | BlowDownPFD     | 1      | Percent                | %             | Blow down specified in PFD                                  |
| 34 | InlcudeDrawing  | 1      | Nounit                 |               | Inlcude svg file drawing of U-tube, 0=no drawing, 1=include |


