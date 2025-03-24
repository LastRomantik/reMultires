# ReMultires
Krpano script for assembling panorama from sliced pieces of multiresolutions

## Install
For the script to work, the path to the folder with krpano installed must be specified in the operating system environment variable.

The script works in two modes: automatic and manual.  
## Automatic mode
Automatic mode is suitable if you have a tour with two or more panoramas that need to be stitched back together into an equidistant view and there is a virtual tour code source file.
To work in this mode it is necessary to prepare the settings file first and after that it is enough to move the folder with the sliced panorama to the script file itself.  
The contents of the settings file:
```
[first line] - value of url parameter of cube or sphere tags  
[second line] - value of multires parameter of cube or sphere tags  
```

Example:  
Original xml code line:  
``` 
<cube url="pano/00-02/%s/l%l/%v/l%l_%s_%v_%h.jpg" multires="1024,1024,2048,3072,4096" />
```

Based on the string, the "settings.txt" file would look like this:  
```
pano/00-02/%s/l%l/%v/l%l_%s_%v_%h.jpg
1024,1024,2048,3072,4096
```

## Manual mode
This mode is suitable for one-time use when you have one panorama or if you don't have access to the xml source with panorama breakdown parameters.  
To start the process move the folder with the sliced panorama to the script file.  
Next, you will need to specify the input parameters of the panorama partitioning:  
* level: maximum level of partitioning.  
    You can find it by looking in the directories named l1, l2, l3, ...  
* size width: the maximum size of the width of the panorama cube side at the maximum level.  
    It can be found out by adding the width of all tiles of one line in the folder with maximal level.  
* size height: the maximum size of the panorama cube side height at the maximum level.  
    It can be found out by adding the height of the tile with the number of slicing lines of the maximum level of partitioning.  
* tile size: tile size (width or height) at the maximum partitioning level.  
    Usually this value is 512 or 1024.  
* url: string with panorama partitioning template.  
    This string points to the panorama side tiles.  
	%s - cube side [b, d, f, l, r, u]  
	%l - maximum level of partitioning [l1, l2, l3, ...].  
	%v - vertical index of the tile  
	%h - horizontal tile index  
    Example: for a panorama where one of the tiles has the path ".\pano1\b\l4\1\l4_b_1_1.jpg", the url string will look like this: "pano1\%s\l%l\%v\l%l_%s_%v_%h.jpg".
