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

##### PR : ![#417](https://github.com/camicroscope/caMicroscope/pull/417) , ![#34](https://github.com/camicroscope/SlideLoader/pull/34)


### Week 5 :

This week was a buffer week. Since I had some unmerged PRs , so this week I worked on incorporating review comments and trying to merge them . I made small changes such as the download directory structure and added some comments and cleaned my code a bit. Also I changed the way patches are selected. Earlier the choices given by the user were validated on only the top predicted class of the patch . But that meant that even if some other class passes the user criteria it will not be selected . So now , the choices are validated against all the classes instead of just the top class. 

Also this was the Phase I review week . So this is a screencast showing the work done in Phase I ![Link](https://drive.google.com/file/d/1evU0FrRCvvry1_jFQUDZA4Lhw9bX1m6s/view?usp=sharing)

### Week 6 and 7 :

I got delayed in my work because of an incident that happened to my laptop . Now I know why it is suggested to not use local machine to train ML models ( though I had a NVIDIA 1050 and in the paper it was written that the authors used 1060 Ti) . Anyways that made Week 6 mostly useless but since I had already implemented one model back in April and I had suggested implementing two models in this period , so I just had to complete one more. So I started working on this segmentation model YNet . I ran into some problems with downloading the dataset . But after implementing the model and training , it took me two days to convert it into the tfjs model due to multiple errors in the version compatability of keras , tf and tfjs. I completed the model and have made the PR . Next week will be mostly spent on polishing the model and roi feautures and probably start thinking of integrating the roi branch into the develop branch.

##### PR : ![#3](https://github.com/camicroscope/tfjs-models/pull/3) 


### Week 8 :

This week I made some small changes to roi like adding esc key to get out of roi mode. Other than that I updated the readme of the model and segment apps.Most of the week was spent on trying things out for phase 3. I went through the suggestions I made for phase 3 and found many dead ends. I think I would require discussion on what I should do next.  The thing with Digital Pathlogy is that the datasets are huge which makes training anything even a little complex very power consuming.
One of the ideas I mentioned was training a GAN to generate fake images but that seems hard due to the complexity of the network and the size of the dataset.Also using fake images to train models is not a good idea. It took me a very long time ( and several problems) to even train a simple model like YNet on a relatively small dataset. Also using fake images to train models is not a good idea. Also for generating fake image of a particular type, the model has to be trained everytime with relevant slides of that type.
The other idea of normalizing slides also doesn't make much sense now that I went through the paper thoroughly. Also, caMicroscope already does numerical normalization before its ML tasks, so it is mostly redundant .


