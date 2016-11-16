# worldsPlanetGen

* classes.php - this holds the actual functions that make the thing work
* singleStarSystem.php - generate the contents of a star system that has only 1 primary star.  this includes generation of moons, generation of a sample alien artifact if artifacts are present on a given planet or moon, biospheres, and species (but not full stats for them).  biosphere and species generation is still a work in progress
* artifact.php - generates an alien artifact
* data folder - holds the CSVs that are used for data import

## DOCUMENTATION OF FUNCTIONS IN CLASSES.PHP (WORK IN PROGRESS, I'M NOT KNOWN FOR THIS KIND OF THING)
* genStar (takes no parameters) - generates and returns a star formatted as array (string $starType, string $starSize).
* numPlanets ($starType, $starSize, $numStars=1) - determines the number of planets based on the provided parameters and returns it as an integer.  for multi-star systems where the planets orbit a pair (or more) of stars, use the star highest on the appropriate scale for each of $starType (Harvard System extended for additional star types) and $starSize (Yerkes spectral classification system, currently no support for spectral pecularity codes, with white dwarfs flagged as "VII" instead of the more appropriate "D" and subdwarfs flagged as "VI" instead of the more appropriate "sd" (these are on the to-do list)).
* genPlanetZones ($starType, $numPlanets) - generates zone locations for a number of planets ($numPlanets) based on $starType.  returns the data as an array formatted like $array[planetNumber] = (1, 2, or 3).  1 = hot zone, 2 = habitable zone, 3 = cold zone.
* genPlanetType ($zone) - generates the type of planetary body given the specified zone.  returns an integer.  the key for this integer is as follows: 1 = gas giant, 2 = terrestrial, 3 = asteroid belt, 4 = icy
* genRoids(int $modifier) - generates an asteroid belt based on the parameters of the $modifier.  for reference, $modifier should be -4 if there are 3 or more gas giants in the system, or 2 if there are one or fewer gas giants.  returns the data as a string, properly formatted for output.  also generates major asteroids in that belt (if any) and adds them to the output as well.
* genPlanetSize($zone, $type, $moon = FALSE, $planetSize = 1) - generates the planet size based on the input parameters ($moon = TRUE is used to indicate you are generating a moon, in which case $planetSize also needs to be set to the size code for the planetary body it orbits).  returns an array formatted as array (int sizeCode, string fluffText).  fluffText includes diameter of the planet or moon in kilometers.  sizeCode is keyed as follows: 1 = diminutive, 2 = fine, 3 = tiny, 4 = small, 5 = medium, 6 = large, 7 = huge, 8 = small gas giant, 9 = medium gas giant, 10 = huge gas giant, 11 = gargantuan gas giant, 12 = y-class brown dwarf
* genSystemFeatures (takes no parameters) - generates and returns an array of system features, if any.  possible features at this writing include planetary debris disks (such as protoplanetary disks), flare stars,  Oort clouds, status as a raider haven, flux space gateways, and if the system is flux-space capable for ships that cannot go against a gradient.
* genGravity ($size, $type, $moon = FALSE, $planetGrav = FALSE) - generates the gravity of a body based on the input variables.  for moon generation, set $moon = TRUE and $planetGrav equal to the planetary gravity code of the parent body to ensure that a moon does not end up with a higher gravity than its parent body. returns an array formatted as array = (int gravityCode, string fluffText).
* genAtmoDense ($gravity, $zone, $moon = FALSE) - generates the atmospheric density of the body.  $moon should be set to true for moons.  returns an array formatted as array = (int atmoDensityCode, string fluffText)
* genAtmoComp ($zone, $moon = FALSE) - generates the atmospheric compsition of the body.  $moon should be set to true for moons.  returns an array formatted as array = (int atmoCompositionCode, string fluffText)
