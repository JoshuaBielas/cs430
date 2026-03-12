# Names: Josh Bielas and Josh Garbi
# Lab: lab7 (Vision)
# Date: 3/11/2026

1. Describe two or three distinct visual patterns you observe across the 16 feature maps. What kind of image structures (edges, textures, colors) does Layer 1 appear to be responding to?

    Filter 0 and filter 3 appear to look at the eyes of the rabbit a lot. Filter 8 looks at the background. Filter 2 traces the outline of the rabbits head and ears. For the most part it looks at textures. It also appears to look at the edges quite a bit. 

2. Some feature maps appear almost entirely dark or uniform. What does a near-zero activation mean in terms of what the filter "found" in this particular image? What would cause a filter to activate strongly?'

    It would mean that it didn't find anything. What it was looking for wasn't very present in the image. A filter would activate strongly if it found a lot of strong matches to what it was looking for. 

3. How do the Layer 4 feature maps differ visually from Layer 1 maps? What does this tell you about the nature of the representations learned at different depths?

    Layer 1 has many more smaller pixel groupings that it checks. Layer 4 has fewer but larger groupings of pixels that it checks. Pixel groupings in layer 4 are larger and contain more information. It tells us that it starts by gaining understanding of small sections, and then it combines that understanding to learn about larger sections. 

4. If you used a completely different image (e.g., a car instead of a dog), which layer's feature maps would change more dramatically — Layer 1 or Layer 4? Justify your answer based on what each layer has learned.

    Layer 1 has more pixels to show change visibly, but layer 4 stores much more meaning because it has combined the information from the previous layers into bigger groups. Althout it may look like there is more change in layer 1, layer 4 would actually be storing more dramatic changes. Layer 4 would change more because it has learned more. 

5. Describe the spatial pattern of the Grad-CAM heatmap. Does the model appear to focus on the object of interest or on surrounding context? What are the implications for model trustworthiness?

    It seems to focus on the object of interest pretty well. It does get off of it a little bit, but the center of its interest is near the rabbits head. Since it focuses on the model of interest pretty well, it would be pretty trustworthy in this case. How trustworthy it is will depend on where it focuses for different images. It predicted well.

6. Grad-CAM uses gradients from a specific class to generate the heatmap. What would happen to the heatmap if you asked it to explain the prediction for a wrong class (e.g., generating a heatmap for "cat" when the image contains a dog)?

    We would expect the heatmap to focus on the regions of the heatmap that it would be looking at if the image actually was a dog. Since the animals are somewhat similar, it might do ok, but they are still different animals. This would probably lead to a prediction that isn't very good. 

7. If a model correctly classifies a "polar bear" image but Grad-CAM shows it attended primarily to the snow background, what does this tell us about what the model actually learned? How might this model perform on a polar bear image in a zoo?

    It learned that a snowy background often attends to a polar bear. It may not really have learned what a polar bear actually is. This would affect a model's performance of identifying a polar bear in a zoo if its environment is not snowy. If there is no snow, it likely won't classify it as a polar bear because snow is what it believes is important for being a polar bear. 

8. Look at the amplified perturbation image. Does it look like anything meaningful to you? Now consider that the model finds this pattern highly informative — what does this reveal about the difference between how humans and CNNs represent images?

    No, it doesn't really look like anything meaningful although you can see a little bit of an outline of the rabbit in the noise. It sees this as informative because it does pattern recognition through pixel values rather than looking at the image as a whole like humans do. We know its a rabbit because we have seen rabbits before. The CNN knows its a rabbit because of the values in the many pixels. The adversarial image looks very similar to the original image when looking at it with the human eye. 

9. At what epsilon value does the model lose confidence in the correct class below 50% in your run? What does this tell you about how close the original image is to the decision boundary in pixel space?

    Its confidence in correct class drops below 50% at epsilon = 0.005. It tells us that the original image is close to the decision boundary in pixel space because it changes to not being confident in its original classification very quickly. 

10. Consider a safety-critical application like medical imaging diagnosis or autonomous driving. Based on your observations across Exercises 6 and 7, what specific risks do adversarial examples pose, and what would you want to know about a deployed model's adversarial robustness before trusting it?

    For medical imaging diagnosis adversarial images pose a high risk of false negatives which is a big problem when we need to know with high confidence what something is such as cancer. A self driving car could incorrectly classify a pedestrian and end up injuring them. I would want to know about its ability to correctly identify adversarial images with high confidence. I would also want to know that it knows the objects it will be seeing very well, and that it has been thoroughly tested. 