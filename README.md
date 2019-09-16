# MitoMot v1.2 Guide

MitoMot is an ImageJ/Fiji macro creaed to analyze Mitochondria Motility. It is still a work in progress so make sure you have the latest possible version. And if you have any doubts, find any bugs or want further information on how I created it, just send me an email at: carnopo@alumni.uv.es.


## Prerequisites:

Before starting to use the tool, you would first have to install the following:

- ImageJ/Fiji (https://imagej.net/Fiji/Downloads)

- Add the IJPB-plugins site to your list of update sites:

   *1. Select Help > Update... from the menu to start the updater.*  
   *2. Click on Manage update sites. This brings up a dialog where you can activate additional update sites.*  
   *3. Activate the IJPB-plugins update site and close the dialog. Now you should see an additional jar file for download.*  
   *4. Click Apply changes and restart ImageJ.*  

- Download the MitoMot macro


## Pipeline:

What this macro basically does is:

- Isolate the chosen cell 

- Subtract Background (Rolling Ball 5 px radius)

- Apply Median Filter (1 px radius) to de-noise

- Apply White TopHat Filter (3 px radius) to isolate bright particles (in our case, the mitochondria)

- Apply again Median Filter (1 px radius) to remove noise introduced by the previous step 

- Binarize by Otsu’s method 

- Subtract consecutive frames to calculate “newcomer” pixels

- Calculate the mitochondrial area in both the normal binarized sequence and the subtracted one  

- Create an overlay with “newcomer” pixels in red  

## User Guide:

1. Start by opening your timelapse in Fiji by dragging & dropping or by    File > Open. It is recommended to open the .czi file format as it contains all the metadata needed, but many other file formats will work too (including .avi). 

   Make sure to select Hyperstack in the “Bio-Formats Import Options” 	dialog box. 

2. Select the cell or area you want to analyze by any of the tools offered  by the Fiji program. After drawing the selection, make sure to go through all the frames and change it accordingly so that it applies to all. 

3. Run MitoMot by going to Plugins > Macros > Run... and choosing the MitoMot file you downloaded.

4. After the macro does its job, this is the windows that will pop up: 

   a) 3 image sequences:  
     i. BIN (Binarized sequence)  
     ii. BIN Sub (Subtraction of consecutive frames from BIN)  
     iii. BIN-ovr (Overlay of BIN Sub over BIN in red)  

   b) 3 result tables (the important descriptor is Total Area):  
     i. Summary of BIN Sub  
     ii. Summary of BIN (used to normalize)  
     iii. Results (descriptors for each individual mitochondria)  

You can then save the the visuals as image sequences (File > Save As > 	Image Sequence...) to save each frame separately or in movie format such as .avi. 

As for the result tables, you can select all the cells with Ctrl + A , copy 	(Ctrl + C) and paste in the data analysis software of your preference 	(Excel, Prism, etc). The important descriptor is Total Area. If all your 	frames are the same size, you don’t need to normalize with total 	mitochondrial area. Also, as the first frame doesn’t have a previous 	frame to subtract you should not include its data in the analysis. 	However, it is useful to check if everything worked out correctly as the 	area for the first frame in both BIN and BIN Sub should be the same.
