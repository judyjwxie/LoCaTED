# Low Carbon Transition Employment Distribution (LoCaTED) Model
This GitHub repository contains the source code to evaluate the distributive employment impacts in the US state-level electricity systems. The analysis framework compiles open-source models and publicly available demographic data to evaluate how the low carbon transition may impact the sectoral, skill-level, and gender composition of the workforce. The open-source models are the Regional Energy Deployment System (ReEDS) and Jobs and Economic Development Impact (JEDI) models developed by the National Renewable Energy Laboratory (NREL). More detailed descriptions of the framework and data sources can be found in the Methods section of Xie et al. 

Any correspondence can be made to Judy Xie: j.xie20@imperial.ac.uk

## Software Requirements
The scripts are written in Python (Version 3.8.5) using Jupyter Notebooks. Additional software (e.g. GAMS and R) is required to run the ReEDS model beyond the Standard Scenarios. The JEDI model operates on Excel Macros. 

## Data Requirements
Access to the ReEDS model GitHub can be requested from the NREL website (https://www.nrel.gov/analysis/reeds/request-access.html). The annual Standard Scenarios can be downloaded from the Scenario Viewer (https://scenarioviewer.nrel.gov/). The JEDI model can be downloaded from the NREL website (https://www.nrel.gov/analysis/jedi/models.html). The following files need to be placed in the correct directories for this analysis to run,
- The complete suite of the JEDI models should be placed in directory <code>data/JEDI</code> which needs to be created. The list of the JEDI model technologies used by Xie et al. and the corresponding model versions can be found in the Supplementary Information. The existing file <code>analysis/1_ReEDS_to_JEDI/tech_specs.xlsx</code> shows the locations of the input project specification cells and those of the output cells indicating the job creation by sector.
- The ReEDS model outputs should be placed in directory <code>data/ReEDS</code>. The files should follow the format of the Standard Scenarios like the dummy scenarios in the folder. 
- The ReEDS transmission assumptions located in <code>ReEDS_OpenAccess-main/inputs/transmission</code> are used in this analysis. This entire directory should be placed in <code>data/ReEDS/transmission</code> here. 
- The ReEDS assumption on construction time in file <code>ReEDS_OpenAccess-main/inputs/construction_times/construction_times_default.csv</code> is also used in this analysis. This file should be placed in <code>data/ReEDS</code> here.

## Running the Analysis
### ReEDS to JEDI 
The first step of the analysis is to convert the ReEDS scenario outputs to sectoral employment through the JEDI model. The Jupyter Notebook <code>analysis/1_ReEDS_to_JEDI/batch_ReEDS_to_Jobs.ipynb</code> batch runs the process. The variable <code>orig_scen</code> can be a list of basic scenarios, such as "Mid_Case" and the batch process can run the analysis on all emission reduction scenarios including "Mid_Case_95_by_2050" and "Mid_Case_95_by_2035". After the initial run, an additional Jupyter Notebook <code>analysis/1_ReEDS_to_JEDI/batch_post_treatment.ipynb</code> needs to be run to include the jobs associated with the coal and natural gas supply chains. 

The outputs are stored in <code>analysis/1_ReEDS_to_JEDI/output</code> for further analysis. <code>Fig1_historical_comparison.ipynb</code> visualizes the state-level employment impacts compared to historical events. 

### JEDI to Demographics
The second step of the analysis is to disaggregate sectoral employment impacts into distributed gender and skill-level (ONET Job Zone) impacts. The Jupyter Notebook <code>analysis/2_JEDI_to_demographics/batch_emp_dist.ipynb</code> batch runs the process. 

The outputs are stored in <code>analysis/2_JEDI_to_demographics/output</code> for further analysis. <code>Fig5_women_employment.ipynb</code> visualizes the gender implication. 

### Demographics to Indicators
The third and final step of the analysis is to compile the distributed impacts into indicators (i.e. Employment Change and Net Employment Change). <code>analysis/2_JEDI_to_demographics/Process_Heatmap.ipynb</code> integrates the employment impacts by state, sector, and country. <code>Fig3_heatmap.ipynb</code> visualizes the employment impacts from these perspectives. <code>analysis/2_JEDI_to_demographics/Process_sum.ipynb</code> calculates the overall impact across states and the outputs are used in QGIS for Figure 2. <code>analysis/2_JEDI_to_demographics/Process_jobzone_detailed.ipynb</code> evaluates the impacts across states in different Job Zones and the outputs are used in QGIS for Figure 4. 


