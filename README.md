# Overview

This repository contains the code lists for the Medical Research Council/National Institute for Health Research funded project "Understanding the relationship between depression and trajectories of physical multimorbidity accrual: longitudinal analysis of UK Biobank data" (grant number MC/S028013). 

This project measured 80 long-term physical and mental health conditions. We used Read version 2 (Read v2) and Clinical Terms v3 (CTV3) codes to identify conditions from primary care data. We used ICD-10 codes to identify conditions from hospital, cancer registry and death records. For a subset of conditions, we used both ICD-10 and OPCS-4 codes to identify the conditions from hospital data. We additionally identified conditions using data from the UK Biobank baseline assessment (for more information see: Prigge (2024)). This repository includes information on the Read v2, CTV3, ICD-10 and OPCS-4 code lists. 

We used existing code lists or adapted existing code lists, where available. For ICD-10, OPCS-4 and Read v2, we mostly used or adapted code lists from those published on GitHub (https://github.com/spiros/chronological-map-phenotypes) alongside the paper:
> Kuan, Valerie et al. A chronological map of 308 physical and mental health conditions from 4 million individuals in the English National Health Service. The Lancet Digital   Health, Volume 1, Issue 2, e63 - e77. https://doi.org/10.1016/S2589-7500(19)30012-3

For CTV3, we identified existing code lists from repositories, by contacting topic experts and through a review of existing literature. Where we could not identify any CTV3 code lists for a condition, we developed new code lists through a process which included mapping Read v2 codes and free-text searching of CTV3 descriptions. 

Further details on the origin of each code list are available in the following paper. Please cite this paper if you re-use our code list repository:
> Prigge (2024). Robustly measuring multiple long-term health conditions using disparate linked datasets in UK Biobank. [manuscript in preparation]

# Structure of this repository

This repository includes a folder for each of the four coding systems (Read v2, CTV3, ICD-10 and OPCS-4). Each of the coding system folders includes a README file with additional information relevant to the coding system, as well as the code lists in CSV format. 

## Dictionary
The dictionary.csv file included in this folder maps the 80 conditions to the CSV format code lists. Note that some conditions include multiple sub-conditions, each with their own code list. The file contains the following columns: 
* Category: physical or mental health condition
* System: body system
* Condition: long-term health condition
* Sub-condition: sub-condition, where applicable; otherwise the same as the condition column
* Sub-condition (synonym): any synonym used for the sub-condition
* ReadV2: name of the file that contains the Read v2 codes
* CTV3: name of the file that contains the CTV3 codes
* ICD: name of the file that contains the ICD-10 codes
* OPCS-4: name of the file that contains the OPCS-4 codes (if used)

## Origin of code-lists
The codelists_sources.csv file included in this folder describes the origin of each code list (e.g. whether it is a newly created code lists or a pre-existing code lists), with acknowledgement of the source, where needed. The file contains the following columns: 
* Code list: Name of code list file
* Coding system: One of Readv2, CTV3, ICD-10 or OPCS-4
* Condition: long-term health condition
* Sub-condition: sub-condition, where applicable; otherwise the same as the condition column
* Source: Newly created code-list or acknowledgement of previously existing source

A list of references is included from row 408 onwards.

# Implementation

Most conditions were defined such that if a person has any code for the condition (or one of its sub-conditions, where applicable), then they were defined to have the condition from the date of the earliest recorded code. However, there are some conditions that are defined using different rules.

## Life-long conditions

We included eight life-long conditions (or sub-conditions). If a person had a code for one of these conditions (or sub-conditions), then they were defined to have the condition from their date of birth.

* Autism and Asperger's syndrome
* Intellectual disability
* Down's syndrome
* Cerebral Palsy
* Sickle-cell anaemia
* Thalassaemia
* Cystic Fibrosis
* Juvenile arthritis (within the condition group inflammatory arthritis and other inflammatory conditions)

## Sex-specific conditions

The following conditions were sex-specific. If a person had a code for a condition which was inconsistent with their sex, we assumed the code was incorrect and excluded it.

Men only:
-	Hyperplasia of prostate
-	Erectile dysfunction
-	Primary malignancy – prostate
-	Primary malignancy – testicular
  
Women only:
-	Primary malignancy – cervical
-	Primary malignancy – ovarian
-	Primary malignancy – uterine 


## Diabetes

For people with any diabetes code (a code in the type 1, type 2 or diabetes not otherwise specified code lists), we identified diabetes type (type 1, type 2 or diabetes not otherwise specified) by applying a modified version of the algorithm used by Kuan et al. (see below). We defined diabetes date of diagnosis as the earliest date of any diabetes code.

The algorithm prioritises type 1 or type 2 diabetes diagnosis codes (e.g. type 1 diabetes mellitus) from primary care data, over other codes from primary care data (e.g. dietary advice for type 1 diabetes) and codes from all other sources. The Read v2 and CTV3 code lists for type 1 and type 2 diabetes each include a Diagnosis column which defines whether each code is a diagnosis code (Diagnosis = Y) or not (Diagnosis = N). 

Our modified algorithm is described below:

* If there is at least one primary care diagnosis code for type 2 diabetes and no primary care diagnosis code for type 1 diabetes, then classify the person as type 2 diabetes
* If there is at least one primary care diagnosis code for type 1 diabetes and no primary care diagnosis code for type 2 diabetes, then classify the person as type 1 diabetes
* Else if there are no primary care diagnosis codes, or the primary care diagnosis codes are inconsistent
    * If there is at least one record for type 2 diabetes and no record for type 1 diabetes then classify the person as type 2 diabetes
    * If there is at least one record for type 1 diabetes and no record for type 2 diabetes then classify the person as type 1 diabetes
* Else classify the person as diabetes not otherwise specified


## Stroke NOS
We excluded records of stroke not otherwise specified, if there was a subarachnoid haemorrhage record within the previous 28 days (note that dictionary.csv includes a row for subarachnoid haemorrhage - we did not include this as one of our 80 conditions - but we used the code lists for subarachnoid haemorrhage in order to implement this rule).

## Chronic kidney disease (sub-condition of chronic renal disease)
In each of our publications using these code lists, we combined codes for chronic kidney disease (CKD) with serum creatinine codes and serum creatinine measurements from the UK Biobank baseline assessment, as follows: 

*	If the participant had a UK Biobank baseline assessment serum creatinine measurement then
    - We excluded other records (e.g. hospital records) of CKD up to and including the date of the baseline assessment
    - We defined the participant to have CKD from the date of the baseline assessment if they had an eGFR of less than 60 ml per minute per 1.73 m2. We calculated eGFR from serum creatinine measurements using the CKD-EPI Creatinine Equation (2021) ([DOI: 10.1056/NEJMoa2102953](https://www.nejm.org/doi/10.1056/NEJMoa2102953)).  
*	If the participant did not have a baseline assessment serum creatinine measurement then we defined CKD if
     *	the person had a code for CKD, or
     *	if the person had two eGFR values in their primary care record of less than 60 ml per minute per 1.73 m2 within 90 days (in which case we took the date of the second value as the date of diagnosis). We calculated eGFR from serum creatinine measurements as above, excluding serum creatinine values less than 10 or greater than 2000. If there were multiple serum creatinine measurements on a single day, we used their mean value instead of the individual values. Our code list repository includes Read V2 and CTV3 code lists for serum creatinine. 

# Publications
The following publications use the code lists included in this repository 
* Prigge (2024). Robustly measuring multiple long-term health conditions using disparate linked datasets in UK Biobank. [manuscript in preparation]
* To be added
