# NCDI Procedure in Detail

This document describes the procedures for calculating the Nutrient Composition Diversity Index (NCDI) using ASA24-2014 and ASA24-2016 data.  Similar procedures can be used for other detailed dietary intake data by adapting the sample code.  Refer to the [README](/README.md) for an overview of the procedure and required resources.

Files from the USDA FFNDS and SR databases are needed to run the following steps.  Please confirm that you have downloaded and extracted the files listed above under [README: USDA Food Composition Databases](/README.md#usda-food-composition-databases) before proceeding.  All Stata sample code below assumes these files are already converted to .dta format.

## Step 1: Create Nutrient Trait Matrix
### Step 1.1: Disaggregate mixed food items in the FNDDS food composition table to their ingredients using SR recipes data
In Step 1.1, the source files for the nutrient trait matrix are reshaped and mixed foods are disaggregated into individual ingredients.\
\
\
**1.1.1:** Transpose the SR23 food composition data file (nut_data) from long to wide.

See sample code FL100_FNDDS2012_IngredientNutrients_20240505.do.

Note that for this sample code, the SR23 nut_data file was renamed srnutval and the output file is named FNDDS2012_ingnutrval. The output file should contain one row per food, with columns corresponding to the nutrients reported in the SR food composition data and cells containing the nutrient composition values for each food.  At this point, the expression of nutrient composition values on a per 100g of food basis is retained.\
\
\
**1.1.2:** Disaggregate mixed food items in the FNDDS 2011-2012 foods list (mainfooddesc) using SR recipes data (fnddssrlinks) and merge the nutrient values table from Step 1.1.1 (named FNDDS2012_ingnutrval in sample code).

See sample code FL100_FNDDS2012_Ingredientizer_20240506.do.

The output file (FNDDS2012_ingredientizednutrval in sample code) should contain all FNDDS items broken down to individual foods or ingredients from the SR food composition database, with nutrient composition data for each ingredient.  Because some mixed dishes in FNDDS contain sub-recipes, multiple iterations are required to disaggregate the mixed dish recipes down to the level of individual foods.  For FNDDS 2011-2012, four iterations are required.  For other versions, more or fewer iterations may be needed.
<br/>
<br/>   
   
### Step 1.2: Repeat for all versions of FNDDS used
Repeat Steps 1.1.1 and 1.1.2 using the SR22 and FNDDS 4.1 data files.  See sample code FL100_FNDDS4_IngredientNutrients_20240505.do and FL100_FNDDS4_Ingredientizer_20240510.do.
<br/>
<br/>

### Step 1.3: Append the disaggregated food composition tables into a single nutrient trait matrix
Append the disaggregated food composition tables from FNDDS 2011-2012 (SR23) and FNDDS 4.1 (SR22) into a single nutrient trait matrix and clean the data as follows.  
  - Remove duplicate foods or ingredients from each FNDDS version.
  - Create variables marking the version for each unique food or ingredient.  (Note: some foods or ingredients remain unchanged across FNDDS versions, while nutrient composition values for some foods or ingredients are updated.  In both of these cases, the record from both versions is retained.)
  - Drop items that occur in the SR tables but not in the FNDDS tables and items with missing nutrient composition data.
  - Delete columns for nutrients that will not be used in the NCDI calculation.
  - Mean-standardize values for all nutrients that will be used in the NCDI calculation.

    
See sample code FL100_FoodSystemDendrogram_20240521.do.



## Step 2: Calculate Distance Matrix



