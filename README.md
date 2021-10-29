# Drug repurposing for COVID-19 based on protein-protein and drug-protein interaction network

Authors: Melissa Alegría-Arcos, Tábata Barbosa, Felipe Sepúlveda, Janneth González, Germán Combariza and David Ramírez

## Abstract
<div align="justify">In this work we have collected information regarding the protein-virus interaction and also the protein-drug interaction, representing these data as a network that allows a more visual analysis. Additionally, considering this information we have obtained statistical metrics of the networks. This data analysis has allowed us to obtain relevant information on which proteins and drugs are the most relevant in this interaction network. This method not only allows us to focus on viral proteins as the main targets in the COVID-19 disease, but also reveals that some human proteins could be important in the study of drug repurposing.</div>
 

## About this repository
<div align="justify">To support our analysis we have reported the steps to obtain the information from Chembl databases as well as its processing. In addition you will find information about the further analysis of the networks using R.</div>
 
 
 ## Retrieve Protein-Protein Interactions data

Four datasets were used to retrive the information:
   
    1.-
    
    2.-
    
    3.-
    
    4.-
    
<div align="justify">Then, a pipeline using [Knime analytics platform](https://www.knime.com/str) was built to obtain human protein-protein interaction from the [STRING](https://string-db.org/) database for each protein obtained in the three datasets previously mentioned. This Knime pipeline can be accesesed <a href="https://github.com/ramirezlab/COVID-protein-drug-network/blob/main/Files/STRING-interactions.knwf" target="_blank"><b>here</b></a>.</div>
 
 ## Retrieve Compounds and Target from Chembl related to SARS-COV-2 data.
 
 #### We generated two jupyter notebooks that can be followed to obtain the necessary data to replicate our dataset.

  <div align="justify"> Firstly, Data about Compounds and Targets were retrieve from ChEMBL database following the pipeline described in <a href="https://github.com/ramirezlab/COVID-protein-drug-network/blob/main/ChEMBL_compounds_targets.ipynb" target="_blank"><b>Here</b></a>.</div>
 
  <div align="justify"> Secondly, a pipeline to filter drugs based on activities values <a href="https://github.com/ramirezlab/COVID-protein-drug-network/blob/main/Filtering_drugs.ipynb" target="_blank"><b>Here</b></a>.</div>
 
 #### Addionaly, we provied raw datafiles for compounds present in ChEMBL SARS-CoV-2 section.
 
  <div> <a href="https://github.com/ramirezlab/COVID-protein-drug-network/blob/main/chembl_covid_raw.csv" target="_blank"><b>Raw data</b></a> </div>
 
 #### And, raw data about activities for each drugs obtained after cURL queries:
 
  <div> Ki values for each drug: <a href="https://github.com/ramirezlab/COVID-protein-drug-network/blob/main/data_Ki.csv" target="_blank"><b>Ki</b></a> </div>
  
  <div> IC50 values for each drug: <a href="https://github.com/ramirezlab/COVID-protein-drug-network/blob/main/data_IC50.csv" target="_blank"><b>IC50</b></a> </div>
  
 #### Finally, we provide a Supplementary table with each filtered compound-target pair and their respective Ki and IC50 values: 
 
 - `Supplementary_data_Filtered_Drugs_Activities.tsv`: 1999 drugs and 1279 targets pairs filtered using as threshold Ki <= 5000 nM or IC50 <= 5000 nM.
 
 
 
 ## Network Analysis
 
<div align="justify">For all the network analysys we used Graph Theory.
<a href="https://github.com/ramirezlab/COVID-protein-drug-network/tree/main/R-NetworkAnalysis" target="_blank"><b>Here</b></a> we report the R pipeline, which we use for all reported analyses.  This pipeline can be applied to other networks if required.</div>
 
### Supplementary Information

- `Supplementary_Data_1.xlsx`:  The list of top 150 novel drug-target interactions predicted by DTINet, which was trained based all on drugs and targets that have at least one known interacting pair. Known drug-target pairs (corresponding to those non-zero entries in the drug-target interaction matrix) and novel predicted DTIs that share homologous proteins (with sequence identity scores >40%) with known DTIs were excluded from the list.
- `Supplementary_Data_2.xlsx`:  The entire list of novel drug-target interactions predicted by DTINet, which was trained based on all drugs and targets that have at least one known interacting pair.
- `Supplementary_Data_3.xlsx`:  Examples of the novel predictions which can be supported by the previous known evidence in the literature.

 
 ## Citation
 

    @article{Alegría-Arcos,
      author = {Melissa Alegría-Arcos, Tábata Barbosa, Felipe Sepúlveda, Janneth González, Germán Combariza and David Ramírez},
      title = {Drug repurposing for COVID-19 based on protein-protein and drug-protein interaction network. },
      doi = {XX.XX/sXX-0Xx-00XX0-X},
      url = {https://doi.org/XX},
      year  = {20xx},
      month = {x},
      publisher = {xx},
      volume = {x},
      number = {x},
      journal = {xxx}
    }

## Contacts

If you have any questions or comments, please feel free to email David Ramirez (dramirezs[at]udec[dot]cl).
