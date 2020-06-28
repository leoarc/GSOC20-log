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


## Week 3 :

This week I worked on expanding the Roi feature so that now users can select a portion of the slide to extract patches instead of the whole slides . This comes in handy when the slide is very large and the user doesn't require patches from the whole slide . This feature is still not fully polished . Also I haven't done much testing so I'll probably come back to this to clean it up . Also as my last PR is still open I added this to it and didn't make a new PR.

##### PR :  ![#410](https://github.com/camicroscope/caMicroscope/pull/410)


### Week 4 :

This week I worked in shifting the extraction process in the model app to the slideloader app. Now there is an option to either do everything completely in the browser or use the slideloader app for the extraction . This solves the issue of tabs crashing and is also much more faster and efficient then using JSZip and creating zip files in the browser. Now , on completing the predictions using  ``` tfjs  ``` in the client side, the results are sent to the slideloader app in  ``` json ``` format . This is used to extract the patces using PIL . The patches are then sent back and downloaded.  This addition makes the ``` roi ``` feature useabe for even large sides!

