
-                     Specification of Feed Streams

(I) NFS               Number of feed streams (maximum 6)
(I) FSN(NFS)          Feed stream numbers
(I) FPN(NFS)          Feed stream stage locations
                      (Bottom-most stage/Reboiler is stage 1)

-                    Specification of Product Streams

(I) NPS               Number of product streams (maximum 6)
(I) PSN(NPS)          Product stream numbers
                      Note that if condenser and/or reboiler sections
                      are specified, the product stream numbers from
                      the condenser stage and/or the reboiler stage
                      are not used by GHEMB and must not be specified.
(I) PPN(NPS)          Product stream stage locations
                      (Bottom-most stage/Reboiler is stage 1)
(I) IFASE(NPS)        Phase of stream (1: Vapor, 2: Liquid)
(I) IUNIT             Flow type
                      0:  Flow rates are molar flow rates
                      1:  Flow rates in % of total column feed
                      One or two rates must be specified as '?'.
                      This depends on the values of ISTOP and ISBOT in
                      480252 or of CONTYP in 480253. For a partial or
                      mixed condenser the following applies:
                      If one as ? : Either ISTOP or ISBOT must be 0
                      If two as ? : Both ISTOP and ISBOT must be 
                                    different from 0
(R) PRATE(NPS)        Molar rate of product stream withdrawals (#Unit)
(R) FRATE(NPS)        Product stream withdrawals as % of total feed (#Unit)

 -                       SEPTOWER Main Data Group

(S) STMAIN            Name of Main data group for SEPTOWER (Typeno 480202)
                      If only one column in the calculation the default
                      names can be use.
                      If more columns names must be given for: 
                      Specification of calculation modes (480252)
                      Names of result data groups and name of output data group
                      Individual names must also be given for the SEPTOWER data
                      groups with pressure drop, initial values, etc. if used
                      The default names of the transfer data groups between 
                      GHEMB and SEPTOWER can be used.
(L) REBTRA            Transfer reboiler data to GHEMB ?
(L) CONTRA            Transfer condenser data to GHEMB ?

-                        Reboiler Specifications
               GHEMB generates stream names for SEPTOWER

(S) REBOIL            Name of reboiler heat exchange operation in GHEMB
                      Note heat loss are taken from the actual GHEMB 
                      operation, whereas pressure drop is from SEPTOWER
(I) SNBOT             Stream number for bottom stream out of column
(I) SNREB             Stream number for reboiler stream back to column
                      It is the stream number specified in the GHEMB
                      operations for the reboiler. Usually the vapor stream
                      from the separator

-                        Condenser Specifications
               GHEMB generates stream names for SEPTOWER

(S) CONDEN            Name of condenser heat exchange operation in GHEMB
                      Note heat loss is taken from the actual GHEMB 
                      operation, whereas pressure drop is from SEPTOWER
(S) RECOND            Name of condenser recycle split operation
                      (Note only two streams are allowed and the first 
                      output stream is the reflux stream)
(I) SNTOP             Stream number for top stream out of column
(I) SNREC             Stream number for recycle stream back to column
                      It is the stream number specified in the GHEMB
                      operations for the condenser

 -                      Pump-around Specifications

(L) PMPTRA            Transfer pump-around data to GHEMB ?
(I) NPUMP             Number of pump-around streams.
                      Must be the same as in 480360.
(S) PMPHEX(NPUMP)     Names of pump-around heat exchanger operations
(S) PMPPMP(NPUMP)     Names of pump-around pump operations
(I) PMPFR(NPUMP)      Stream number for pump-around stream taken
                      from column
(I) PMPTO(NPUMP)      Stream number for pump-around stream led to
                      column
(D) PRATEF(NPS)       Molar rate of product stream withdrawals (#Unit)

-                           Printing of Output

(L) PRINT             Print output?
(S) COND2             Name of second condenser heat exchange operation in GHEMB
                      Note heat loss is taken from the actual GHEMB 
                      operation and can be specified in both CONDEN and COND2.
                      Duty/outlet temperature and pressure drop can be
                      specified either in COND2 or in CONDEN.

-                         Calculated Properties

(R) $DUTYC            Condenser duty (#Unit)
(R) $DUTYR            Reboiler duty (#Unit)
