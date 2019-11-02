# Normal and Reduction cell implementation for Test task
- This Repository contains Implementation of the Normal and Reduction cell stacked together on CIFAR10 dataset 
- It also contains summary of paper, in a presentation.
- Normal Cell and Reduction cell has two inputs. For now giving two input same, i.e. previous cell output.
- I tried stacking normal and reduction cell and also implemented skip connections but network was too slow to train. so for now keeping N = 1. Code is there but I have commented it out. You can have a look at commented code.

## Normal Cell Structure

![normal_cell](https://user-images.githubusercontent.com/8547940/68075981-56455800-fdaf-11e9-9d34-cbb2b43f9311.png)

## Reduction Cell Structure

![Reduction_cell](https://user-images.githubusercontent.com/8547940/68069559-c3320100-fd61-11e9-8361-5cb28421a1bb.png)

## Network Structure
- N = 1
- F = 32

![Network](https://user-images.githubusercontent.com/8547940/68069578-08eec980-fd62-11e9-8d92-a274b579f807.png)

## Implementation Details
- Normal Cell keeps the image size same; so stride for operations on normal cell is (1,1) keeping padding as "same" to maintain the size.
- Reduction Cell decreases the image size; so stride for operations on reduction cell is (2,2) keeping padding as "same". 
- Images are upsampled with size (2,2) interpolation='nearest':
  - Why Image is upsampled again to the normal size after reduction cell reduces the image size by half?  Because reduction cell requires combining different size operation; for example one op might give to output (16\*16\*3) and another op might give you output(32\*32\*3). To add these two operation you need same size. 
  - Also, in each combination image size in reduction cell is decreased by half so keep the image size same so I thought of upsampling it.

## Training Details

- Training dataset size is 50000 images.
- Network is trained for 10 epochs.
- Train Accuracy:  77.48 % .

## Loss and Optimizer
- Since we have classes so loss used is categorical crossentropy.
- And RMSprop is used as an optimizer.

## Evaluate
- Dataset size is 10000 images
- Test Accuracy: 68.56 %

## Future work 
- We can use different values of N and F and try changing learning rate and other hyperparameters.
- We can also apply transpose convoulution for upsampling the image in reduction cell, which might give better result.
- Model is overfitting so we can use drop out and batch normalization.


