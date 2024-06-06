# Read Version 2 code lists

This folder contains the Read v2 code lists.

Each code list contains 4 columns: 
* Code: Read v2 code
* Description: Read v2 code description
* Condition: long-term health condition
* Sub-condition: sub-condition, where applicable; otherwise the same as the condition column

Please note that care must be taken if opening and saving these files in Microsoft Excel. For example, if the atrial fibrillation code list is opened in Excel the code '3272.' (ECG: atrial fibrillation) is automatically converted to '3272' (without the fullstop).

Read version 2 codes consist of 7 digits, however the UK Biobank primary care data only provides the first 5 digits of the codes. Thus the code lists in this repository, which were adapted for use with UK Biobank data, only contain the first 5 digits of the codes. Further information about Read version 2 codes, and how we adapted the 7 digit Read v2 code lists from Kuan et al. (2019) to 5 digit Read v2 code lists is provided below.

The first 5 digits define the clinical concept and the final 2 digits define the term used to describe the clinical concept. For each clinical concept there is a preferred term. Many clinical concepts also have synonyms. For example, the preferred term and synonyms for the Read version 2 code F49.. are:
- **F49..00**  Blindness and low vision
- **F49..11**  Impaired vision
- **F49..12**  Low vision
- **F49..13**  Partial sight
- **F49..14**  Sight impaired

Usually the preferred terms and synonyms share the same meaning, however there are exceptions. For example, the preferred term and synonyms for the Read version 2 code G65.. are:
- **G65..00**  Transient cerebral ischaemia
- **G65..11**  Drop attack
- **G65..12**  Transient ischaemic attack
- **G65..13**  Vertebro-basilar insufficiency

However, transient cerebral ischaemia, commonly known as a transient ischaemic attack, is different from vertebro-basilar insufficiency and drop attacks. Further information about Read version 2 codes can be found in this useful guide: https://www.scimp.scot.nhs.uk/better-information/clinical-coding/scimp-guide-to-read-codes.  

The Read v2 code lists published by Kuan et al. (2019), which we adapted for this project, included 7 digit Read v2 codes. For some clinical concepts all of the preferred terms and synonyms were included, whereas for other clincal concepts only a subset of these were included. We adapted the 7 digit Read v2 code lists provided by Kuan et al. as follows:

For each condition, unless otherwise specified, we adapted the code list provided by Kuan et al. (2019) as follows:
1. We trimmed the 7 digit Read version 2 codes provided by Kuan et al. to 5 digit codes and ascertained their frequency in the UK Biobank primary care data released in September 2019.
2. We excluded any 5 digit codes that never appeared in the UK Biobank primary care data.
3. Of the remaining 5 digit codes:
   
    a. Where Kuan et al. (2019) included all of the preferred terms and synonyms, the 5 digit code was included in our code list
   
    b. Where Kuan et al. (2019) only included a subset of the preferred terms and synonyms, a clinician reviewed the 5 digit code and decided whether it should be included in our code list.


References:
> Kuan, V., Denaxas, S., Gonzalez-Izquierdo, A., Direk, K., Bhatti, O., Husain, S., Sutaria, S., Hingorani, M., Nitsch, D., Parisinos, C. A., Lumbers, R. T., Mathur, R., Sofat, R., Casas, J. P., Wong, I. C. K., Hemingway, H., & Hingorani, A. D. (2019). A chronological map of 308 physical and mental health conditions from 4 million individuals in the English National Health Service. The Lancet. Digital health, 1(2), e63–e77. https://doi.org/10.1016/S2589-7500(19)30012-3

