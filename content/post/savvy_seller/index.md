---
categories:
- Computer Vision
- Object Detection
date: "2019-10-01"
diagram: true
image:
  caption: 'Algorithm flowchart'
  placement: 1
math: true
title: Predicting Sale Price Using Images
tags:
- Computer Vision
- Object Detection
---

I am a fashion lover and environmentalist at heart. Buying and selling pre-loved clothes is a great way to reduce our carbon footprint yet still manage to stay hip and look good. Clothing resale is a 28 million dollars market and will reach 51 billion dollars in the next five years. Online marketplaces such as Etsy and Poshmark provide an easy way for people to sell and buy clothes.  Usually, at those online marketplaces, to sell, users simply upload a photo, enter the brand name, and enter an asking price. But it can hard for users to know how much their items are actually worth, and these websites do not provide price suggestions.

In this post, I develop an app, Savvy Seller, to **predict clothing sale prices based on a photo and brand name of an item**. The goal is to help clothing resellers better price their items to improve sale performance at online marketplaces. Savvy Seller requires only a photo of the sale item and its brand name from users’ end, but increased price prediction accuracy by 30% comparing with traditional models.


### Steps

1.Use AWS to scrape daily sale histories from online clothing resale marketplaces. Each sale history includes photos of the item, brand name, as well as final sale prices.

2.Use VGG16 image classifier to find similiar looking items. Top layer of VGG16 was choppd off, this will skip the final classification step. All images were converted to vectors through VGG16. When user upload a photo, VGG search for similar-looking item by using cosine similiarity between image vectors.

3.To improve matching accuracy, YOLO object detection framewwork was used to autimatically identiy and crop the human and clothes in the images. Feed cropped the images to VGG16 has greatly improved model accuracy.

4.Classify more than 1600 brands in my database into 5 tiers using k-means clustering based on mean sale price if each brand.

5.Final Pipeline:
when user upload a photo and enter the brand name of the clothes, Savvy seller will first identify the human/clothes in the image and automatically crop out the background, then feed the cropped images to the headless VGG16 model and convert that specific images into vector. After that, Savvy Seller will search for images that were from the same brand tires as entered brand to find most similar looking items in the database. Cosine similarity between images vectors to find the most similar looking items that were sold in the last 2 weeks and return the average sale price.

For detailed code, please check out my [github repo](https://github.com/enjieli/Savvy_Seller), or click on the video below.
[![watch this video](https://img.youtube.com/vi/bLUPUxkJRuI/maxresdefault.jpg)](https://youtu.be/bLUPUxkJRuI)

