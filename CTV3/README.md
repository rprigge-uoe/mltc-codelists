# Clinical Terms v3 code lists

This folder contains the CTV3 code lists.

Each code list includes 4 columns:

* Code: CTV3 code
* Description: CTV3 code description
* Condition: long-term health condition
* Sub-condition: sub-condition, where applicable; otherwise the same as the condition column

Please note that care must be taken if opening and saving these files in Microsoft Excel. For example, if the atrial fibrillation code list is opened in Excel the code '3272.' (ECG: atrial fibrillation) is automatically converted to '3272' (without the fullstop).

We applied a two-step process of systematically identifying existing CTV3 code-lists and creating new CTV3 code-lists for conditions with no published code-list. For each condition, we searched for matching CTV3 code-lists in the OpenSafely repository [1], on the UK Biobank website [2], by contacting topic experts, and through a review of existing literature. For each condition with at least one existing CTV3 code-list, we created a combined code-list containing all codes that were included in one or more existing code-list and any additional codes identified through mapping relevant Read v2 codes to potentially relevant CTV3 codes. For each condition with an existing Read v2 code-list but no existing CTV3 code-list, we developed new CTV3 code-lists. A clinician then selected clinically relevant codes for inclusion in our project.

References:
1.	University of Oxford for the Bennett Institute for Applied Data Science. OpenSAFELY codelists 2022 [20/02/2023]. Available from: https://www.opencodelists.org/codelist/opensafely/
2.	UK Biobank. Resource 594 - Code lists for algorithmically-defined outcomes [20/02/2023]. Available from: https://biobank.ndph.ox.ac.uk/showcase/refer.cgi?id=594