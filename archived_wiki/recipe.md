---
layout: bootstrap
---
`Archived Contents from the original OpenAg Wiki`

# Climate Recipes
While plants can be altered genetically to produce different or more desirable traits, plants with the same genetics 
may naturally vary in color, size, texture growth rate, yield, flavor, and nutrient density depending on the 
environmental conditions in which they are grown.

In Food Computers, a set of environmental variables that could affect the plant (e.g. the pH and nutrients in the 
water, the temperature and humidity, the intensity and timing of the lights) is packaged up with small scripts of 
code to maintain a very specific climate inside the growth chamber. This data packet of conditions are what we call 
“Climate Recipes.”

Users create, download and run Climate Recipes to produce unique phenotypic results in plants. The data collected 
during their growth cycle is recorded and filed in an open-source digital library called the [Open Phenome](https://web.archive.org/web/20190720114223/https://www.media.mit.edu/projects/open-phenome-project/overview/).

With Climate Recipes, Food Computers, and the Open Phenome, nerdfarmers can join together in a citizen science 
experiment to cross link environmental, biologic, genetic variables and other cultivation inputs to phenotypic 
outputs in plants (like nutrition, color, flavor), then share, borrow, scale up, and improve their results 
around the world, instantly.

# How they work
Examples of recipes we use at MIT OpenAg for test and research.

#What they look like
```json
{
   "_id": "long_test_recipe",
   "format": "simple",
   "operations": [
       [
           0,
           "air_temperature",
           25
       ],
       [
           3600,
           "air_temperature",
           26
       ]
   ]
}
```

# Test Recipes
[Repository of Recipes(Github)](https://github.com/OpenAgricultureFoundation/openag_recipe_bag)