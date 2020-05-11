---
toc: true
layout: post
description: Lesson 2 notes from fastai course.
categories: [markdown]
title: Building an image classifier
---

## DataBlock api
- container which build datasets and dataloaders
- expects to have 4 items passed as an positional parameters : 
    - blocks (type of data)
    - get_items
    - splitter
    - get_y
    - item_tfms

- once DataBlock object is created, we can call dataloaders on each path.



## Useful methods or class used in the lesson 2 
- search_images_bing : 
- TransformBlock : A basic wrapper that links default transforms for datablock api. 
<newline>    TransformBlock(type_tfms=None,item_tfms=None,batch_tfms=None,dl_type=None,dls_kwargs=None)
- ImageBlock  : TransformBlock` for images of `cls = PILImage' 
- CategoryBlock : TransformBlock` for single-label categorical targets
- DataBlock : Generic Contrainer to build Datasets and DataLoaders
<newline> DataBlock(blocks=None, dl_type=None, getters=None, n_inp=None, item_tfms=None, batch_tfms=None, get_items=None, splitter=None, get_y=None, get_x=None)
- DataBlock has dataloaders class, dls.items = gives list of all elements.
- aug_transforms : utility functions to create flip, zoom, rotate transforms.
- ClassificationInterpretation : Sub-class of Interpretation, used for interpretation of classification models.
- ImageClassifierCleaner : picks the one which the model is least confident about.

Open Questions 
1. What was the reason behind creation of class L . If it is only behaving like list of items.

2. how many augmented images are created by function batch_tfms=aug_transforms. 

3. After randomly splitting dev and train set. I did ImageClassifierCleaner on my cnn_learner and validation set had a white bear marked as black.
   My question is we need to clean, validation set as well ? Although we are not training our model on validation set but since loss is computed on validation set. How big will be the impact if we don't curate our validation set correctly. 

## Different resizing of images and data augmentation
1. default is cropping and center of the image.
2. Squish gives more detail
3. RandomResizedCrop different part of image are zoomed. basically squished in different ways.
4. aug_transform returns list of different augmentation. This are batch_tfms and happens on gpu. Fastai enables to run this on gpu.
