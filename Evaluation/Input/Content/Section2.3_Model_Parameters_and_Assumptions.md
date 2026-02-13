### Absorption <a id="model-parameters-and-assumptions-absorption"></a>

The parameter value for  `Specific intestinal permeability` was based on the passive permeability measured in Caco-2 cell line, see [Section 2.3.4](#model-parameters-and-assumptions-parameter-identification) ([Litjens 2022](#main-references)). The aqueous solubility in water was used in the model (see [Section 2.2.1](#invitro-and-physico-chemical-data)) ([U.S. Pharmacist 2023](#main-references)). The dissolution of tablets was implemented via empirical Weibull dissolution. 

### Distribution <a id="model-parameters-and-assumptions-distribution"></a>

Moxifloxacin is 40-50 % bound to albumin (see [Section 2.2.1](#invitro-and-physico-chemical-data)) [Willmann 2019](#main-references). A value of fu = 55 % was used in this PBPK model for `Fraction unbound (plasma, reference value)`.

An important parameter influencing the resulting volume of distribution is lipophilicity. The reported lipophilicity ranged from 0.6 to 1.80, and a value of 1.80 (logMA) was used in this model (see [Section 2.2.1](#invitro-and-physico-chemical-data)) ([Willmann 2019](#main-references)). 

After testing the available organ-plasma partition coefficient and cell permeability calculation methods built in PK-Sim, observed clinical data was best described by choosing the partition coefficient calculation by `Rodgers and Rowland` and cellular permeability calculation by `PK-Sim Standard`. 

### Metabolism and Elimination <a id="model-parameters-and-assumptions-metabolism-and-elimination"></a>

The major enzymes involved in the sulfate conjugation (SULT2A1) and glucuronidation (UGT1A1) were included in the PBPK model. The expression profile of SULT2A1 was based on EST. The expression profile of UGT1A1 was based on RT-PCR. Michaelis-Menten kinetics for SULT2A1 were reported in literature, but protein content was not reported. Therefore, SULT2A1 was implemented as a `Intrinsic clearance - First order` process and fitted via Parameter Identification. UGT1A1 was implemented as `In vitro metabolic rate in the presence of recombinant CYPs/enzymes - First order` parametrized based on the reported intrinsic clearance of 0.058 µL/min/pmol enzyme, derived via retrograde calculation ([Litjens 2022](#main-references)). SULT2A1 `specific clearance` and UGT1A1 `CLspec/[Enzyme]` were fitted to observed fractions metabolized (38 % sulfate conjugation and 14 % glucuronidation) via Parameter Identification.

Renal clearance contributes to about 20% of the metabolism and elimination of moxifloxacin. The renal clearance was derived from the reported in vivo clearance (2.61 L/h for a 85 kg subject) ([Stass and Kabitza 1999](#main-references)). Biliary clearance was derived from the in vivo clearance, assuming it contributed 25 % of the total clearance (11.6 L/h for a 85 kg subject). Enterohepatic recirculation was implemented assuming EHC continuous fraction equal to 1.

### Automated Parameter Identification <a id="model-parameters-and-assumptions-parameter-identification"></a>

The following parameters have been estimated in the model:

| Model Parameter      | 
| -------------------- | 
| `specific clearance` (SULT2A1) | 
| `CLspec/[Enzyme]` (UGT1A1) |

