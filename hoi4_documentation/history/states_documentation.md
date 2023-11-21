# State Modding Documentation

## Mandatory Arguments
- The entire file should be contained within a "state = { ... }" block, it will not work otherwise.
- These are necessary for the functioning of the game, the state will not work right if any of these are used incorrectly, if at all.

### State ID
- Identifies each state through a number.
- The state ID is shown in a file for each state, here is an example: "id = 1".
- The ID can't be the same number as another state and the IDs have to go from 1 to however many states you have, if there is 
  any gap in the numbers there will be errors.

### State Name
- Determines the name of a state (obviously)
- To name a state you will have to input the line "name = EXAMPLE_NAME_1".
- The name itself actually needs to be named in a localisation file, the localisation file is going to be called state_names_l_english.yml, you will need to make a new file for it. The file location will be in "/Hearts of Iron IV/localisation/english/state_names_l_english.yml".
- The name will be defined in the file like this "EXAMPLE_NAME_1:0 "My Example State Name"".

### Manpower
- Pretty easy concept to grasp, "manpower = 7142834" would show that there are 7,142,834 people living in that state, the game itself will run calculations on the actual in game "manpower" a state has.

### State Category
- Determines the category of the state, which determines the number of building slots the state starts out with at the start of the game and gives each type of category it's own color in the state view map mode.
- The list of state categories and their respective information can be found in "/Hearts of Iron IV/common/state_category".
- Here is an example of how to implement this in your file: "state_category = wasteland".

### Provinces
- Determines what provinces go in what state, because obviously a state can't exist in the game if it is assigned no provinces.
- Here is an example of how to implement this in your file: "provinces = { 1827 7819 6271 162 }"
- Numerical order does not matter but I think it would be useful to put it in some order, the provinces are also seperated by only white space

## Optional Arguments ##
- You likely won't use any of these except for resources, unless you really need or want them in some state somewhere.

### Impassable
- Determines if a state is impassable, if it is troops will not be able to move into any provinces within the state at all.

### Resources 
- Assigns resources to the state, such as steel or chromium
- Here is an example of how to implement this into your code: "resources = { steel = 10 chromium = 621 oil = 4 }".

### Local Supplies
- Determines the base supply of a state, one unit of local supply is 0.2 supply. If this is not defined in the state file it is assumed to be 0.
- Here is an example of how to use it "local_supplies = 10.5".

### Buildings Max Level Factor
- Gives an additional multiplier on the amount of unlocked shared building slots in a state, it is highly recommended that you just use state categories instead of using this.
- To implement this you would need the following line: "buildings_max_level_factor = 0.5".

## History Arguments ##
- These are all within a "history = { ... }" block of code, which can be further specified depending on start date using a YYYY.MM.DD format datestamp inside of the aforementioned history block to tell when things will be different depending on start dates (like buildings).

### Owner
- Determines who owns the state initially, it's fine if left blank but attempting to transfer it to another country will crash the game.
- The code used country tags to give it to countries, here is an example of it's use: "owner = GER", this would give the state to Germany.

### Controller
- Determines the initial controller of the state. This is only needed if the controller differs from the owner.
- An example of how to use this would be "controller = ITA".

### Add Core Of
- Can be used to add cores to the state from various countries.
- To implement it all you need is "add_core_of = GER"

### Add Claim By
- Adds claims to the state from other countries.
- Can be implemented by doing "add_claim_by = ITA"

### Victory Points
- Determines what provinces have victory points, and the number of points they are worth. If you want multiple victory points in a state you will need multiple instances of the code for each individual victory point.
- Each point can be assigned a name in a localisation file called "victory_points_l_english.yml" located in "/Hearts of Iron IV/localisation/english/victory_points_l_english". An example of the localisation is "VICTORY_POINTS_1234:0 My victory point".
- To use this in the code you would do "victory_points = { 1234 15 }", this would give province 1234 a total of 15 victory point value.

### Buildings
- Determines what buildings are in the state, if at all. It's also possible to specify a specific province for provincial buildings to go in too.
- Below this line will be an example of how to implement buildings into your state:

		buildings = {
			dockyard = 3
	 		1234 = {
	 			bunker = 9
	 		}
	 	}
  
- This example would have a state with 3 dockyards and a level 9 bunker on province 1234.
- Buildings can also be different depending on what date they choose to start on, if they choose a different date from the normal history then the game will look for that datestamp in the history section and change whatever is added (or removed) from the state, like adding infrastructure.

## Example State


	state = {

		id = 617 # Germania (not really but still)
		name = STATE_617
		manpower = 7162194
		state_category = megalopolis
		provinces = { 1111 2222 3333 4444 5555 6666 7777 8888 9999 }
		resources = { steel = 10 oil = 182 }
		local_supplies = 18

		history = {
			owner = GER
			add_core_of = GER

			victory_points = { 1111 15 }
			victory_points = { 8888 50 }

			buildings = {
				infrastructure = 4
				industrial_complex = 13
				arms_factory = 5
				6666 = {
					bunker = 10
				}
			}
			2023.2.3 = { # remember that the format is YYYY.MM.DD so it would be the 3rd of February, 2023 in this example
				buildings = {
					infrastructure = 5
				}
			}
		}
	}
