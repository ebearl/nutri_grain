Phase 1 Requirements. These requirements are for phase 1 but we can continue forward if they are completed in a short amount of time. The requirements at the top are more critical and should be completed first.

Example of how to mark something off and create task lines:
-------------------------------------------------------------
- [ ] something to do
- [x] something is completed
  - [ ] an incomplete subtask
  - [x] a completed subtask

Food Database Multiple Concurrent API Requests
-------------------------------------------------------------
- [ ] Requirement DB001: Use retrieve within the CRUD operations through API calls to access food through various databases.
  -USDA Food Search endpoint example: https://api.nal.usda.gov/fdc/v1/search?api_key=MY_API_KEY
    -Request parameters: api_key, generalSearchInput, includeDataTypeList, ingredients, brandOwner
  -USDA Food Detail endpoint example: https://api.nal.usda.gov/fdc/v1/######?api_key=MY_API_KEY (# is the id of the food search unique id)
    -Request parameters: api_key, FoodData Central ID (the output for this search will return a lot of data and the data that are crit. We will need to determine what we want (https://fdc.nal.usda.gov/portal-data/external/dataDictionary)
  -ESHA Food Search endpoint example: https://www.esha.com/products/nutrition-database-api/ (that's all the info I have without talking to them).
  -EDAMAM Food Search endpoint example: https://api.edamam.com/api/food-database/parser?ingr=red%20apple&app_id={your app_id}&app_key={your app_key} (parser without NLP food logging), https://api.edamam.com/api/food-database/parser?nutrition-type=logging&ingr=red%20apple&app_id={your app_id}&app_key={your app_key} (parser with NLP food logging), https://api.edamam.com/api/food-database/nutrients (nutrient data requests)
    -Request parameters: there are many
    
  - [ ] Requirement DB001.1: Ability to search for commercially sold meals, homemade meals, or individual ingredients (this is dependent on the API endpoint).
  
  - [ ] Requirement DB001.2: Response should display critical pieces of information important to the user:
    - [ ] Response displays Database Title (crit)
    - [ ] Response displays Food Name (crit)
    - [ ] Response displays Food Description (optional? this is useful for homemade meals)
    - [ ] Response displays Calorie Total (crit)
    - [ ] Response displays Total Fat (crit)
    - [ ] Response displays Total Saturated Fat
    - [ ] Response displays Total Polyunsaturated Fat
    - [ ] Response displays Total Monosaturated
    - [ ] Response displays Total Transfat
    - [ ] Response displays Cholesterol
    - [ ] Response displays Sodium
    - [ ] Response displays Potassium
    - [ ] Response displays Total Carbs (crit)
    - [ ] Response displays Dietary Fiber
    - [ ] Response displays Sugars
    - [ ] Response displays Protein (crit)
    - [ ] Response displays Vitamin A
    - [ ] Response displays Vitamin C
    - [ ] Response displays Calcium
    - [ ] Response displays Iron
    - [ ] Response displays Default Serving Quantity (crit)
    - [ ] Response displays Default Unit of Measurement (crit)
    - [ ] Response displays Default Measurement Quantity (crit)
    - [ ] Response displays Health Label(s) (crit)
 
- [ ] Requirement DB002: Ability to save the food search API responses to the NutriGains internal database.
 
  - [ ] Requirement DB002.1: Save/store the food search output to the internal database if the responses are unique among the responses AND are unique to the internal NutriGains database. The onSave event will happen after the user selects the unique response and saves it to their daily diary meal input. A check will be run to determine if the food output is unique among the other outputs. A check will be run after the user has saved the response to their daily diary meal input to determine if the response is unique to the internal NutriGains database.
  
  - [ ] Requirement DB002.2: Update the database title to NutriGains when the second check has been run.
 
- [ ] Requirement DB003: Ability to display API response in a list view.
 
  - [ ] Requirement DB003.1: If the responses are not unique concatenate the database titles into one title.
  
  - [ ] Requirement DB003.2: API response sort order descedending: from internal database, is unique output, is non-unique output.
  
*Note: when a user saves the response to their diary and then manipulates the servings size or saves the ingredients as a meal it is not saved to the internal NutriGains database, but it is saved in a place where they can still access the data so that it can be copied and used repetitively in future food diary entries.*


Search the Map API Requests
-------------------------------------------------------------
- [ ] Requirement LS001: Ability to request and get the user's geolocation.

- [ ] Requirement MS001: Use a map service API like Google maps that allows the user to search for food outlets, display them on a map, then get directions to the choice.

- [ ] Requirement MS002: Ability to search the map based on ad-hoc search parameters.

  - [ ] Requirement MS002.1: Search by distance (mandatory) - radius defined in miles or kilometers to display the nearest food outlets. This will be a range input for min/max values that looks like a spectrum (linear input). The default range will be 0-10 miles or kilometers depending on user two-choice option for metric or imperial. This is a mandatory parameter and if no selection is made it will default to the 0-10 range.
  
  - [ ] Requirement MS002.2: ood outlet type (optional) - this will be a multi-select option set that will display the different types of food outlet types. This will include classes such as but not limited to: 
    -Food mart class
      -Grocery store class
      -Supermarket class
      -Hypermarket class
    -Restaurant class
      -Fast food chain class
      -Cafe class
      -Cafeteria class
      -Food hall/food court class
      -Specialty restaurant class
      -Grill room and rotisserie class
      -Bar class
      -Public house class
      -Discotheque/lounge class
      -Casual dining class
      -Functions restaurant class
      -Fine dining class
      -Buffet class
    -Special interest class
      -Food truck class
      -Hole in the wall class
      -Pop-up class
    -Other class

----*this should be the cutoff for phase 1.*
 
- [ ] Requirement MS003: Ability to search the map based on user-profile-derived paramters.

  - [ ] Requirement MS002.2: Cuising Type (optional) - a multi-select option set that will display types of cuisines. These options will be affected by the the diet input from the profile page. The options will look like “Italian” or “Asian”. Asian can have subsets like “Chinese” or “Japanese”.
  
  - [ ] Requirement MS002.3: Diet (system) - this will be boolean options that are derived from the user’s profile page. If the user chooses specific options such as “Kosher” or “Hallal” or “Vegan” or “Food Allergan (of type <<subset>>)” then the list of options within the cuisine type search criteria and food outlet type criteria will dictated by these settings. The diets that are derived from the user profile are read-only fields that cannot be changed on map search and can only be changed on the user profile page, however if the user wants to add in more diets for the search then it will only alter the search and not the user profile.

  - [ ] Requirement MS002.4: Keyword search (optional) - a string search that can represent any of the other search criteria. The keyword may also represent the names of restaurants, name of food, new to market search, is open?, <<keyword search might expand>>. Examples below:
“Within 15 miles” “47” “twenty two” “seventy 1” “between 5-20 miles” (distance)
“Grocery store” “Food truck” (food outlet type)
“Peanut allergy” “Caveman” “Vegetarian” (diet)
“McDonald’s” “Poppadeux” “The Ragin’ Cajun” (name of restaurant)
“Cheeseburger” “Sushi” “Continental breakfast” (name of food/meal)
“New” “Just opened” “3 days old” (new to market)
“Is open” “Is closed” “opening in 2 hours” “closing in 30 minutes” (is open?)


