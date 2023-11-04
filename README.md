# Revisiting_and_Refining_AdaIN
*Project of ECE285: Deep Generative Models*

This project primarily concentrates on the enhancement of the AdaIn style transfer model through two fundamental alterations: the integration of multi-level style transfer and the replacement of the AdaIn Module with a style-attentional Module. While the conventional AdaIN model employs the COCO Dataset for content images and the Wikiart Dataset for style images, the focus of this project lies in broadening the model's adaptability through the incorporation of new datasets for evaluation. To this end, the project makes use of the Flickr Image Dataset for content images and the Painter by Numbers Dataset for style images.

## Model Enhancement
### Multi-level Style Transfer
Departing from the traditional single-level approach, the proposed enhancement aims to implement a multi-level style transfer (Figure \ref{NewArch}). This approach allows for a more nuanced and enriched stylization process, resulting in superior output images.

The proposed approach exploits the encoder's ability to extract hierarchical features at various levels, with each level capturing unique style information at different scales and complexities. Incorporating features from multiple encoder layers (specifically '$relu2\_1$' to '$relu4\_1$' in the implementation) deepens the richness of the style transfer by capturing stylistic elements at varying scales and abstraction levels. However, this method demands greater computational resources due to its comprehensive style representation.

### Loss Function Modification
Transitioning from single-level to multi-level style transfer necessitates an adaptation in the structure of the loss function. Given the AdaIN model's tendency to overfit and compromise content integrity, and the need to accommodate the multi-level architecture, I significantly modify the content loss function while the overall and style loss functions remain consistent:

## Results and Discussion

This section delineates the outcomes from the reimplementation of the original AdaIN model and juxtaposes the enhanced model against the original one.

### Alpha
<img width="1000" alt="image" src="https://github.com/GAOChengzhan/Revisiting_and_Refining_AdaIN/assets/39005000/9e4ba774-fed2-4294-89ba-bda60087994a">

The AdaIN model utilizes a parameter, termed as 'alpha', which dictates the degree of stylization during training. As evident from Figure 5, the stylization intensity of the output image escalates as $\alpha$ elevates from 0 to 1. This variable, therefore, stands crucial in managing the level of style infusion within the content image.

### Style interpolation

<img width="800" alt="image" src="https://github.com/GAOChengzhan/Revisiting_and_Refining_AdaIN/assets/39005000/539696d3-7857-4f2a-a079-411886d1044b">

The AdaIN model can assimilate multiple styles simultaneously, as depicted in Figure 6. Different style inputs are individually processed with the content image through the AdaIN module. The resultant stylized features are then normalized by the corresponding weights and aggregated. The consolidated feature set finally passes through the decoder to yield the output image.

### Multi-level Style Transfer

<img width="400" alt="image" src="https://github.com/GAOChengzhan/Revisiting_and_Refining_AdaIN/assets/39005000/27d8be63-b411-40e4-8188-b201c64cd178">
<img width="400" alt="image" src="https://github.com/GAOChengzhan/Revisiting_and_Refining_AdaIN/assets/39005000/9e8eae5e-072d-4c97-b7f1-5e01abbb9f35">

*Upper-left: content image, bottom-left: style image, upper-right: stylized image by multi-level style transfer, bottom-right: stylized image by single-level style transfer, right column: details of the stylized images*

<img width="1000" alt="image" src="https://github.com/GAOChengzhan/Revisiting_and_Refining_AdaIN/assets/39005000/5d4a2b3d-c65b-4bd7-9654-69b6e640205e">


Incorporating the AdaIN module at multiple stages of the VGG encoder, the enhanced model demonstrates a marked improvement over its predecessor. A conspicuous divergence between the multi-level and single-layer transfer models lies in their ability to retain the original content. The multi-level style transfer approach maintains the content image in superior detail and refinement, which is evident from Figure 8. This enhanced content preservation is credited to the fact that in a multi-level setup, even the lower features of the encoder, encapsulating the original content information, are subjected to style transfer.

The whole-scale comfort and nuanced detail preservation of the enhanced model become apparent upon comparison with the original one, as shown in Figure 6. This is further corroborated by the portrait example (Figure 7.a), where the lip, hair, and mustache details are well conserved, and the landscape example (Figure 7.b), where the bridge and mountain specifics are well preserved. While this detailed retention in most cases is advantageous, it might hamper the artistic style for users seeking a more immersive stylization matching the brushstroke of the style image, as evident in Figure 7.b.

### Style-Attentional Module

<img width="1200" alt="image" src="https://github.com/GAOChengzhan/Revisiting_and_Refining_AdaIN/assets/39005000/5a9a1c72-0b8c-4803-b35f-0f6c291b3d7b">

Substituting the AdaIN Module with the Style-Attentional Module enriches the resultant stylized image by incorporating not only the color cues but also additional aspects such as texture, shape, and brushstroke style from the style input(Figure 9). This advancement is well illustrated in the first column, where the splashed-ink style of the input is effectively imitated by the enhanced model. In the fourth and fifth columns, the stylized outputs of the enhanced model, unlike its counterparts, adeptly recreate the straight lines and circles from their respective style inputs. Similarly, in the last column, the style of the enhanced model's output closely resembles the painting style of the input. The superior performance of the Style-Attentional module underscores its effectiveness in capturing and transposing nuanced stylistic details.

## Conclusion

This project constituted a comprehensive exploration and enhancement of the AdaIN style transfer model, a cornerstone of computer vision. The primary aim was to augment the model's capabilities and extend its applications across different datasets. The project was successful in implementing the proposed modifications, leading to improved style transfer performance.

An innovative approach was the introduction of multi-level style transfer, where the AdaIN module was applied at various encoder levels, yielding a more integrated and detailed rendering of stylized images. This approach preserves the original content more effectively compared to single-level style transfers, but the increase in computational resources needed for this more comprehensive style representation is a downside. It would be beneficial for future research to seek methods that optimize this resource demand.

To provide an even more nuanced style transfer, the AdaIN module was replaced with a Style-Attentional Module. The Style-Attentional Module employs a self-attention mechanism for a more detailed style representation and precise matching process between content and style features. This modification enabled a detailed and accurate style transfer, capturing the unique attributes of the style image while simultaneously preserving the integrity of the content.

The successful implementation of these enhancements significantly improved the quality of the output images, which was clearly demonstrated in various examples. This notwithstanding, it is important to note that while the enhanced model's detailed content retention is beneficial in many cases, it might inhibit the artistic style for users seeking a more immersive stylization.

Overall, the modifications made to the AdaIN style transfer model in this project highlight the potential for future innovations in this field. The improvements made, while significant, represent just a fraction of what is possible. Future work could focus on reducing the computational burden without compromising the model's performance, and possibly fine-tuning the balance between content preservation and stylization. It is hoped that the work done here can serve as a stepping stone for further advancements, pushing the boundaries of what is possible in the fascinating realm of style transfer.
