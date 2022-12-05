# distributive-employment
This GitHub repository contains the source code to evaluate the distributive emeployment impacts in the US state-level electricity systems. The analysis framework compiles open-source models and pubicly available demographic data to evaluate how the low carbon transition may impact the sectoral, skill-level, and gender composition of the workforce. The open-source models are the Regional Energy Deployment System (ReEDS) and Jobs and Economic Development Impact (JEDI) models developed by the National Renewable Energy Laboratory (NREL). More detailed descriptions of the framework and data sources can be found in the Methods section of Xie et al. 

Any correspondance can be made to Judy Xie: j.xie20@imperial.ac.uk

## Software Requirements
The scripts are written in Python (Version 3.8.5) using Jupyter Notebooks. Additional softwares (e.g. GAMS and R) are required to run the ReEDS model beyond the Standard Scenarios. The JEDI Model operates on Excel Macros. 

## Data Requirements
Access to the ReEDS model GitHub can be requested from the NREL website (https://www.nrel.gov/analysis/reeds/request-access.html) and the annual Stanfard Scenarios can be downloaded from the Scenario Viewer (https://scenarioviewer.nrel.gov/). The JEDI model can be downloaded from the NREL website (https://www.nrel.gov/analysis/jedi/models.html). The following files need to be placed in the correct directories in order for this analysis to run,
- The complete suite of the JEDI models should be placed in directory <code>data/JEDI</code> which needs to be created. The list of the JEDI model technologies used in Xie et al. and the corresponding model versions can be found in the Supplementary Information. The existing file <code>analysis/1_ReEDS_to_JEDI/tech_specs.xlsx</code> shows the locations of the input project specification cells and those of the output cells indicating the job creation by sector.
- The the ReEDS model outputs should be placed in directory <code>data/ReEDS</code>. The files should follow the format of the Standard Scenarios like the dummy scenarios in the folder. 
- The transmission assumptions from the ReEDS model <code>ReEDS_OpenAccess-main/inputs/transmission</code> are used in this analysis. This entire directory should be placed in <code>data/ReEDS/transmission</code> here. 

## Running the Analysis
### ReEDS to JEDI 
The first step of the analysis is to convert the ReEDS scenarios outputs to sectoral employment through the JEDI model. The Jupyter Notebook <code>analysis/1_ReEDS_to_JEDI/batch_ReEDS_to_Jobs.ipynb</code> batch runs the process. The variable <code>orig_scen</code> can be a list of basic scenarios, such as "Mid_Case" and the batch process can run the analysis on all emission reduction scenarios including "Mid_Case_95_by_2050" and "Mid_Case_95_by_2035". After the initial run, an additional Jupyter Notebook <code>analysis/1_ReEDS_to_JEDI/batch_post_treatment.ipynb</code> needs to be run to include the jobs associated with the coal and natural gas supply chains. 

The outputs are stored in <code>analysis/1_ReEDS_to_JEDI/output</code> for further analysis. <code>Fig1_historical_comparison.ipynb</code> visualizes the state-level employment impacts compared to historical events. 

### JEDI to Demographics
The second step of the analysis is to disaggregate sectoral employment impacts into distributed gender and skill-level (ONET Job Zone) impacts. The Jupyter Notebook <code>analysis/2_JEDI_to_demographics/batch_emp_dist.ipynb</code> batch runs the process. 

The outputs are stored in <code>analysis/2_JEDI_to_demographics/output</code> for further analysis. <code>Fig5_women_employment.ipynb</code> visualizes the gender implication. 

### Demographics to Indicators
The third and final step of the analysis is to compile the distributed impacts into indicators (i.e. Employment Change and Net Employment Change). <code>analysis/2_JEDI_to_demographics/Process_Heatmap.ipynb</code> integrates the employment impacts by state, sector, and country. <code>Fig3_heatmap.ipynb</code> visualizes the employment impacts from these perspectives. <code>analysis/2_JEDI_to_demographics/Process_sum.ipynb</code> calculates the overall impact across states and the outputs are used in QGIS for Figure 2. <code>analysis/2_JEDI_to_demographics/Process_jobzone_detailed.ipynb</code> evaluates the impacts across states in different Job Zones and the outputs are used in QGIS for Figure 4. 


