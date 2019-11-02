# Normal and Reduction cell implementation for Test task
- This Repository contains Implementation of the Normal and Reduction cell stacked together on CIFAR10 dataset 
- It also contains summary of paper, in a presentation.
## Normal Cell Structure

![normal_cell](https://user-images.githubusercontent.com/8547940/68075981-56455800-fdaf-11e9-9d34-cbb2b43f9311.png)

## Reduction Cell Structure

![Reduction_cell](https://user-images.githubusercontent.com/8547940/68069559-c3320100-fd61-11e9-8361-5cb28421a1bb.png)

## Network Structure
- N = 1, tried with N = 2, but network is too large to train
- F = 32

![Network](https://user-images.githubusercontent.com/8547940/68069578-08eec980-fd62-11e9-8d92-a274b579f807.png)

## Implementation Details
- Normal Cell keeps the image size same; so stride for operations on normal cell is (1,1) keeping padding as "same" to maintain the size.
- Reduction Cell decreases the image size; so stride for operations on reduction cell is (2,2) keeping padding as "same". 
- Images are upsampled with size (2,2) interpolation='nearest':
  - Why Image is upsampled again to the normal size after reduction cell reduces the image size by half?  Because reduction cell requires combining different size operation; for example one op might give to output (16\*16\*3) and another op might give you output(32\*32\*3). To add these two operation you need same size. 
  - Also, in each combination image size in reduction cell is decreased by half so keep the image size same we are upsampling it.

## Training Details

- Training dataset size is 50000 images.
- Network is trained for 25 epochs.
- Training with Add operation to add the hidden outputs: Adding is nice if you want to interpret one of the inputs as a residual "correction" or "delta" to the other input.
- Train Accuracy: 71.91 % .

## Loss and Optimizer
- Since we have classes so loss used is categorical crossentropy.
- And RMSprop is used as an optimizer.

## Evaluate
- Dataset size is 10000 images
- Test Accuracy: 65.99 %**

## We can also apply transpose convoulution for upsampling the image in reduction cell, which might give better result.


