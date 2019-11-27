# slicing-and-saving-model
Code to slice a model and save the slices using HE_Mesh by Frederick Vanhoutte

My needs for this was fairly simple. I needed to cut a model into slices and save them as seperate models.

I needed this so I could use the model in Blender and create contour lines easily for plotting because there is an extention in that program that will provide SVG lines with occlusion.

In processing, exporting a 3D drawing as SVG will gie you ALL the lines, and not just the ones which are visible to the camera.

This code requires the HE_Mesh library which you can find in the processing libraries under 'wblut'. Explore it. There is a lot there.

![six pieces of beethove made with five slices](https://github.com/nosarious/slicing-and-saving-model/blob/master/sliced-beethoven.png)
