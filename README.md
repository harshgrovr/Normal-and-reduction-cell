# Normal and Reduction cell implementation for Test task

- This Repository contains Implementation of the Normal and Reduction cell stacked together on CIFAR10 dataset
## Implementation Details
- Normal Cell keeps the image size same; so stride for operations on normal cell is (1,1) keeping padding as "same" to maintain the size.
- Reduction Cell decreases the image size; so stride for operations on reduction cell is (2,2) keeping padding as "same". 
- Images are upsampled with size (2,2) interpolation='nearest':
  - Why Image is upsampled again to the normal size after reduction cell reduces the image size by half?  Because reduction cell requires combining different size operation; for example one op might give to output (16\*16\*3) and another op might give you output(32\*32\*3). To add these two operation you need same size. 
  - Also, in each combination image size in reduction cell is decreased by half so keep the image size same we are upsampling it.
- Parameters:  N=1(number of normal and reduction cell in network), F=32(Filters)
- Tried two approaches:
  -  Normal cell and reduction cell both using add operarion while combining two hidden states.
  -  Normal cell and reduction cell both using concatenate operarion while combining two hidden states.
-  Training and test Results are shared for both.



## Training Details

- Training dataset size is 50000 images.
- Network is trained for 25 epochs.
- Training with Add operation to add the hidden outputs: Adding is nice if you want to interpret one of the inputs as a residual "correction" or "delta" to the other input.
  - Train Accuracy with add: 62.78 % .
- Training with Concatenate operation to merge the hidden outputs: Concatenating may be more natural if the two inputs aren't very closely related.
  - Train Accuracy with add: 71.91 % .


## Loss and Optimizer
- Since we have classes so loss used is categorical crossentropy.
- And RMSprop is used as an optimizer.

## Evaluate
- Dataset size is 10000 images
- Test Accuracy with add: 60.61 % 
- Test Accuracy with Concatenate: 65.99 % 


## We can also apply transpose convoulution for upsampling the image in reduction cell, which might give better result.
