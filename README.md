# Project overview
This repo holds materials for a paper I presented at the 37th SIOP conference. The paper was about the utility (in terms of compute and training time) of using variational autoenoders for parameter recovery as compared to multidimensional IRT. This was a kind of "lofi" simulation to seed the idea in the I/O psychology community.

The project was to create a head-to-head comparison between VAEs and MIRT models. This is based on work by Curi et al. (2019) and Converse (2020). 

## What are the advantages of using VAEs? 

- VAEs produce exact approximations of parameters recovered from multidimensional 2PL models
  - Thus, unity is achieved between theta estimates of each factor for 2PL models and VAEs
- VAEs require _way_ less compute than IRT models
- VAEs recover parameters at faster speeds (by orders of magnitude)
- VAE architecture can be built to meet IRT assumptions

## Simulation setup 
- Data 
  - Simulated response data and Q matrices using simcdm package in R 
  - 30, 50, 100 items
  - 3, 5 factors (correlated) 
- IRT model
  - 2PL models built using mirt package in R
  - MIRT model specified to Q-matrix structure
  - Monte Carlo EM estimation (1000 cycles)
- VAE architecture 
  - VAE models built using ML2Pvae package in R
  - 2 encoder hidden layers
  - 3 factors: 16 nodes (hidden 1), 8 nodes (hidden 2)
  - 5 factors: 24 nodes (hidden 1), 16 nodes (hidden 2) 
  - Epochs and batch sizes were tuned

## Results 
We can see training times are lower for VAE across all conditions. Training times are more or less consistent and linear for VAE across conditions. However, the training times for MIRT models exponentially increase as sample sizes increase. We also see training times increase as estimated latent factors increase. VAEs remain unaffected. 
![vae-training-time](https://user-images.githubusercontent.com/24941864/205695209-a91ed34c-7dfa-449f-8b1a-daa811656baa.png)

### References 
Converse, G. (2020). ML2Pvae: Variational autoencoder models for IRT parameter estimation. R package version 1.0.0. https://CRAN.R-project.org/package=ML2Pvae

Curi, M., Converse, G. A., Hajewski, J., & Oliveira, S. (2019, July). Interpretable variational autoencoders for cognitive models. In 2019 International Joint Conference on Neural Networks (IJCNN) (pp. 1-8). IEEE.
