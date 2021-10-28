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
