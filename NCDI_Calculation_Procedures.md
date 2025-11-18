

# NCDI Procedure in Detail
Files from the USDA FFNDS and SR databases are needed to run the following steps.  Please confirm that you have downloaded and extracted the files listed above under [USDA Food Composition Databases](/README.md#usda-food-composition-databases) before proceeding.  All Stata sample code below assumes these files are already converted to .dta format.

## Step 1: Create Nutrient Trait Matrix
### Step 1.1: Disaggregate mixed food items in the FNDDS food composition table to their ingredients using SR recipes data
1.1.1: Transpose the SR food composition data file (nut_data) from long to wide.  See sample code FL100_FNDDS2012_IngredientNutrients_20240505.do.  Note that for this sample code, the SR23 nut_data file was renamed srnutval.
1.1.2:

