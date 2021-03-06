
## Roadmap
Initially, a test object array is hard-coded into a file, but will need to be able to import a csv, json or text file to be of any use.<br /><br />

Refresh browser window to re-align dots - until a non-overlapping system is deployed. The 1px black stroke helps identify partially hidden dots and all of them are able to display their information when hovered over.<br /><br />

Legend added:<br />
    It can be moved down if you don't want it covering the radar:<br />
            #legend-wrapper	top:40em;  sits nicely below the radar.<br />
    Adding / changing Legend text:<br />
        .show-legend -	height is set to 33em - change that for another fixed height.<br />
        Or you can set it to auto - but then you lose the nice transition effect.<br />
        Or you can add a scrollbar:<br />
	        change #legend - overflow-y:auto;<br />
	        but then it doesn't look as neat - depends on your colour scheme. It's still not easy to change scrollbars          across all the browsers...(was in IE6!).<br />
    IE9 doesn't have the transition effect.<br /><br />
    
    
### Updated 3-7-17:<br />
Main container file renamed to .html from .shtml - so it can render properly without the need for a virtual server offline. This file contains the content components: The SVG radar, the legend etc.<br />
The css and js files are still separate from the main content.<br /> <br />

### Updated 2-7-17:<br />
Files split into folders for css, js and other, mainly txt includes. So the main .shtml file is the vehicle to contain everything else.<br />
    
### 7-7-2017 <br />
Added list representation tables for sectors.<br />
Added a table, on the right, for anomalies in the input data - to catch unallocated category/sectors and unallocated statii (? status's) - which can not appear on the radar with this info missing:<br />
A way to check errors in the input data and also add technologies to be assigned later.<br />
Tidied up and consolidated code a bit.<br />
Renamed a few files to better reflect their contents.<br />
Created some 'anomalies' in the test input data to show how it works.<br />

### 15-7-2017 <br />
Added functionality to add / remove / rename sectors. <br />
Sectors will be created dynamically on whatever category fields are entered into the input data source. Sectors are recalculated equally, the List Representation dropdown menu and tables are also updated. <br />
As before, the dots do jump out of their sectors into the neighbouring sector by a small margin - this needs to be fixed!!<br />
Because the dropdown category menu can't be a fixed height now, it's lost it's glide movement, and so will just appear when clicked on - can't seem to keep this property without having a fixed height.<br />

### 23-7-17 <br />
Added tables for Status, similar to the Sector tables.<br />
Changes to the Anomaly table to hide it when not needed.<br />
Changes to scripts and data input layouts. Separate file (status_config.js) added for easy configuration of titles, radiuses and legend text:<br />
Status names can now be easily added, deleted or changed - and the radiuses of each group can be easily changed. The titles, dots, tables, legend etc. automatically update with any changes.<br /><br />

### 26-7-17 <br />
Accepts a JSON file as input data.<br />
The test JSON file - 'data.json' - is in the main directory, and simply needs to be replaced with your own data - and named 'data.json'.<br />
To accept a file in another location and/or of different name - the file path at the top of 'js/input_data.js' will need to be edited.<br />

There is a neat little JSON validator here:<br />
https://jsonlint.com  <br />

### 27-7-17 <br />
A few adjustments so that features can be just deleted from the main html page if not wanted: <br />
for anomaly chart, <br />
pop-up details box, <br />
sector table, <br />
status table. <br />

### 28-7-17 <br />
Fixed the maths for the sector angles. <br />

### 31-7-17 <br />
Changed design to go with a white background. <br />
Changed code around to eliminate some globals. <br />

### 18-11-17 <br />
New features added: <br />

1. Subcategories : <br />
	Added new column SUBCAT next to CAT. on JSON input data file. <br />
	On the test data file there are 3 subcategories:   <br />
	   Mobile, Cloud, Client-Side - but I've allowed for up to 6.  <br />
	If no subcat is entered the dots don't show in subcat view.   <br />
	The names can be changed/added to/deleted via the subcat_config file.  <br />
	If the subcats aren't recorded on the subcat_config file, they appear in the anomaly list as 'Unallocated Subcategory'.   <br />
	(The test data has one listed as 'X' and one as blank to show this.)  <br />
	The view mode can be changed via a new drop-down menu - Radar View Mode.   <br />
	New subcats entered on the subcat_config file will also show up on this menu.	I've chosen the colors to contrast with the classic colors. They can be changed on the radar.css file (.dot-sub1 etc) - color names instead of hex values are fine.  <br />

2. Dots now have directional arrows:  <br />
  Added column DIRECTION next to the STATUS column, in which the values can be entered manually when status is manually changed.  <br />
		Arrow length = velocity: <br />
		Values -n to +n: <br />
		-n for outgoing techs.  <br />
		+n for incoming techs.  <br />
		Any values accepted (values expected are -6 to +6).  <br />
		Use larger values for longer arrows.  <br />
		Can also leave blank.  <br />
		Leaving blank or 0 = no arrow, just dot.  <br />

3. List tables are now draggable.  <br />
	Onclick/double-click - to bring to front:  <br />
	The layer position is based on z-index (click = +1)  <br />
	The new subcategories are on all 3 tables.  <br />

Notes on persisting data between file loads/screen refreshes:  <br />
There doesn't seem to be a way to write to a file with JS - so I think the best ways to persist data are:  <br />
1. One or two more simple changes when the input data is altered by the user - as implemented in this version.  <br />
2. Local storage  <br />
Is there a better solution I'm not seeing?  <br />

Use of 'Local Storage': <br />

Pros:  <br />
1. Subcats can be changed/deleted/added dynamically just by changing the subcat on the data input file - removing the need for the subcat_config file.  <br />
2. Directional arrows can also dynamically update - removing the need for the DIRECTION column in the data input file. <br />

Cons:  <br />
1. This will take control away from the user and the program.  <br />
2. Portability is lost - browsers might be changed, caches might be cleared - it is no longer self-contained.  <br />

The subcat_config file is likely to be only needed on first set-up (to change Mobile, Cloud and Desktop to different names or add/delete subcats) - and to make the odd changes.  <br />

The subcats did work very well without the subcat_config file, using dynamic keys linked to the subcat names - except that when new data gets added to the list the color keys change around depending on the order of the subcats on the input data. Asking the user to add the subcats in the same order every time doesn't seem acceptable - unless they group their data in this way anyway, then it will work. <br />

### 11-1-18 <br />

Eliminated detached DOM objects
Fixed some memory leaks
Fixed Console warnings
Put in strict mode

### 12-1-18 <br />
Condensed the 3 x list table css files into one file.

### 14-1-18 <br />
More code changes.

### 23-2-18 <br />
Renamed security-radar to: radar.html <br />
Updated some code.  <br />

JSON import fixes:  <br />

If the radar doesn't appear in the browser and/or you get a console warning similar to: <br />
    XMLHttpRequest cannot load  file:///...Cross origin requests are only supported for HTTP
(FireFox lets it still work (with a console error warning) - but not the other browsers.) <br />
Try:

Solution1:  <br />

(Mac OSX):  <br />
Use one of the simple servers that's probably already built in: <br />
Open a terminal and cd to the directory containing your radar.html <br />
Type: python -m SimpleHTTPServer <br />
or: <br />
Type: php -S localhost:8000 (or 8001, or another port not in use) <br />
In the browser address bar type: http://localhost:8000/radar.html (or whatever port was specified). <br />
Then it should work fine. <br />
(Ctrl C exits the server.) <br />
or a Node or Apache server etc. <br />

A similar solution may available with Windows. <br />
or:

Solution2:  <br />

Convert/copy the data.json file to a js object file - data.js - and add: <br /> 
  const techList =  <br />
before the first opening bracket \[... <br />
data.json will be used if the data isn't in data.js.

### 19-5-19 <br />
Code rewrite. <br />
More ES6. <br />
Used npm, webpack and babel - axios to get the data - cssnano to minify and autoprefixer to add vendor prefixes to the dist css. <br />
Improved transitions - the mode and anomaly tables are draggable now as well. <br />
A max-height of 500px and scrollbar have been added to the anomaly table - not sure if this is preferred, so I've only added it to this table. It can be changed in:
**anomaly_table.css** :
```.anomalies-show {max-height: 50rem;} ``` (1rem = 10px here).

### 21-5-19 <br />
A few small code improvements: <br />
 - changed line 30 of **index.js** to a simple map() fn.  <br />
 - removed unneeded function and simplified line 7 from **formatData.js**.  <br />
 - big improvement on repositioning dots when clicked on - changes to **index.js, radar.js and radarView.js**. <br />
 - changes to error message appearance in **main.css**. <br />
 - streamlined code for the svg eventListeners at the bottom of **index.js**. - No need for **detailsPopup.js** - using ```find()``` to go direct to render page. <br />
 ```find()``` works well here. To compare, ```filter()``` worked out well for the eventListener above. <br />
 ```console.log``` them (```console.log(selected);```) to see the difference. <br />
 
 ### 25-5-19 <br />
 Added the ability to change sector sizes - all equal or weighted to data - buttons in the **Rada View Mode** chart. <br />
  - Clicking on the same button also rearranges the dots without having to refresh the screen. <br />
  - The transitions aren't good in Safari or FF - poss. because initial positions aren't set in the css - not sure...will look into.. <br />
  
Renamed some variables in radar and radarView to make them clearer. <br />
Made randomPosition calc clearer and fixed the issue with the center circle dots going out of their range. <br />
Changes to **radar.js, radarView.js, index.js, modeTableView.js, radar.css, anomaly_table.css, mode_table.css.** <br />
  
 ### 27-5-19 <br />
 Added the ability to click and drag the radii. <br />
  - A cicle is resizable when it's outer edge lights up blue. <br />
  - The dots will automatically reposition. <br />
  - Maximum limits have been set so they don't overlap when resizing outwards - but not minimum limits, so use your new powers wisely! <br />
  - The main changes are in **radar.js**, **radarView.js** and **index.js**. <br />
  
 Also tidied up the eventListeners on **index.js** and made small changes in **formatData.js** and **radar.css**. <br />
 
 ### 28-5-19 <br />
 Fixed the arc calculation in **radar.js** ```calcSectors``` that was making the sector titles go off course when in unequal sector mode - by removing the 3px offset from here and adding it as: ```textElement.setAttribute("dy", "-3");``` to ```renderSectors``` in **radarView.js**. 
 
 ### 29-5-19 <br />
 Fixed arc calculation in **radar.js** - wasn't taking reflex angles into consideration.
 
 ### 1-6-19 <br />
 Changed the radar's subcategory mode so that the subcategories become the sectors, instead of just changing colour. <br />
   - I've kept them the same subcat colours to differentiate which mode it's in easier. <br />
   - Where there is no cat (or subcat in the subcat mode), the dots will still appear as 'ghosts' - translucently. This is easy to switch off if annoying - see Configure in README. <br />
   
The weighted sectors on the radar took into account the entire dataset, including any unallocated sector entries - I've fixed this to just represent all data with sectors. So ```360 deg / data count for each sector```.<br />
Also some refactoring and removed a function not needed anymore for changing the colors. <br />
Main changes are to **radar.js**, **radarView.js**, and **modeTable.js**, with smaller changes to other .js and .css files. <br />

### 2-6-19 <br />
Refactored the tables code and moved the tableList to be created with the anomalyList data so the anomalies are set in one place. <br />

Added a binary search - to lookup dot details - which may help with large datasets - and shouldn’t slow down small data sets. Anyway, the sort function needed for it is nice to have for keeping the table data in alphabetical order. <br />

Added some errorhandling in a few places - for the less expected data sets. <br />

Changes are to **listTables.js, listTableView.js, anomalyTable.js, index.js, formatData.js, LoadData.js. radar.js, modeTable.js** (removed fn reference), **details_box.css** (capitalize text not needed) and **search.js** added. 

### 5-6-19 <br />
Refactored code for tables. Changes to **listTables.js** and **index.js**.
