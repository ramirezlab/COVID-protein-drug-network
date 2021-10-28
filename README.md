# Drug repurposing for COVID-19 based on protein-protein and drug-protein interaction network

Authors: Melissa Alegría-Arcos, Tábata Barbosa, Felipe Sepúlveda, Janneth González, Germán Combariza and David Ramírez

## Abstract
In this work we have collected information regarding the protein-virus interaction and also the protein-drug interaction, representing these data as a network that allows a more visual analysis. Additionally, considering this information we have obtained statistical metrics of the networks. This data analysis has allowed us to obtain relevant information on which proteins and drugs are the most relevant in this interaction network. This method not only allows us to focus on viral proteins as the main targets in the COVID19 disease, but also reveals that some human proteins could be important in the study of drug repurposing.

## About this repository
To support our analysis we have reported the steps to obtain the information from Chembl databases as well as its processing. In addition you will find information about the further analysis of the networks using R.
 
 ## Retrive Protein-Protein Interactions data

Four datasets were used to retrive the information:
    1.-
    
    2.-
    
    3.-
    
    4.-
    
Then, a pipeline using [Knime analytics platform](https://www.knime.com/str) was built to obtain human protein-protein interaction from the [STRING](https://string-db.org/) database for each protein obtained in the three datasets previously mentioned
 
 ## Retrive Compounds and Target from Chembl related to SARS-COV-2 data.
 
 
 
 ## Network Analysis
 
 For all the network analysys we used Graph Theory. [Here](https://github.com/ramirezlab/COVID-protein-drug-network/tree/main/R-NetworkAnalysis) we report the R pipeline, which we use for all reported analyses.  This pipeline can be applied to other networks if required.
 
 
 ## Citation

Melissa Alegría-Arcos, Tábata Barbosa, Felipe Sepúlveda, Janneth González, Germán Combariza and David Ramírez. Drug repurposing for COVID-19 based on protein-protein and drug-protein interaction network. 

@article{Alegría-Arcos202X,
  author = {Yunan Luo and Xinbin Zhao and Jingtian Zhou and Jinglin Yang and Yanqing Zhang and Wenhua Kuang and Jian Peng and Ligong Chen and Jianyang Zeng},
  title = {Drug repurposing for COVID-19 based on protein-protein and drug-protein interaction network. },
  doi = {XXXXX},
  url = {https://doi.org/XXXXX},
  year  = {202X},
  month = {xxx},
  publisher = {xxx},
  volume = {x},
  number = {x},
  journal = {xxx}
}

# Contacts

If you have any questions or comments, please feel free to email David Ramirez (dramirezs[at]udec[dot]cl).
