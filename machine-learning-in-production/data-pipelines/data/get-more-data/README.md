# How do you get more data?

## Data Augmentation

- Augmentation is a way to expand datasets
- One is introducing minor alterations in the existing samples (flip, rotate, etc.)
- can reduce overfitting
- beware invalid exmaples (flipping STOP sign) could be problematic

CIFAR-10 dataset is common for computer vision
60k 32x32 color images
10 classes with 6k in each class

```
def augment(x, height, width, num_channels):
    x = tf.image.resize_with_crop_or_pad(x, height + 8, width + 8)
    x = tf.image.random_crop(x, [height, width, num_channels])
    x = tf.image.random_flip_left_right(x)
    # return the altered image 
    return x
```

Other techniques
1. semi-supervised data augmentation (UDA)
1. Policy based data augmentation (AutoAugment)