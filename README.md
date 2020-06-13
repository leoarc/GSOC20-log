# GSOC-20-log
Weekly log of GSoC'20 work done under caMicroscope

## Week 1 :
In the first week I worked on implementing the ```Region Of Interest``` (roi) extraction feature  inside the model app. The idea is to let user choose a models from the uploaded ones and apply it to a whole slide at once and download the patches based on the criteria given by the user. For starting , the options include the class of the patch , a threshold accuracy value and scaling options. Most of the things required were already present . My work was to integrate the features into one and make that into the roi feature. So I didn't face any issue in this week . Also , this implemetation is completely in the frontend. So, with larger slides the browser is running out of memory and the tab is crashing . Even for the small the slides the memory used is very high . For example for 1.9 MB slide , and zipping files of 8.6 MB the memory being used is over 80 MB .

So, either we have to look into why so much memory is being used and fix it or else we have to move some of the functions to the backend.

##### PR : ![#408](https://github.com/camicroscope/caMicroscope/pull/408)


## Week 2 :

This week I worked mostly replicatinf the ``` roi ``` feature for the segment app . The memory concern for segment is even higher as int the model app the only thing which was stored for the entire process was the labels which were classes. But for the segment app the labels i.e the mask data has to be stored which is much higher. For example for the same slide from week 1 the memory being used for extracting roi in segment app is over 310 MB. 

With this week an initial implementation of ```roi ``` is completed in the model and segment apps. These will serve as a base to work on them further and improve them.

##### PR : ![#410](https://github.com/camicroscope/caMicroscope/pull/410)
