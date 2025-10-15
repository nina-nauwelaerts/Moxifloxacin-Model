# Building and evaluation of a PBPK model for COMPOUND in healthy adults

| Version                                         | x.x-OSPy.y                                                   |
| ----------------------------------------------- | ------------------------------------------------------------ |
| based on *Model Snapshot* and *Evaluation Plan* | https://github.com/Open-Systems-Pharmacology/COMPOUND-Model/releases/tag/vx.x |
| OSP Version                                     | y.y                                                          |
| Qualification Framework Version                 | z.z                                                          |

This evaluation report and the corresponding PK-Sim project file are filed at:

https://github.com/Open-Systems-Pharmacology/OSP-PBPK-Model-Library/

# Table of Contents

 * [1 Introduction](#introduction)
 * [2 Methods](#methods)
   * [2.1 Modeling Strategy](#modeling-strategy)
   * [2.2 Data](#methods-data)
     * [2.2.1 In vitro / physico-chemical Data ](#invitro-and-physico-chemical-data)
     * [2.2.2 Clinical Data  ](#clinical-data)
       * [2.2.2.1 Model Building ](#model-building)
       * [2.2.2.2 Model Verification ](#model-verification)
   * [2.3 Model Parameters and Assumptions](#model-parameters-and-assumptions)
     * [2.3.1 Absorption ](#model-parameters-and-assumptions-absorption)
     * [2.3.2 Distribution ](#model-parameters-and-assumptions-distribution)
     * [2.3.3 Metabolism and Elimination ](#model-parameters-and-assumptions-metabolism-and-elimination)
     * [2.3.4 Automated Parameter Identification ](#model-parameters-and-assumptions-parameter-identification)
 * [3 Results and Discussion](#results-and-discussion)
   * [3.1 Final input parameters](#final-input-parameters)
   * [3.2 Diagnostics Plots](#diagnostics-plots)
   * [3.3 Concentration-Time Profiles](#ct-profiles)
 * [4 Conclusion](#conclusion)
 * [5 References](#main-references)

# 1 Introduction<a id="introduction"></a>

Moxifloxacin is an a broad-spectrum fluoroquinolone antibiotic, used to treat a variety of bacterial infactions ([U.S. Food and Drug Administration 2016](#main-references)). Moxifloxacin is administered typically with a 400 mg once daily regimen.

Moxifloxacin is absorbed well from the gastrointestinal tract, with almost complete bioavailability (90 %) ([U.S. Food and Drug Administration 2016](##main-references)). Plasma concentrations show dose-linear PK ([U.S. Food and Drug Administration 2016](#main-references)). The elimination half-life is 12h. Plasma protein binding is approximately 30-50 % ([U.S. Food and Drug Administration 2016](#main-references)). Moxifloxacin has a distribution volume ranging between 1.7-2.7 L/kg ([U.S. Food and Drug Administration 2016](#main-references)). About half of the dose is metabolized to inactive metabolites via glucuronide and sulfate conjugation, whereas about 20 % is found unchanged in urine and 25 % in feces ([U.S. Food and Drug Administration 2016](#main-references)). The sulfate conjugate (M1) accounts for approximately 38 % of the dose, and is eliminated primarily in the feces ([U.S. Food and Drug Administration 2016](#main-references)). The glucuronide conjugate (M2) accounts for approximately 14 % of the dose, and is eliminated in the urine ([U.S. Food and Drug Administration 2016](#main-references)). 

The herein presented model building and evaluation report evaluates the performance of the PBPK model for Moxifloxacin in (healthy) adults. The model was developed using data of 3 clinical studies with intravenous and oral administration of 400 mg QD ([Sullivan 1999, Stass and Kabitza 1999, U.S. Food and Drug Administration 2016](#main-references)). The model was evaluated using data of 3 clinical studies with intravenous and oral administration of doses ranging between 60 and 600 mg ([Siefert 1999, U.S. Food and Drug Administration 2000 U.S](#main-references)). The PK-Sim project file contains simulations and the observed data of all clinical studies used for model development and evaluation. 

The presented Moxifloxacin PBPK model as well as the respective evaluation plan and evaluation report are provided open-source ([https://github.com/Open-Systems-Pharmacology/Moxifloxacin-Model](https://github.com/Open-Systems-Pharmacology/Moxifloxacin-Model)).

# 2 Methods<a id="methods"></a>

## 2.1 Modeling Strategy<a id="modeling-strategy"></a>

The general concept of building a PBPK model has previously been described by Kuepfer et al. ([Kuepfer 2016](#main-references)) Regarding the relevant anthropometric (height, weight) and physiological parameters (e.g. blood flows, organ volumes, binding protein concentrations, hematocrit, cardiac output) in adults was gathered from the literature and has been previously published ([PK-Sim Ontogeny Database Version 7.3](#main-references)). The information was incorporated into PK-Sim® and was used as default values for the simulations in adults.

The  applied activity and variability of plasma proteins and active processes that are integrated into PK-Sim® are described in the publicly available PK-Sim® Ontogeny Database Version 7.3 ([Schlender 2016](#main-references)) or otherwise referenced for the specific process.

First, a base PBPK model was built using clinical data including selected single and multiple 400 mg dose studies with intravenous and oral applications (tablet) of moxifloxacin to find an appropriate structure to describe the pharmacokinetics in plasma ([Sullivan 1999, Stass and Kabitza 1999, U.S. Food and Drug Administration 2016](#5-references)). The PBPK models were built based on data from healthy individuals, using the reported sex, ethnicity and mean values for age, weight and height from each study protocol. If no demographic information was reported in the respective clinical study, a default mean individual was used with the following properties: male, European, 30 years of age, 73 kg body weight and 176 cm body height. The relative tissue-specific expressions of the enzymes involved in the glucuronide (UGT1A1) and sulfate (SULT2A1) conjugation of moxifloxacin were considered. 

The clearance parameters were identified usin the Parameter Identification module provided in PK-Sim®. A Weibull function was used to describe the oral dissolution of moxifloxacin. Structural model selection was mainly guided by visual inspection of the resulting description of data and biological plausibility.

The model was then verified by simulating:

- Intravenous and oral administration of 400 mg ([U.S. Food and Drug Administration 2000 U.S](#5-references))
- Intravenous and oral administration of 100 mg ([Siefert 1999](#5-references))
- Single oral administration of doses ranging between 60 and 600 mg ([U.S. Food and Drug Administration 2000 U.S](#5-references))

Details about input data (physicochemical, *in vitro* and clinical) can be found in [Section 2.2](#methods-data).

Details about the structural model and its parameters can be found in [Section 2.3](#model-parameters-and-assumptions).

## 2.2 Data<a id="methods-data"></a>

### 2.2.1 In vitro / physico-chemical Data <a id="invitro-and-physico-chemical-data"></a>

A literature search was performed to collect available information on physicochemical properties of moxifloxacin. The obtained information from literature is summarized in the table below. 

| **Parameter**   | **Unit** | **Value** | Source                                     | **Description**                                 |
| :-------------- | -------- | --------- | ------------------------------------------ | ----------------------------------------------- |
| MW              | g/mol    |  401.4         | [Willmann 2019](#main-references)               | Molecular weight                                |
| pK<sub>a</sub> (acid) |          | 6.25          | [Langlois 2005](#main-references)         | Acid dissociation constant                      |
| pK<sub>a</sub> (base) |          | 9.29          | [Langlois 2005](#main-references)         | Acid dissociation constant                      |
| Solubility (pH) | mg/mL         | 2.9          | [U.S. Pharmacist 2023](#main-references)               | Aqueous Solubility                 |
| Solubility (pH) | mg/mL         | sparingly soluble in water         | [Willmann 2019](#main-references)               | Aqueous Solubility                |
| logMA            |          | 1.8          | [Willmann 2019](#main-references) | Membrane affinity |
| logP            |          | 0.6          | [Willmann 2019](#main-references) | Partition coefficient between octanol and water |
| logP            |          | 1.04          | [Edginton 2009](#main-references) | Partition coefficient between octanol and water |
| logP            |          | 0.832          | [Litjens 2022](#main-references) | Partition coefficient between octanol and water |
| fu              | %        | 50          | [Edginton 2009](#main-references)                | Fraction unbound in plasma                      |
| fu              |         | 0.606          | [Litjens 2022](#main-references)                | Fraction unbound in plasma                      |
| fu              | %        | 50-60         | [Willmann 2019](#main-references)                | Fraction unbound in plasma                      |
| B/P ratio       |          | 1.10          | [Litjens 2022](#main-references)                | Blood to plasma ratio                           |
| Passive permeability     | 10E-6 cm/s         | 11.5          | [Litjens 2022](#main-references)                | Passive permeability (Caco-2)                           |

### 2.2.2 Clinical Data  <a id="clinical-data"></a>

A literature search was performed to collect available clinical data on moxifloxacin in healthy adults.

#### 2.2.2.1 Model Building <a id="model-building"></a>

The following studies were used for model building (training data):

| Publication                 | Arm / Treatment / Information used for model building |
| :-------------------------- | :---------------------------------------------------- |
| [Stass and Kabitza 1999](#main-references) | Healthy Subjects with a single IV dose of 400 mg           |
| [Stass and Kabitza 1999](#main-references) | Healthy Subjects with a single PO dose of 400 mg           |
| [U.S. Food and Drug Administration 2016](#main-references)                         | Healthy Subjects with IV doses of  400 mg QD                                                  |
| [U.S. Food and Drug Administration 2016](#main-references)                         | Healthy Subjects with PO doses of  400 mg QD                                                  |
| [Sullivan 1999](#main-references)                         | Healthy Subjects with PO doses of  400 mg QD                                                   |

#### 2.2.2.2 Model Verification <a id="model-verification"></a>

The following studies were used for model verification:

| Publication                 | Arm / Treatment / Information used for model building |
| :-------------------------- | :---------------------------------------------------- |
| [Siefert 1999](#main-references) | Healthy Subjects with a single IV dose of 100 mg          |
| [Siefert 1999](#main-references) | Healthy Subjects with a single PO dose of 100 mg          |
| [U.S. Food and Drug Administration 2000](#main-references) | Healthy Subjects with a single IV dose of 400 mg (Study PH 27517/0139)         |
| [U.S. Food and Drug Administration 2000](#main-references) | Healthy Subjects with a single PO dose of 400 mg (Study PH 27517/0139)         |
| [U.S. Food and Drug Administration 2000](#main-references) | Healthy Subjects with a single PO dose of 60 mg (Study PH 26024/0101)        |
| [U.S. Food and Drug Administration 2000](#main-references) | Healthy Subjects with a single PO dose of 60 mg (Study PH 26024/0101)         |
| [U.S. Food and Drug Administration 2000](#main-references) | Healthy Subjects with a single PO dose of 100 mg (Study PH 26024/0101)         |
| [U.S. Food and Drug Administration 2000](#main-references) | Healthy Subjects with a single PO dose of 200 mg (Study PH 26024/0101)         |
| [U.S. Food and Drug Administration 2000](#main-references) | Healthy Subjects with a single PO dose of 400 mg (Study PH 26024/0101)         |
| [U.S. Food and Drug Administration 2000](#main-references) | Healthy Subjects with a single PO dose of 600 mg (Study PH 26024/0101)          |

## 2.3 Model Parameters and Assumptions<a id="model-parameters-and-assumptions"></a>

### 2.3.1 Absorption <a id="model-parameters-and-assumptions-absorption"></a>

The parameter value for  `Specific intestinal permeability` was based on the passive permeability measured in Caco-2 cell line, see [Section 2.3.4](#model-parameters-and-assumptions-identification) ([Litjens 2022](#main-references)). The aqueous solubility in water was used in the model (see [Section 2.2.1](#invitro-and-physico-chemical-data)) ([U.S. Pharmacist 2023](#main-references)). The dissolution of tablets was implemented via empirical Weibull dissolution. 

### 2.3.2 Distribution <a id="model-parameters-and-assumptions-distribution"></a>

Moxifloxacin is 40-50 % bound to albumin (see [Section 2.2.1](#invitro-and-physico-chemical-data)) [Willmann 2019](#main-references). A value of fu = 55 % was used in this PBPK model for `Fraction unbound (plasma, reference value)`.

An important parameter influencing the resulting volume of distribution is lipophilicity. The reported lipophilicity ranged from 0.6 to 1.80, and a value of 1.80 (logMA) was used in this model (see [Section 2.2.1](#invitro-and-physico-chemical-data)) ([Willmann 2019](#main-references)). 

After testing the available organ-plasma partition coefficient and cell permeability calculation methods built in PK-Sim, observed clinical data was best described by choosing the partition coefficient calculation by `Rodgers and Rowland` and cellular permeability calculation by `PK-Sim Standard`. 

### 2.3.3 Metabolism and Elimination <a id="model-parameters-and-assumptions-metabolism-and-elimination"></a>

The major enzymes involved in the sulfate conjugation (SULT2A1) and glucuronidation (UGT1A1) were included in the PBPK model. The expression profile of SULT2A1 was based on EST. The expression profile of UGT1A1 was based on RT-PCR. Michaelis-Menten kinetics for SULT2A1 were reported in literature, but protein content was not reported. Therefore, SUL2A1 was implemented as a `Intrinsic clearance - First order` process and fitted via Parameter Identification. UGT1A1 was implemented as `In vitro metabolic rate in the presence of recombinant CYPs/enzymes - First order` parametrized based on the reported intrinsic clearance of 0.058 µL/min/pmol enzyme, derived via retrograde calculation ([Litjens 2022](#main-references)). SULT2A1 `specific clearance` and UGT1A1 `CLspec/[Enzyme]` were fitted to observed fractions metabolized (38 % sulfate conjugation and 14 % glucuronidation) via Parameter Identification.

Renal clearance clearance contributes to about 20 % of the metabolism and elimination of moxifloxacin. The renal clearance was derived from the reported in vivo clearance (2.61 L/h for a 85 kg subject) ([Stass and Kabitza 1999](#main-references)). Biliary clearance was derived from the in vivo clearance, assuming it contributed 25 % of the total clearance (11.6 L/h for a 85 kg subject). Enterohepatic recirculation was implemented assuming EHC contibuous fraction equal to 1.

### 2.3.4 Automated Parameter Identification <a id="model-parameters-and-assumptions-parameter-identification"></a>

The following parameters have been estimated in the model:

| Model Parameter      | 
| -------------------- | 
| `specific clearance` (SULT2A1) | 
| `CLspec/[Enzyme]` (UGT1A1) |

# 3 Results and Discussion<a id="results-and-discussion"></a>

The PBPK model for moxifloxacin was developed and verified with clinical pharmacokinetic data.

The model was evaluated covering data from studies including in particular

* Intravenous and oral administration of 400 mg ([U.S. Food and Drug Administration 2000 U.S](#5-references))
* Intravenous and oral administration of 100 mg ([Siefert 1999](#5-references))
* Single oral administration of doses ranging between 60 and 600 mg ([U.S. Food and Drug Administration 2000 U.S](#5-references))

The model quantifies moxifloxacin metabolism via glucuronidation and sulfate conjugation, and elimination via renal and biliary clearance. The PBPK model shows good predictive performance after intravenous administration, and reasonable predictions for oral administration. The PBPK model shows some discrepancy in prediction of tmax compared to the  clinical data. This could be explained by the assumptions implemented for regarding the formulation and biliary clearance processes. Nevertheless a tmax closer to the model predictions (about 1-2h) is  reported in literature, suggesting that the discrepancy could be related to data extraction and/or secondary peaks ([Stass and Kabitza 1999, Siefert 1999, U.S. Food and Drug Administration 2000](#main-references)). Furthermore, the PBPK model shows sensitivity to the gastronintestinal transit time, which could also explain the variability observed in clinical data. Gastrointestinal transit time has been shown to affect oral pharmacokinetics for several medicines ([Grimm 2018](#main-references)) Sullivan et al., 1999 contributed observed differences in accumulation ratio between studies to random variation associate with small sample sizes ([Sullivan 1999](#main-references)). Further model refinements could integrate *in vitro* data for the metabolism pathways, formulation characteristics and mechnistics behind interindividual variability. Nevertheless, this PBPK model can be applied to predict pharmacokinetics of moxifloxacin after intravenous and oral administration.

The next sections show:

1. the final model parameters for the building blocks: [Section 3.1](#final-input-parameters).
2. the overall goodness of fit: [Section 3.2](#diagnostics-plots).
3. simulated vs. observed concentration-time profiles for the clinical studies used for model building and for model verification: [Section 3.3](#ct-profiles).

## 3.1 Final input parameters<a id="final-input-parameters"></a>

The compound parameter values of the final PBPK model are illustrated below.

### Compound: Moxifloxacin

#### Parameters

Name                                             | Value         | Value Origin                                                                                 | Alternative  | Default
------------------------------------------------ | ------------- | -------------------------------------------------------------------------------------------- | ------------ | -------
Solubility at reference pH                       | 2.9 mg/ml     | Internet-In Vitro-https://www.uspharmacist.com/article/moxifloxacin-20-mg-ml-oral-suspension | Measurement  | True   
Reference pH                                     | 7             | Internet-In Vitro-https://www.uspharmacist.com/article/moxifloxacin-20-mg-ml-oral-suspension | Measurement  | True   
Lipophilicity                                    | 1.8 Log Units | Publication-Other-Willmann 2019                                                              | Measurement  | True   
Fraction unbound (plasma, reference value)       | 0.55          | Publication-In Vitro-Willmann 2019                                                           | Measurement  | True   
Specific intestinal permeability (transcellular) | 1.15E-05 cm/s | Publication-In Vitro-Litjens 2022                                                            | Litjens 2022 | True   
F                                                | 1             |                                                                                              |              |        
Is small molecule                                | Yes           |                                                                                              |              |        
Molecular weight                                 | 401.4 g/mol   |                                                                                              |              |        
Plasma protein binding partner                   | Albumin       |                                                                                              |              |        

#### Calculation methods

Name                    | Value              
----------------------- | -------------------
Partition coefficients  | Rodgers and Rowland
Cellular permeabilities | PK-Sim Standard    

#### Processes

##### Metabolizing Enzyme: SULT2A1-Fit

Species: Human

Molecule: SULT2A1

###### Parameters

Name                | Value              | Value Origin                                                                                 
------------------- | ------------------ | ---------------------------------------------------------------------------------------------
Intrinsic clearance | 0.1 l/min          |                                                                                              
Specific clearance  | 0.0187322414 1/min | Parameter Identification-Parameter Identification-Value updated from 'IV' on 2025-08-21 17:37

##### Metabolizing Enzyme: UGT1A1-Litjens 2022

Molecule: UGT1A1

###### Parameters

Name                           | Value                         | Value Origin                                                                                 
------------------------------ | ----------------------------- | ---------------------------------------------------------------------------------------------
In vitro CL/recombinant enzyme | 0.058 µl/min/pmol rec. enzyme |                                                                                              
CLspec/[Enzyme]                | 0.0212088311 l/µmol/min       | Parameter Identification-Parameter Identification-Value updated from 'IV' on 2025-08-21 17:37

##### Systemic Process: Renal Clearances-Stass and Kabitza 1999

Species: Human

###### Parameters

Name                          | Value        | Value Origin
----------------------------- | ------------ | ------------:
Fraction unbound (experiment) | 0.55         |             
Plasma clearance              | 0.031 l/h/kg |             

##### Systemic Process: Biliary Clearance-Stass and Kabitza 1999

Species: Human

###### Parameters

Name                          | Value         | Value Origin
----------------------------- | ------------- | ------------:
Fraction unbound (experiment) | 0.55          |             
Lipophilicity (experiment)    | 1.8 Log Units |             
Plasma clearance              | 0.034 l/h/kg  |             

### Formulation: Tablet

Type: Weibull

#### Parameters

Name                             | Value | Value Origin    
-------------------------------- | ----- | ----------------
Dissolution time (50% dissolved) | 1 h   | Other-Assumption
Lag time                         | 0 h   |                 
Dissolution shape                | 0.92  |                 
Use as suspension                | Yes   |                 

## 3.2 Diagnostics Plots<a id="diagnostics-plots"></a>

Below you find the goodness-of-fit visual diagnostic plots for the PBPK model performance of all data used presented in [Section 2.2.2](#clinical-data).

The first plot shows observed versus simulated plasma concentration, the second weighted residuals versus time. 

<a id="table-3-1"></a>

**Table 3-1: GMFE for Goodness of fit plot for concentration in plasma**

|Group             |GMFE |
|:-----------------|:----|
|Model development |1.29 |
|Model evaluation  |1.67 |
|All               |1.50 |

<br>
<br>

<a id="figure-3-1"></a>

![](images/006_section_results-and-discussion/008_section_diagnostics-plots/2_gof_plot_predictedVsObserved.png)

**Figure 3-1: Goodness of fit plot for concentration in plasma**

<br>
<br>

<a id="figure-3-2"></a>

![](images/006_section_results-and-discussion/008_section_diagnostics-plots/3_gof_plot_residualsOverTime.png)

**Figure 3-2: Goodness of fit plot for concentration in plasma**

<br>
<br>

## 3.3 Concentration-Time Profiles<a id="ct-profiles"></a>

Simulated versus observed concentration-time profiles of all data listed in [Section 2.2.2](#clinical-data) are presented below.

<a id="figure-3-3"></a>

![](images/006_section_results-and-discussion/009_section_ct-profiles/1_time_profile_plot_Moxifloxacin_Bayer_Avelox_3963471_IV_400_mg_qd.png)

**Figure 3-3: Bayer Avelox 3963471_IV_400 mg qd**

<br>
<br>

<a id="figure-3-4"></a>

![](images/006_section_results-and-discussion/009_section_ct-profiles/2_time_profile_plot_Moxifloxacin_Bayer_Avelox_3963471_PO_400_mg_qd.png)

**Figure 3-4: Bayer Avelox 3963471_PO_400 mg qd**

<br>
<br>

<a id="figure-3-5"></a>

![](images/006_section_results-and-discussion/009_section_ct-profiles/3_time_profile_plot_Moxifloxacin_Stass_1999_IV_400_mg.png)

**Figure 3-5: Stass 1999_IV_400 mg**

<br>
<br>

<a id="figure-3-6"></a>

![](images/006_section_results-and-discussion/009_section_ct-profiles/4_time_profile_plot_Moxifloxacin_Stass_1999_PO_400_mg.png)

**Figure 3-6: Stass 1999_PO_400 mg**

<br>
<br>

<a id="figure-3-7"></a>

![](images/006_section_results-and-discussion/009_section_ct-profiles/5_time_profile_plot_Moxifloxacin_Sullivan_1999_PO_400_mg_qd.png)

**Figure 3-7: Sullivan 1999_PO_400 mg qd**

<br>
<br>

<a id="figure-3-8"></a>

![](images/006_section_results-and-discussion/009_section_ct-profiles/6_time_profile_plot_Moxifloxacin_PH_26024_0101_PO_100_mg.png)

**Figure 3-8: PH 26024/0101_PO_100 mg**

<br>
<br>

<a id="figure-3-9"></a>

![](images/006_section_results-and-discussion/009_section_ct-profiles/7_time_profile_plot_Moxifloxacin_PH_26024_0101_PO_200_mg.png)

**Figure 3-9: PH 26024/0101_PO_200 mg**

<br>
<br>

<a id="figure-3-10"></a>

![](images/006_section_results-and-discussion/009_section_ct-profiles/8_time_profile_plot_Moxifloxacin_PH_26024_0101_PO_400_mg.png)

**Figure 3-10: PH 26024/0101_PO_400 mg**

<br>
<br>

<a id="figure-3-11"></a>

![](images/006_section_results-and-discussion/009_section_ct-profiles/9_time_profile_plot_Moxifloxacin_PH_26024_0101_PO_60_mg.png)

**Figure 3-11: PH 26024/0101_PO_60 mg**

<br>
<br>

<a id="figure-3-12"></a>

![](images/006_section_results-and-discussion/009_section_ct-profiles/10_time_profile_plot_Moxifloxacin_PH_26024_0101_PO_600_mg.png)

**Figure 3-12: PH 26024/0101_PO_600 mg**

<br>
<br>

<a id="figure-3-13"></a>

![](images/006_section_results-and-discussion/009_section_ct-profiles/11_time_profile_plot_Moxifloxacin_PH_27517_0139_IV_400_mg.png)

**Figure 3-13: PH 27517/0139_IV_400 mg**

<br>
<br>

<a id="figure-3-14"></a>

![](images/006_section_results-and-discussion/009_section_ct-profiles/12_time_profile_plot_Moxifloxacin_PH_27517_0139_PO_400_mg.png)

**Figure 3-14: PH 27517/0139_PO_400 mg**

<br>
<br>

<a id="figure-3-15"></a>

![](images/006_section_results-and-discussion/009_section_ct-profiles/13_time_profile_plot_Moxifloxacin_Siefert_1999_IV_100_mg.png)

**Figure 3-15: Siefert 1999_IV_100 mg**

<br>
<br>

<a id="figure-3-16"></a>

![](images/006_section_results-and-discussion/009_section_ct-profiles/14_time_profile_plot_Moxifloxacin_Siefert_1999_PO_100_mg.png)

**Figure 3-16: Siefert 1999_PO_100 mg**

<br>
<br>

# 4 Conclusion<a id="conclusion"></a>

The herein presented PBPK model adequately describes the pharmacokinetics of moxifloxacin in adults.

In particular, it applies quantitative metabolism via glucuronidation and sulfate conjugation, and elimination via renal and biliary clearance. Thus, the model is fit for purpose to be applied for simulation of intravenous and oral administration of moxifloxacin in adults.

# 5 References<a id="main-references"></a>

**Edginton 2009** Edginton AN, Ahr G, Willmann S, Stass H. Defining the role of macrophages in local moxifloxacin tissue concentrations using biopsy data and whole-body physiologically based pharmacokinetic modelling. Clin Pharmacokinet. 2009;48(3):181-7. doi: 10.2165/00003088-200948030-00004.

**Grimm 2018** Grimm M, Koziolek M, Kühn JP, Weitschies W. Interindividual and intraindividual variability of fasted state gastric fluid volume and gastric emptying of water. Eur J Pharm Biopharm. 2018 Jun;127:309-317. doi: 10.1016/j.ejpb.2018.03.002. Epub 2018 Mar 6. PMID: 29522898.

**Kuepfer 2016** Kuepfer L, Niederalt C, Wendl T, Schlender JF, Willmann S, Lippert J, Block M, Eissing T, Teutonico D. Applied Concepts in PBPK Modeling: How to Build a PBPK/PD Model.CPT Pharmacometrics Syst Pharmacol. 2016 Oct;5(10):516-531. doi: 10.1002/psp4.12134. Epub 2016 Oct 19. 	

**Langlois 2005** Langlois MH, Montagut M, Dubost JP, Grellet J, Saux MC. Protonation equilibrium and lipophilicity of moxifloxacin. J Pharm Biomed Anal. 2005 Feb 23;37(2):389-93. doi: 10.1016/j.jpba.2004.10.022. 

**Litjens 2022** Litjens CHC, Verscheijden LFM, Bolwerk C, Greupink R, Koenderink JB, van den Broek PHH, van den Heuvel JJMW, Svensson EM, Boeree MJ, Magis-Escurra C, Hoefsloot W, van Crevel R, van Laarhoven A, van Ingen J, Kuipers S, Ruslami R, Burger DM, Russel FGM, Aarnoutse RE, Te Brake LHM. Prediction of Moxifloxacin Concentrations in Tuberculosis Patient Populations by Physiologically Based Pharmacokinetic Modeling. J Clin Pharmacol. 2022 Mar;62(3):385-396. doi: 10.1002/jcph.1972. 

**PK-Sim Ontogeny Database Version 7.3** ([https://github.com/Open-Systems-Pharmacology/OSPSuite.Documentation/blob/38cf71b384cfc25cfa0ce4d2f3addfd32757e13b/PK-Sim%20Ontogeny%20Database%20Version%207.3.pdf](https://github.com/Open-Systems-Pharmacology/OSPSuite.Documentation/blob/38cf71b384cfc25cfa0ce4d2f3addfd32757e13b/PK-Sim%20Ontogeny%20Database%20Version%207.3.pdf))	

**Schlender 2016** Schlender JF, Meyer M, Thelen K, Krauss M, Willmann S, Eissing T, Jaehde U. Development of a Whole-Body Physiologically Based Pharmacokinetic Approach to Assess the Pharmacokinetics of Drugs in Elderly Individuals. Clin Pharmacokinet. 2016 Dec;55(12):1573-1589. 	

**Siefert 1999** Siefert HM, Domdey-Bette A, Henninger K, Hucke F, Kohlsdorfer C, Stass HH. Pharmacokinetics of the 8-methoxyquinolone, moxifloxacin: a comparison in humans and other mammalian species. J Antimicrob Chemother. 1999 May;43 Suppl B:69-76. doi: 10.1093/jac/43.suppl_2.69. PMID: 10382878.

**Stass and Kabitza 1999** Stass H, Kubitza D. Pharmacokinetics and elimination of moxifloxacin after oral and intravenous administration in man. J Antimicrob Chemother. 1999 May;43 Suppl B:83-90. doi: 10.1093/jac/43.suppl_2.83. 

**Sullivan 1999** Sullivan JT, Woodruff M, Lettieri J, Agarwal V, Krol GJ, Leese PT, Watson S, Heller AH. Pharmacokinetics of a once-daily oral dose of moxifloxacin (Bay 12-8039), a new enantiomerically pure 8-methoxy quinolone. Antimicrob Agents Chemother. 1999 Nov;43(11):2793-7. doi: 10.1128/AAC.43.11.2793.

**U.S. Food and Drug Administration 2000** U.S. Food and Drug Administration. Avelox (moxifloxacin) [biopharmaceutics review]. 2000. Available at: [https://www.accessdata.fda.gov/drugsatfda_docs/nda/99/21-085_Avelox_biopharmr.pdf](https://www.accessdata.fda.gov/drugsatfda_docs/nda/99/21-085_Avelox_biopharmr.pdf)

**U.S. Food and Drug Administration 2016** U.S. Food and Drug Administration. Moxifloxacin hydrochloride [package insert]. 2016. Available at: [https://www.accessdata.fda.gov/drugsatfda_docs/label/2016/021085s063lbl.pdf](https://www.accessdata.fda.gov/drugsatfda_docs/label/2016/021085s063lbl.pdf)

**U.S. Pharmacist 2023** U.S. Pharmacist. Moxifloxacin 20 mg/mL Oral Suspension. 2023. Available at: [https://www.uspharmacist.com/article/moxifloxacin-20-mg-ml-oral-suspension](https://www.uspharmacist.com/article/moxifloxacin-20-mg-ml-oral-suspension)

**Willmann 2019** Willmann S, Frei M, Sutter G, Coboeken K, Wendl T, Eissing T, Lippert J, Stass H. Application of Physiologically-Based and Population Pharmacokinetic Modeling for Dose Finding and Confirmation During the Pediatric Development of Moxifloxacin. CPT Pharmacometrics Syst Pharmacol. 2019 Sep;8(9):654-663. doi: 10.1002/psp4.12446. 

