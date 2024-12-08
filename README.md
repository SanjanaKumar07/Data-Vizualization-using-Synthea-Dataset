# Data-Vizualization-using-Synthea-Dataset
**Tableau Dashboard Link** - https://public.tableau.com/app/profile/sanjana.kumar6755/viz/SyntheaHealthcareDataVisualization/FinalWorksheet?publish=yes

## Workflow 
1)  Data Generation Process: Synthea Dataset
- Generated a synthetic dataset containing 11,410 patient records across the state of Washington.
- Used specific commands to generate the data
Commands:  
```
java -jar synthea-with-dependencies.jar  
java -jar synthea-with-dependencies.jar -p 10000 Washington --exporter.csv.export=true -s 777
```
- Captured successful data download.
- If you want to download the files please find it here : https://drive.google.com/drive/folders/1xHn_TbvJH6r-b0GMcq6K-L3wzpWXLGmw?usp=sharing
```
Running with options:
Population: 10000
Seed: 777
Provider Seed:1733097479793
Reference Time: 1733097479793
Location: Washington
Min Age: 0
Max Age: 140

Records: total=11410, alive=10000, dead=1410
RNG=10000
Clinician RNG=5160
```
2)  Data Exploration: Excel
- Analyzed all the generated files to understand the structure and relationships between the tables.
- Identified relevant tables based on the specific questions to be answered.
3)  Data Cleaning Process: Python
-	Checked for null values and duplicates in relevant files to identify discrepancies in the data.
-	Jupyter Notebook path : csv/app.ipynb
![image](https://github.com/user-attachments/assets/4c015421-894a-406e-97f6-7d4b43fa4471)
4) Data Visualization: Tableau
- Combined tables appropriately to ensure accurate and meaningful visualizations.
- Created visualizations tailored to address each specific question.
- Developed calculated fields for key variables using custom formulas.
  
## Features of the Dashboard
- Hover over each metric to see a tooltip with information
- All values in the output were cross verified with excel values using pandas (Jupyter Notebook path : csv/app.ipynb and csv/new_app.ipynb)

## Visualization Details

#### Age Group Distribution(patients.csv):  
1.	Percentage of patients across all age groups
2.	Count of patients across all age groups
      
#### Psychiatric Diagnoses (conditions.csv, patients.csv):  
1.	Total count of psychiatric patients
2.	Number of psychiatric cases reported
3.	Number of patients for each psychiatric diagnosis
   
#### PHQ-9 scores (observations.csv, patients.csv, conditions.csv):
1.	Number of patients with PHQ-9 value greater than 10
2.	Number of patients with PHQ-9 value greater than 10 according to age group
3.	Patient information of people who have PHQ-9 value greater than 10 with diagnosis and value of PHQ-9 
#### Depression Treatment Analysis (medications.csv, observations.csv, patients.csv):
1.	Key takeaways from depression treatment analysis
2.	Number of patients who did not receive antidepressant treatment withing the first 90 days of diagnosis according to age and gender
3.	Patient information of people who did not receive antidepressant treatment withing the first 90 days of diagnosis with date difference
#### Bonus: CPT Code Utilization (procedures.csv, conditions.csv):
1. Frequency of CPT codes used in patients with psychiatric-related ICD-10 codes.
2. Frequency of CPT codes used in patients with the procedure names.

Process : 
1. Getting all the encounters related to psychiatric condition descriptions. I did this by applying the filter on descriptions of conditions and getting the list of unique encounter ids. (Python)
2. After this, I took a look in the procedures table to find all the procedures done for these encounter ids that were related to psychiatric conditions and noted down the descriptions of these procedures. (Python)
3. I researched on ways to find the mapping from SNOMED of procedures to CPT codes but all the tools I found for this were paid so I just got the CPT codes for these descriptions manually from a couple of quick google searches. (Python)
4. Now that I had a mapping from description of the procedures to CPT codes, I ran a small piece of code that generated a new csv file 'CPT_DATA' where I include all the procedure descriptions and the CPT Codes. (Python)
5. Using the new csv file, I plotted a histogram plot to represent the frequency of the CPT codes. (Tableau)
- Researched multiple resources to gain more information on how to use the existing data for CPT codes and ICT-10 code
- References used for the research
  - https://github.com/synthetichealth/synthea/issues/403
  - https://stackoverflow.com/questions/tagged/hl7-fhir?page=10&sort=Votes&pageSize=50
  - https://pmc.ncbi.nlm.nih.gov/articles/PMC6416981/
  - SNOMED to ICD-10: https://www.nlm.nih.gov/research/umls/mapping_projects/snomedct_to_icd10cm.html
  -  SNOMED to CPT: https://www.findacode.com/tools/map-a-code/snomed-cpt.php
  -  SNOMED to CPT: https://forums.ohdsi.org/t/mapping-icd10pcs-and-cpt-procedure-codes-to-snomed/18402
  -  SNOMED to CPT: https://confluence.hl7.org/download/attachments/144977510/AMA%20-%20SNOMED-CPT%20Mappings%20-%20Prior%20Auth.pptx?version=1&modificationDate=1670619604248&api=v2  

## Assumptions made in the process:
- Manually compiled a list of psychiatric diagnoses and applied a filtering process to refine the data.
- Incorporated data from both deceased and living individuals for a comprehensive analysis.
- Assessed whether treatment was given for the following diagnosis without specifically verifying if the medication was classified as an "anti-depressant."

## References 
https://github.com/synthetichealth/synthea/wiki/Basic-Setup-and-Running
https://synthetichealth.github.io/synthea/
https://github.com/synthetichealth/synthea/blob/master/src/main/resources/synthea.properties
https://github.com/synthetichealth/synthea/wiki/CSV-File-Data-Dictionary
https://github.com/synthetichealth/synthea/tree/master/src/main/resources

