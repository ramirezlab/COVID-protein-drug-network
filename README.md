# Drug repurposing for COVID-19 based on protein-protein and drug-protein interaction network

Authors: Melissa Alegría-Arcos, Tábata Barbosa, Felipe Sepúlveda, German Combariza, Janneth González, Carmen Gil, Ana Martinez and David Ramírez

## Abstract
<div align="justify">In this work we have collected information regarding the protein-virus interaction and also the protein-drug interaction, representing these data as a network that allows a more visual analysis. Additionally, considering this information we have obtained statistical metrics of the networks. This data analysis has allowed us to obtain relevant information on which proteins and drugs are the most relevant in this interaction network. This method not only allows us to focus on viral proteins as the main targets in the COVID-19 disease, but also reveals that some human proteins could be important in the study of drug repurposing.</div>
 

## About this repository
<div align="justify">To support our analysis we have reported the steps to obtain the information from ChEMBL database as well as its processing. In addition you will find information about the further analysis of the networks using R.</div>
 
 
 ## Data Retrieval of Protein-Protein Interactions

Three datasets were used to retrieve the information:
   
1.- <a href= "https://ppi.zoiclabs.io/#/" target="_blank"><b>Krogan’s Lab website</b></a>.
    
2.- <a href= "https://covid19interactome.org/" target="_blank"><b>BioID-based interactome of the SARS-CoV-2 proteome</b></a>.
    
3.-  SARS-CoV-2 proteins in <a href= "https://covid-19.uniprot.org" target="_blank"><b>UniProt</b></a> database as September 2021.
    
    
<div align="justify">Then, a pipeline using <a href= "https://www.knime.com" target="_blank"><b>[Knime analytics platform]</b></a> was built to obtain human protein-protein interaction from the <a href= "https://string-db.org/" target="_blank"><b>[STRING]</b></a> database for each protein obtained in the three datasets previously mentioned. This Knime pipeline can be accesed <a href="https://github.com/ramirezlab/COVID-protein-drug-network/tree/main/Knime_Workflow" target="_blank"><b>here</b></a>.</div>
 
 ## Data Retrieval of Compounds and Target from ChEMBL related to SARS-COV-2
 
 #### We generated two jupyter notebooks that can be followed to obtain the necessary data to replicate our dataset.

 + <div align="justify"> Firstly, data about compounds and targets were retrieve from ChEMBL database following the pipeline described <a href="https://github.com/ramirezlab/COVID-protein-drug-network/blob/main/ChEMBL_dataset/ChEMBL_compounds_targets.ipynb" target="_blank"><b>here</b></a>.</div>
 + <div align="justify"> Secondly, a pipeline to filter drugs based on activities values <a href="https://github.com/ramirezlab/COVID-protein-drug-network/blob/main/ChEMBL_dataset/Filtering_drugs.ipynb" target="_blank"><b>here</b></a>.</div>
 
 #### <div> Addionaly, we provided <a href="https://github.com/ramirezlab/COVID-protein-drug-network/blob/main/ChEMBL_dataset/chembl_covid_raw.csv" target="_blank"><b>raw data files</b></a> for compounds present in ChEMBL SARS-CoV-2 section, and raw data about activities for each drug obtained after the cURL queries: </div>
 
  + <div> Ki values for each drug: <a href="https://github.com/ramirezlab/COVID-protein-drug-network/blob/main/ChEMBL_dataset/data_Ki.csv" target="_blank"><b>Ki</b></a> </div>
  + <div> IC50 values for each drug: <a href="https://github.com/ramirezlab/COVID-protein-drug-network/blob/main/ChEMBL_dataset/data_IC50.csv" target="_blank"><b>IC50</b></a> </div>
  
 #### Finally, here we provide a Supplementary Table with each filtered compound-target pair, as well as their respective Ki and IC50 values: 
 
 - `Supplementary_data_Filtered_Drugs_Activities.tsv`: 1999 drugs and 1279 targets pairs filtered using as threshold Ki <= 5000 nM or IC50 <= 5000 nM.
 
 
 
## Network Analysis
 
<div align="justify">For all the network analyses we used Graph Theory.
<a href="https://github.com/ramirezlab/COVID-protein-drug-network/tree/main/R-NetworkAnalysis" target="_blank"><b>Here</b></a> we report the R pipeline, which we use for all reported analyses.  This pipeline can be applied to other networks if required.</div>

## Cytoscape Files
 
<div align="justify">Both PPI and DPI network files are available for download in the <a href="https://github.com/ramirezlab/COVID-protein-drug-network/tree/main/Cytoscape_Sessions" target="_blank"><b>Cystoscape_Sessions</b></a>.</div>
 
### Supplementary Information

- `Supplementary_Data_1.xlsx`:  The list of top 150 novel drug-target interactions predicted by DTINet, which was trained based all on drugs and targets that have at least one known interacting pair. Known drug-target pairs (corresponding to those non-zero entries in the drug-target interaction matrix) and novel predicted DTIs that share homologous proteins (with sequence identity scores >40%) with known DTIs were excluded from the list.
- `Supplementary_Data_2.xlsx`:  The entire list of novel drug-target interactions predicted by DTINet, which was trained based on all drugs and targets that have at least one known interacting pair.
- `Supplementary_Data_3.xlsx`:  Examples of the novel predictions which can be supported by the previous known evidence in the literature.

 
 ## Citation
 

Melissa Alegría-Arcos, Tábata Barbosa, Felipe Sepúlveda, German Combariza, Janneth González, Carmen Gil, Ana Martinez and David Ramírez
(2022) Drug repurposing for COVID-19 based on protein-protein and drug-protein interaction network.
     

## Contact

If you have any questions or comments, please feel free to email David Ramirez (dramirezs@udec.cl).
