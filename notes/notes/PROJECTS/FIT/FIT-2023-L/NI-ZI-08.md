TARGET DECK: NI-ZI-2023::NI-MVI
FILE TAGS: NI-ZI-2023 NI-ZI-08 NI-MVI

prev::[[NI-ZI-07]]
next::[[NI-ZI-09]]

# Autoencodery a generativní neuronové sítě


Co je to autoencoder, základní myšlenka. Využití jednoduchého AE #flashcard 
Je to feed forward NN 
![[ae.png]]
Lze je použít např. na  kompresi dat, redukci dimenzionality, generování datových bodů, recommender, překlad.
Trénuje se pomocí reconstruction error - MSE mezi vstupem a výstupem
<!--ID: 1691966314062-->



Porovnejte Autoencoder a PCA #flashcard 
PCA je lineární transformace zachovávající maximální rozptyl tříd. PCA příznaky jsou ortogonální a lineárně nekorelované. AE je nelineární, pomalejší a dražší, příznaky mohou být korelované. AE s jednou vrstvou a lin. aktivací je hodně podobný PCA.
<!--ID: 1691966314063-->



Jak lze využít autoencoder v computer vision? #flashcard 
Často se používá architektura U-net, která mezi encoder a decoder přidává residual connections:
Superresolution, denoising, image compression, dogenerování barev, oldify, image classification, image generation, semantic segmentation
<!--ID: 1691966314064-->



Autoencodery lze použít na generování. Jaký typ AE se nejčastěji používá a jaké úlohy znáš? #flashcard 
Používají se variational autoencoder (VAE), a generative AI algorithm that uses deep learning to generate new content, detect anomalies and remove noise. Dále se dají použít pro generování textu, časových řad, ale i videa.
<!--ID: 1691966314065-->



Jak principielně funguje variational autoencoder (VAE) #flashcard 
A variational autoencoder (VAE) provides a _probabilistic_ manner for describing an observation in latent space. Thus, rather than building an encoder which outputs a single value to describe each latent state attribute, we'll formulate our encoder to describe a probability distribution for each latent attribute.
![[vae.png]]
Z distribucí co dostaneme v latentním prostoru pak můžeme samplovat a dostaneme tak různé výstupy ve stejné distribuci.
[tohle](https://www.jeremyjordan.me/variational-autoencoders/) je super článek.
<!--ID: 1691966314066-->



Jak počítáme ztrátu pro variational autoencoder? Aspoň principielně... #flashcard 
![](https://www.jeremyjordan.me/content/images/2018/03/Screen-Shot-2018-03-17-at-11.31.15-PM.png)
Our loss function for this network will consist of two terms, one which penalizes reconstruction error (which can be thought of maximizing the reconstruction likelihood as discussed earlier) and a second term which encourages our learned distributioni $q(z\mid x)$ to be similar to the true prior distribution $p(x)$, which we'll assume follows a unit Gaussian distribution, for each dimension of the latent space.
$$\mathcal{L}(x, \hat{x})+\sum_j K L\left(q_j(z \mid x) \| p(z)\right)$$
<!--ID: 1691966314067-->



Namalujte schéma architektury generative adversarial network (GAN) #flashcard 
![[gan.jpeg]]
<!--ID: 1691966314068-->



Algoritmus trénování generative adversarial network GAN #flashcard 
![[gan_alg.png]]
<!--ID: 1691966314069-->



Jaké problémy mají GANy? #flashcard 
* kvalita: Počet, perspektiva, globální struktura
* nestabilní tréning
* mode collapse - Each iteration of generator over-optimizes for a particular discriminator, and the discriminator never manages to learn its way out of the trap. As a result the generators rotate through a small set of output types. This form of GAN failure is called **mode collapse**
<!--ID: 1691966314070-->
