# ComfyUI_TravelSuite_Zho

--------
## LatentTravel Node

Travel between different latent spaces using a range of blend and travel modes.

### 1）How to use：
![9b2a5aa4875c678c95da6ffd80fb5512](https://github.com/ZHO-ZHO-ZHO/ComfyUI_TravelSuite_Zho/assets/140084057/829b7730-4579-4575-8f3a-f873062a58b0)

workflow：[Latent_travel_workflow【Zho】.json](https://github.com/ZHO-ZHO-ZHO/ComfyUI_TravelSuite_Zho/files/13271012/Latent_travel_workflow.Zho.json)


### 2）Compare to Conditioning average & Latent composite：
![image](https://github.com/ZHO-ZHO-ZHO/ComfyUI_TravelSuite_Zho/assets/140084057/6ca11fbb-a5b0-41e0-8f1a-d6edd990239a)

workflow：[Latent_travel_compare2composite_workflow【Zho】.json](https://github.com/ZHO-ZHO-ZHO/ComfyUI_TravelSuite_Zho/files/13271090/Latent_travel_compare2composite_workflow.Zho.json)

### 3）Differences from original branch：
- Change BOOL to BOOLEAN (for "reflect_travel", "output_images" and "save_images")
- Change some names:
  - "write_images" to "save_images"
  - "prefix" to "filename_prefix"


(修改为boolean模式 + 修改参数位置和名称)


--------
## Node：

![image](https://github.com/ZHO-ZHO-ZHO/ComfyUI_TravelSuite_Zho/assets/140084057/933f7e88-65c6-4a19-b9f6-7f220e4a5bbd)


___**Node Inputs**___
- **A, B**: Latent variables needed for the process.
- **vae**: VAE (Variational Autoencoder) type, to decode generated latents to tensors. 
- **steps**: Integer representing the number of steps. This includes the two input latents A and B which will always be the first and last latents. The default value is 5. It should be within the range [0,10000].
- **factor**: A floating-point value with a default of 0.5. This value depends on the travel_mode specified
- **blend_mode**: Specifies the method used for latent blending: lerp", "slerp", "add", "multiply", "divide", "subtract", "overlay", "hard_light", "soft_light", "screen", "linear_dodge", "difference", "exclusion", "random"
- **travel_mode**: Determines the travel interval model:
  - 'linear': linear interpolation
  - 'hinge': takes factor as a cutpoint and splits the steps evenly between above and below the hinge 
  - 'circle': steps along the X-axis of a circle 
  - 'norm': steps along a normal distribution centered at 0.5. Factor is the gaussian scale factor.
  - 'quadratic', 'cubic', 'quartic': steps along linear space raised to 2, 3, 4 powers.  
  - 'geometric': steps along geomspace from 0, 1
- **reflect_travel**: whether to reflect travel mode values around the center. 
- **output_images**: whether to output images.  Requires VAE input.
- **save_images**: whether to save output images.  Requires VAE input.
- **filepath**: String for defining the output path for the files. Default path is 'output/travel'.
- **filename_prefix**: String for prefixing the generated files. By default, this is 'travel'. 

___**Node Outputs**___

- **LATENTS**: Resulting travel latents. There will be `steps` latents, and the first and last will be the input `A` and `B`.
- **IMAGES**: Tensor images, if `output_images=True`. Requires VAE.
- **FILEPATHS**: List of filepaths produced if `save_images=True`.

