The general concept of building a PBPK model has previously been described by Kuepfer et al. ([Kuepfer 2016](#main-references)). Regarding the relevant anthropometric (height, weight) and physiological parameters (e.g. blood flows, organ volumes, binding protein concentrations, hematocrit, cardiac output) in adults was gathered from the literature and has been previously published ([PK-Sim Ontogeny Database Version 7.3](#main-references)). The information was incorporated into PK-Sim® and was used as default values for the simulations in adults.

The  applied activity and variability of plasma proteins and active processes that are integrated into PK-Sim® are described in the publicly available PK-Sim® Ontogeny Database Version 7.3 ([Schlender 2016](#main-references)) or otherwise referenced for the specific process.

First, a base PBPK model was built using clinical data including selected single and multiple 400 mg dose studies with intravenous and oral applications (tablet) of moxifloxacin to find an appropriate structure to describe the pharmacokinetics in plasma ([Sullivan 1999, Stass and Kubitza 1999, U.S. Food and Drug Administration 2016](#main-references)). The PBPK models were built based on data from healthy individuals, using the reported sex, ethnicity and mean values for age, weight and height from each study protocol. If no demographic information was reported in the respective clinical study, a default mean individual was used with the following properties: male, European, 30 years of age, 73 kg body weight and 176 cm body height. The relative tissue-specific expressions of the enzymes involved in the glucuronide (UGT1A1) and sulfate (SULT2A1) conjugation of moxifloxacin were considered. 

The clearance parameters were identified using the Parameter Identification module provided in PK-Sim®. A Weibull function was used to describe the oral dissolution of moxifloxacin. Structural model selection was mainly guided by visual inspection of the resulting description of data and biological plausibility.

The model was then verified by simulating:

- Intravenous and oral administration of 400 mg ([U.S. Food and Drug Administration 2000](#main-references))
- Intravenous and oral administration of 100 mg ([Siefert 1999](#main-references))
- Single oral administration of doses ranging between 60 and 600 mg ([U.S. Food and Drug Administration 2000](#main-references))

Details about input data (physicochemical, *in vitro* and clinical) can be found in [Section 2.2](#methods-data).

Details about the structural model and its parameters can be found in [Section 2.3](#model-parameters-and-assumptions).

