# READ ME 
This repository provides sample code for calculating the Nutrient Composition Diversity Index (NCDI) from 24-hour recall data.  The procedures are described in:
  > A pilot study of the Nutrient Composition Diversity Index in a sample of healthy US adults shows positive associations with adherence to the Dietary Guidelines for Americans and micronutrient adequacy
>
> Authors: Gersten ZP, Wilson SMG, Larke JA, Lemay DG and Caswell BL.\
>  Manuscript under review.

# Requirements
## Software
- R
- Stata

## USDA Food Composition Databases
-   Food and Nutrient Database for Dietary Studies (FNDDS), versions 4.1 and 2011-2012, publicly available at https://www.ars.usda.gov/northeast-area/beltsville-md-bhnrc/beltsville-human-nutrition-research-center/food-surveys-research-group/docs/fndds-download-databases/
-   USDA National Nutrient Database for Standard Reference (SR), Release 22 and Release 23, publicly available at https://www.ars.usda.gov/northeast-area/beltsville-md-bhnrc/beltsville-human-nutrition-research-center/methods-and-application-of-food-composition-laboratory/mafcl-site-pages/sr11-sr28/

## Dietary intake data
This sample code was developed to calculate NCDI from 24-hour dietary recall data collected in the 2014 and 2016 releases of the Automated Self-Administered 24-Hour Dietary Assessment Tool (ASA24®️).  
These versions of ASA24 assign food codes from FNDDS 4.1 and FNDDS 2011-2012, respectively. Use of this sample code with dietary intake data coded to different releases of FNDDS will result in missing linkages and slight variations in nutrient content estimates, as each FNDDS release adds and retires food codes and updates nutrient composition values for some food codes.

# Procedure
The sample code completes four steps to construct NCDI from FNDDS-coded 24-hour recall data as described by Gersten et al. (2025).

## Step 1: Create Nutrient Trait Matrix
Create a nutrient trait matrix, similar to a food composition table, in which each row is a food item or ingredient, and each column contains a value for its nutrient content\
	    1a. Disaggregate mixed food items to their ingredients using the SR recipes data\
	    1b. Remove ingredients without nutrient values\
	    1c. Repeat for all versions of FNDDS used and append disaggregated datasets\
	    1d. Mean-standardize all values by nutrient\

## Step 2: Calculate Distance Matrix
Calculate Euclidean distances for all pairs of food items or ingredients in the nutrient trait matrix.  The Euclidean distance ($D$) between foods $i$ and $j$ is calculated as:

$$\ D_{i,j} = \sqrt{\sum_{i=1}\^{n} (i_x - j_x)\^2} \$$

where $x$ is a nutrient in the nutrient trait matrix and $n$ is the total number of nutrients in the nutrient trait matrix.

## Step 3: Create Dendrogram
Use hierarchical clustering to arrange food items and ingredients in a dendrogram and calculate the total vertical branch lengths

## Step 4: Score individual diets 
Use the dendrogram to score individual diets by summing the vertical branch lengths to the common node\
	    4a. Disaggregate mixed food items and remove non-nutritive items\
	    4b. Create binary variables indicating the food items or ingredients reported in each dietary recall\
	    4c. Calculate sum of branch lengths connecting foods in each individual’s diet\
	    4d. Divide each individual’s summed branch lengths by the summed branch lengths of the total dendrogram
