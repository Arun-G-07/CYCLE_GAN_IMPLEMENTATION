# CYCLE_GAN_IMPLEMENTATION

# CYCLE GAN
------------
Generative Adversarial Networks (GANs) use two neural networks i.e a generator that creates images and a discriminator that decides if those images look real or fake. Traditional GANs need paired data means each input image must have a matching output image. But finding such paired images is difficult which limits their practical use.

CycleGAN solves this problem by learning to change images from one style to another without needing matching pairs. It understands the features of the new style and transforms the original images accordingly. This makes it useful for tasks like changing seasons in photos, turning one animal into another or converting pictures into paintings. In this article we will see more about CycleGAN and its core concepts.

1. The process starts with an input image(xx) and Generator G translates it to the target domain like turning a photo into a painting. Then generator F takes this transformed image and maps it back to the original domain helps in reconstructing an image close to the input.
2. The model measures the difference between the original and reconstructed images using a loss function like mean squared error. This cycle consistency loss helps the network to learn meaningful,reversible mappings between the two domains.

![CYCLE-GAN](https://media.geeksforgeeks.org/wp-content/uploads/20200529210742/pairedvsunpaired.PNG)

# ARCHITECTURE OF CYCLEGAN
# 1. GENERATOR : Create new image in target style

![GENERATOR](https://media.geeksforgeeks.org/wp-content/uploads/20200529210740/cycleconsistencyandlosses.PNG)CycleGAN has two generators G and F:


1. G transforms images from domain X like photos to domain Y like artwork.
2. F transforms images from domain Y back to domain X.

# 2. DISCRIMINATORS : Decides whether the image id real or fake 
  There are two discriminators DₓDₓand DᵧDᵧ.

1. DₓDₓdistinguishes between real images from XXand generated images from F(y)F(y).
2. DᵧDᵧ distinguishes between real images from YYand generated images fromG(x)G(x).

# LOSSES IN CYCLE-GAN
1. Forward Cycle Consistency Loss  : Ensures that when we apply G and then F to an image we get back the original image
2. Backward Cycle Consistence Loss : Ensures that when we apply F and then G to an image we get back the original image.

# GENERATOR ARCHITECTURE
  Each CycleGAN generator has three main sections:

1. **Encoder**: The input image is passed through three convolution layers which extract features and compress the image while increasing the number of channels. For example a 256×256×3 image is          reduced    to 64×64×256 after this step.
2. **Transformer**: The encoded image is processed through 6 or 9 residual blocks depending on the input size which helps retain important image details.
3. **Decoder**: The transformed image is up-sampled using two deconvolution layers and restoring it to its original size.

![GENERATOR-ARCHITECTURE](https://media.geeksforgeeks.org/wp-content/uploads/20200605220659/generator.jpg)

# DISCRIMINATOR ARCHITECTURE(PATHGAN)
  In CycleGAN the discriminator uses a PatchGAN instead of a regular GAN discriminator.

1. A regular GAN discriminator looks at the entire image (e.g 256×256 pixels) and outputs a single score that says whether the whole image is real or fake.
2. PatchGAN breaks the image into smaller patches (e.g 70×70 patches). It outputs a grid (like 70×70 values) where each value judges if the corresponding patch is real or fake.

This lets PatchGAN focus on local details such as textures and small patterns rather than the whole image at once it helps in improving the quality of generated images.

![DISCRIMINATOR-ARCHITECTURE](https://media.geeksforgeeks.org/wp-content/uploads/20200605220731/Discriminator.jpg)

# COST FUNCTIONS IN CYCLE-GAN

1. **Adversarial Loss** : We apply adversarial loss to both our mappings of generators and discriminators. This adversary loss is written as :
                                    ---------------------------------------------------------------------------
                                    Lossadvers(G,Dy,X,Y)=1m∑(1−Dy(G(x)))2Lossadvers​(G,Dy​,X,Y)=m1​∑(1−Dy​(G(x)))2
                                    ---------------------------------------------------------------------------
                                    -----------------------------------------------------------------------------
                                    Lossadvers(F,Dx,Y,X)=1m∑(1−Dx(F(y)))2   Lossadvers​(F,Dx​,Y,X)=m1​∑(1−Dx​(F(y)))2   
                                    -----------------------------------------------------------------------------

2. **Cycle Consistancy Loss** :  Given a random set of images adversarial network can map the set of input image to random permutation of images in the output domain which may induce the output distribution similar to target distribution. Thus adversarial mapping cannot guarantee the input xi  to yi . For this to happen we proposed that process should be cycle-consistent. This loss function used in Cycle GAN to measure the error rate of  inverse mapping G(x) -> F(G(x)). The behavior induced by this loss function cause closely matching the real input (x) and F(G(x))

# APPLICATION OF CYCLE-GAN IN IMAGE TRANSLATION
  1. Collection Style Transfer
  2. Object Transformation
  3. Seasonal Transfer
  4. Photo Generation from painting
  5. Photo Enhancement




















