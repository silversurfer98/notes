**for geometry diags --> [[HX geometry.excalidraw]]
1. TDI --> IN-614-EN
2.  tube sizes for normal exchangers DO/DI in mm
| carbon steel | stainless steel          |
| ------------ | ----------- |
| 12.7/9.4     | 12.7/9.4    |
| 19.05/14.83  | 19.05/15.75 |
| 25.4/21.18   | 25.4/22.1   |

3. in ammonia loop use the
| type           | 150-180 kscg | 180-230 kscg |
| -------------- | ------------ | ------------ |
| gas-gas hx     | 12.7/9.4     | same     |
| water cooler   | 19.05/14.23  | 19.05/13.51  |
| chillers       | 19.05/14.83  | same  |
| chillers cont. | 25.4/20.58   | 25.4/19.86   |
| BFW preheater  | 25.4/17.02   | same             |

4. pitch is always **1.25 times the OD** of the tube
5. nozzle size 
| shell dia->     | DS<=1500 mm        | DS>1500mm             |
| --------------- | ------------------ | --------------------- |
| max nozzle size | 0.5 x DS, max 500 mm | 1/3 x DS, max 1000 mm |

6. baffle spacing practice --> **Shell dia > Baffle spacing > 0.2 x Shell dia**
7. types of baffles --> 
	1. disc and donut (RDDI/RDHO)
	2. double segmental cut (RCUTO/RCUTI)
	3. SINGLE SEGMENTAL --> common

8. SINGLE SEGMENTAL cut = 15 - 45%
9. disc and donut --> RDDI > RDHO, commonly used in **gas-gas hx in amm loop and inside converter
	1. For hot and cold exchangers, based on disc and doughnut baffles, the tube bundle diameters are normally considerably smaller than the shell diameter. This is specified by **fixing RDS at 0.87**
	2. RDDI = 89% and RDHO = 56%
10. double segmental cut --> RCUTO + RCUTI < 50%
11. Overlap in baffles [[overlap in baffles.excalidraw]]
	1. min overlap to provide good support for tubes
	2. formula --> (3 * k * PITCH / DS) * 100%
	3. k depends on pitch
| pitch type | triangular   | rotated triangular | square | rotated square |
|:----------:| ------------ |:------------------:| ------ | -------------- |
|      -->      | $\sqrt{3}$/2 |        0.5         | 1      | $\sqrt{2}$/2   |

12. Partial layout is just breaking the tube sheet symmetry for aligning with nozzle dia [[partial layout.excalidraw]]
13. in case of $\rho V^2$  --> 4000 lb/ft/sec$^2$ for low pressure gases del P will be very high, set tube bundle cut as following
	- TUBECUT = 0.25 x $(\frac{DNIN}{DS}$ x (1+$\frac{0.5DNIN}{DS}$) + x$)$ x 100%
	- x = $\frac{PITCH}{DS}$
	- IF impingement plate present x = -0.25 x $(1-\frac{OD}{PITCH})\frac{DNIN}{DS}$ 
	- if no tubes in window segment tubecur = 50 - 50 x $\sqrt{1-(\frac{DNIN}{DS})^2}$ 
	- IF ntiw TUBECUT = RCUT + $\frac{PITCH}{2*DS} * 100$ 
14. Maximum unsupported tube length --> 36 inches
15. fouling factors --> [[Fouling factors]]
16. thermal conductivity --> a fixed value of  39 kcal/m/hr/°C for carbon steel and low alloy steel (ferritic materials) and 14 kcal/m/hr/°C for TP 304/316 stainless steel (austenitic material) will normally be satisfactory.
| Material        | ASTM Specification | Thermal Conductivity |
| --------------- | ------------------ | -------------------- |
| Carbon steel    | A106 Gr. B         | 38 kcal/mh°C         |
| 1¼Cr ½Mo        | A 335 P11          | 30 kcal/mh°C         |
| 2¼Cr 1Mo        | A 335 P22          | 28 kcal/mh°C         |
| Stainless steel | A 312 TP 304H      | 21 kcal/mh°C         |

> vibration spans diagrams [[Vibration spans.excalidraw]]

17. A figure of 0.04 mm is used as standard
18. tube pitch type
	1. Triangular and rotated triangular pitch provides the most compact tube layout. 
	2. Square pitch is normally used for fouling services where possibilities of mechanical cleaning are requested. 
	3. It should be noted that this also means that a TEMA type with removable tube bundle shall be selected (Type U, T or S), and a cleaning lane of minimum **6.35 mm between the tubes** shall be provided.
	4. can only be a multiple of tube outer dia times [1.25 to 1.67] incremented by 0.0625 mm
	```python
		do=25.4
		multipiler = 1.25
		pitch=do*multipiler
		i=0
		while multipiler<=1.67:
		    print("pitch for ",do," is ",pitch+(i*0.0625), " and multipiler is %4.3f" %(multipiler))
		    multipiler = (pitch+(i*0.0625))/do
		    i=i+1
```

### GIPS OPTIONS

1. option 4
	- in this option program checks the exchanger whether all our spec meet and calculates fouling resistance, even u give those values it wont mind ...
2. option 1 is for proposal
3. option 2 sets tube length and checks whether no. of tubes inside given shell is possible.
4. option 3 --> simulation once design is done
5. option 4 --> always use this method to design and use tube sheet tool to find no.s of tubes

### comments on geometry

1. use this for more insights -->[link](http://dkcphapp030.topsoe.dk/newdoc/dgd/413150_heatex87.html)
	- max shell ID as per TEMA --> 1524 MM
	- front end baffle spacong --> 2 * i/l nozzle ID
	- $rho.V^2$ for shell is 6000 $\frac{kg}{m.s^2}$ or 4000 $\frac{lb}{ft.s^2}$
	-  $rho.V^2$ for tubes is 9000 $\frac{kg}{m.s^2}$ or 6000 $\frac{lb}{ft.s^2}$

> **baffle length only multiple of 10**
> **max shell dia 2500 mm or 100 in**
> U tube max length is 7.5m and 20m tube available only with selected vendors
> No of tie rods --> list (multiple passes – no. of tie-rods to be dividable by the no. of passes)

| Shell ID (mm)    | Tie-rods |
| ---------------- | -------- |
| 0 < ID ≤ 395     | 4        |
| 395 < ID ≤ 852   | 6        |
| 852 < ID ≤ 1232  | 8        |
| 1232 < ID ≤ 1538 | 10       |
| 1538 < ID        | 12       |

> For D and H type no single segmental baffles only and always double segmental
```python
bl = 450.0 # baffle lenght
dia = 1650.0 # hx dia
fbl = 600 # front baffle length
rbl = 600 # rear baffle length
ld_ratio = 0
i=0
len=0

t = fbl + rbl - 2*bl

while ld_ratio<=10 and len<15:
    print("BL = %5.3f  tube length = %5.3f and no of baffles %2d with L/D = %5.3f" %(bl, len, 2*i, ld_ratio))
    len = (bl*2*i+t)/1000
    ld_ratio = len*1000/dia
    i=i+1
```

> for double segmental and disc dougnut types the no of baffles should always be even
