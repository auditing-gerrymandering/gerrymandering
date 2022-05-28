# Auditing for Gerrymandering by Identifying Disenfranchised Individuals

This repo is the home of the data and Python scripts/Jupyter notebooks that accompany the paper Auditing for Gerrymandering by Identifying Disenfranchised Individuals, published in ACM FAccT'22.  The bulk of this research was conducted as part of the
2020 Duke University CS+ Program and under the supervision of Prof. Brandon Fain and Vaishali Jain. 

## Team Members:

Carolyn Chen, Duke University '23

Marc Chmielewski, Duke University '22

Jerry Lin, Duke University '23

Samia Zaman, Duke University '22

# Organization

Generally speaking, the repo has been organized into separate code and data segments. Pathing to the data will likely need to be modified to suit your machine, though all references to data are internal to this repo.

# Code

## /visualization
### `diogenes_scatter.ipynb`
Contains the code to create the scatter plots of how fast the gerrymandering score decreases as the simulated annleaing algorithm progresses. 

### `heatmap.ipynb`
Contains the code to create our heatmap visualizations for the paper. 

## /algos
### `acr_VTD.ipynb`
A Python implementation of Levin and Friedler's Automated Congressional Redistricting algorithm (which was originally written in Java). Takes `NCabs_VTD` shapefiles as input. 

### `Diogenes_stochastic_new.ipynb`
A swapping algorithm to reduce the gerrymandering score, choosing swaps in a stochastic greedy manner. We compare the results of this stochastic greedy algorithm with a simulated annealing approach in our paper. 

### `Diogenes_simulated_annealing_jerry.ipynb`
A swapping algorithm to reduce the gerrymandering score, choosing swaps via simulated annealing. This is the algorithm presented in our paper. 

### `gmand_score.ipynb`
Compute the gerrymandering score of any districting with respect to our 1,055 compliant comparators. 

## /data_processing_notebooks
### `process_VTD_data.ipynb`
Creates the `NCabs_VTD` dataset by combining the NC shapefile `tl_2012_37_vtd10.zip` in Herschlag et al.'s repo [here](https://git.math.duke.edu/gitlab/gjh/nccongressionalensembles/-/tree/master/) with census and election data from the Tufts MGGG group [here](https://github.com/mggg-states/NC-shapefiles). We then did a bit more of additional processing—including absorbing two nested VTDs and calculating the neighbors of each VTD. 

# Data

## /VTD_District_Pairings
Each text file allows you to construct an initial districting. Each file contains two columns. The first column is the VTD number, and the second column is the district that VTD is assigned to. 

`code_data_NC_NCAbs_2016.txt`: for the NC map used in 2012 elections (the 2016 map). Retrieved from Herschlag et al.'s repo [here](https://git.math.duke.edu/gitlab/gjh/nccongressionalensembles/-/blob/master/code/data/NC/NC_2016.txt).

`code_data_NC_NCAbs_2012.txt`: for the NC map used in 2016 elections (the 2012 map). Retrieved from Herschlag et al.'s repo [here](https://git.math.duke.edu/gitlab/gjh/nccongressionalensembles/-/blob/master/code/data/NC/NC_2012.txt).

`acr_VTD.txt`: for the map produced by Levin and Friedler's Automated Congressional Redistricting (ACR) algorithm. Produced by `acr_VTD.ipynb`.

`code_data_NC_NCAbs_Judges.txt`: for Judges map. Retrieved from Herschlag et al.'s repo [here](https://git.math.duke.edu/gitlab/gjh/nccongressionalensembles/-/blob/master/code/data/NC/NC_Judges.txt).

## /shapefiles
`NCabs_VTD`: Contains the shapefiles for each NC VTD. Contains the following columns: 
['VTD_num', 'GEOID10', 'ALAND10', 'AWATER10', 'COUNTY_FIP', 'loc_prec',
       'VTD_Name', 'total_pop', 'total_18+', 'EL08G_GV_D', 'EL08G_GV_R',
       'EL08G_GV_L', 'EL08G_GV_T', 'EL08G_USS_', 'EL08G_US_1', 'EL08G_US_2',
       'EL08G_US_3', 'EL08G_US_4', 'EL10G_USS_', 'EL10G_US_1', 'EL10G_US_2',
       'EL10G_US_3', 'EL10G_US_4', 'EL12G_GV_D', 'EL12G_GV_R', 'EL12G_GV_L',
       'EL12G_GV_W', 'EL12G_GV_1', 'EL12G_GV_T', 'EL14G_USS_', 'EL14G_US_1',
       'EL14G_US_2', 'EL14G_US_3', 'EL14G_US_4', 'Shape_Leng', 'Shape_Area',
       'EL12G_PR_D', 'EL12G_PR_R', 'EL12G_PR_L', 'EL12G_PR_W', 'EL12G_PR_1',
       'EL12G_PR_T', 'EL16G_PR_R', 'EL16G_PR_D', 'EL16G_PR_L', 'EL16G_PR_W',
       'EL16G_PR_T', 'EL16G_USS_', 'EL16G_US_1', 'EL16G_US_2', 'EL16G_US_3',
       'EL16G_GV_D', 'EL16G_GV_R', 'EL16G_GV_L', 'EL16G_GV_T', 'BPOP', 'nBPOP',
       'judge', 'newplan', 'oldplan', 'TOTPOP', 'NH_WHITE', 'NH_BLACK',
       'NH_AMIN', 'NH_ASIAN', 'NH_NHPI', 'NH_OTHER', 'NH_2MORE', 'HISP',
       'H_WHITE', 'H_BLACK', 'H_AMIN', 'H_ASIAN', 'H_NHPI', 'H_OTHER',
       'H_2MORE', 'VAP', 'hispanic', 'white', 'african_am', 'am_indian_',
       'asian', 'hawaii/pac', 'other_race', '2+races', 'my_neighbo',
       'hor12_dem', 'hor12_rep', 'hor12_othe', 'hor16_dem', 'hor16_rep',
       'hor16_othe', 'geometry']

Columns of interest: 

* **loc_prec:** A unique identifier for each of North Carolina's VTDs
* **VTD_num**: Also a unique identifier for each of North Carolina's VTDs. Merge the VTD shapefiles with the district pairings using this column.
* **EL16G_PR_D**: Votes casted for Democratic presidential candidate in 2016 election 
* **EL16G_PR_R**: Votes casted for Republican presidential candidate in 2016 election 
* **EL16G_PR_T**: Total votes casted in 2016 presidential election 
* **TOTPOP**: total population of the VTD
* **neighbors**: a list of `loc_prec` of VTDs that neighbor this VTD 

The code and data to create this dataset is explained in the description of `process_VTD_data.ipynb`. 

### District Shapefiles 
The four files below are shapefiles for each initial districting, although these shapefiles can be constructed using the VTD-district pairings and the individual VTD shapefiles. There are two columns — one column is the district number (which corresponds to the district numbers in the VTD-district pairings) and the second column is the actual geometry. 

`NC_judges_shapefiles`: for Judges map

`2016_NC_shapefiles_updated`: for 2016 map

`2012_NC_shapefiles_updated`: for 2012 map

`acr_shapefiles`: for ACR map

### Comparator Data
We used the comparators generated by Herschlag et al's, from the rank 0 chain. The sample plans, and the file that lists the compliant plans, can be downloaded [here](https://git.math.duke.edu/gitlab/gjh/nccongressionalensembles/-/tree/master/ensembles/main/rank_0).












