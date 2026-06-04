# TC_watches_warnings


The purpose of this project is to produce a map with highlighted states and/or countries of tropical storm and/or hurricane watches and/or warnings that have been issued for a specific storm given a 
specific year from 1987-2022, which will be dependent on user input; user input will be asked upon running the code. User input must be correct otherwise the code will prompt the user to input a 
correct year. If a string is input instead of an integer, an error exception will occur and prompt the user to input a valid integer within the given year. After the year is properly input, the code 
will also prompt the user to input a name that was used during the user specified year. Maps will be inclusive of the continental United States, Mexico, Central America and will also try to encompass 
Caribbean Islands that received watches or warnings. Also, it must be noted that ONLY the maximum (worst) warning to be issued for an area will be shown (i.e. if Florida is put under a tropical storm 
warning but then later is put under a hurricane warning, the hurricane warning will take precedent and will be shown over the tropical storm warning that was issued for that state). Once the user 
inputs a proper year and name, the code will then execute and output a map as states before with certain states, islands, and countries being highlighted given its respective watch or warning. The 
following colours are to be displayed for their respective advisories: a yellow highlight indicates that the worst advisory issued for a region was a tropical storm watch; a blue highlight indicates 
that the worst advisory issued for a region was a tropical storm warning; a pink highlight indicates that the worst advisory issued for a region was a hurricane watch (hurricane watch will take 
precedence over a tropical storm warning as it is assumed a hurricane watch also warrants a tropical storm warning); a red highlight indicates that the worst advisory issued for a region was a 
hurricane warning.

Certain parts of the code were challenging to get a 100% right. Even still, I am sure there are bugs in the code that I have not yet found or accounted for, though, even after the project is 
submitted, I plan on finding them and fixing them appropriately. I would say the most difficult part of coding this project was trying to import the correct libraries so that I could plot the 
states/islands/countries that needed to be highlighted. Furthermore, it was difficult to figure out how to properly find the geometries of these regions and plot them adequately on a map. Originally, 
I wanted to be able to just plot lines along the coasts of the land masses, and more specifically, from certain latitudes and longitudes that were included on certain watch or warning advisories, but 
I had to abort that portion of the project due to time constraints and resorted to just highlighting an entire state/island/country. This was disappointing, of course, however, figuring out how to 
highlight an entire region was rewarding in itself. Another part of this project that I found particularly difficult was simply just figuring out what information I needed and how to access it from 
the text files provided by NOAA. Though coding for-loops or while-loops was not that difficult, the logic behind certainly gave me a run for my money. In order to help myself with debugging or run-
time errors, I created a method called test_print() that takes a list as a parameter and iterates through the list, printing out each index followed by a series of dashes that would print out on a 
singular line to indicate separations in indices. I also had issues with splitting and accessing certain parts of data, but I just usually have issues with strings as they are not my strong suit, 
which brings me to my next issue. I found it quite difficult to code when if-statements are oriented to strings. In other words, I found it difficult to do what I wanted to do when using, for example, 
for [variable] in [list], especially when it came to deleting indices. I fixed this by creating while loops that kept track of a counter that would access each index of the list by invoking list[i], 
where i is the counter and list is an arbitrary list that is being traversed through. By coding my project this way, I found it easier to remove indices from lists.

This project interests me because I have always been interested and even fascinated by tropical cyclones. It’s the weather phenomena that got me interested in meteorology and it’s certainly a 
phenomenon that I am unfortunately all too familiar with. In 2005, I was visiting my Godmother in New Orleans. My mother and I were there during August and had to cut our vacation short as they 
started recommending evacuations for the city. In 2011 and 2012, Tropical Cyclones Irene and Sandy took aim for the Northeast, affecting not only me, but everyone in the Northeast. However, 
experiencing intense storms such as these for the first time first hand put me in awe both times. In 2017, I tracked Hurricane Maria all the way from its beginnings as a tropical wave all the way to 
its dissipation. In fact, as I was tracking it, I was able to warn my family in Puerto Rico about a possible direct hit days before the National Hurricane Center issued its initial advisories for the 
islands. Even in 2020, New Jersey had to direct hits from Tropical Storm Fay and Tropical Storm Isaias which allowed me to further my first hand experiences of intense tropical cyclones. Being able to 
look back at the history of advisories issued for tropical cyclones is not only extremely beneficial, especially when trying to conduct analyses for past storms, but pretty inspiring and amazing as 
well. I hope you enjoy this project and its purpose as much as me.

# Code explanation
**How the program works:** The program works by taking 2 user inputs, year and name, and checks the validity of the user inputs. From there, it calls a method, find_name(), that will traverse through 
text files that would be accessed on the spot looking for the inputted name for the given year. There are 5 text files the code must search through, resulting in two end cases: one being a return 
statement that returns the text file the name was first found in, the other being a printed statement telling the user that the name was not found. This leads to the code prompting the user to input a 
valid name that was used during the user specified year and will go through the process of searching for the name through the 5 text files associated with the specified year. If a text file containing 
the name is found and returned. The code will then make all characters in the file uppercase so that identifying parts of the string the code will need will be easier. The code then splits the text 
file into a list called wx_statements. From there, a for loop is used to append every line that contains the specified name into a new list called storm_advisories. This list should be a list of 
strings (sentences) that contain the storm name inputted by the user. From there, a different method, access_advisory(), is called, which will remove every index from the list that does not contain 
certain keywords that helps narrow down the amount of data the computer must search through to look for land masses that were issued a watch or warning. It returns a list that will be a modified 
version of storm_advisories; this list now only includes advisories issued for the specified storm. If there were no watches or warnings associated with the storm, a printed statement will be 
outputted, telling the user that there were no watches or warnings associated with the specific storm. The code then enters a for-loop for which the advisories in the storm_advisotries list get 
categorized into respective lists of ts_watch_places, ts_warn_places, hurr_watch_places, and hurr_warn_places. This for-loop puts the issued advisories into their proper respective lists by using 
keyphrases which helps determine which advisory should go into a specific list. After this, the code enters a while-loop which then calls a method, obtain_regions(), which takes a list as a parameter 
and compares names of states, islands, and countries from list_land to each word in a sentence, which is what is contained in each index of the list that was the parameter. If a match is found between 
a string in list_land and a word from a sentence from the list, the name of the state, country, or island is appended to a temporary list, temp, which is returned after the method finishes iterating 
through the list which was the parameter of the method. This method is called four times, once for each list of watches or warnings. Lastly, the code enters a while-loop that attempts to remove places 
that might have been appended multiple times for a specific watch or warning. This is to reduce the runtime of the code when the code creates and plots the information on a map, which brings us to the 
final part of the program. After multiplicities of places have been removed from the lists, the code then creates geometries/shapes for each state, country, and island that was interpreted to have a 
watch or warning. It goes through each list and accesses the land in the list then creates a geometry for it to be plotted. It stores the information created by the geometries by appending the 
geometries to four separate lists for tropical storm watches and warnings and hurricane watches and warnings. From there, the code then creates a map and adds the geometries appended into the four 
lists onto the graph for each of the possible advisories. It does it in the form of tropical storm watch, then tropical storm warning, then hurricane watch, then hurricane warning. This is to ensure 
that the ‘worst’ advisory takes precedence; it accounts for state, countries, or islands that were issued different advisories for the same storm. After everything is added to the map, the map is then 
outputted and displayed to the user.
