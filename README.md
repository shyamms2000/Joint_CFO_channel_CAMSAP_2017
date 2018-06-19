# CAMSAP_paper
The directory contains all the codes required to reproduce the results in our CAMSAP 2017 paper titled "Joint CFO and channel estimation in millimeter wave systems with one-bit ADCs" [1].

On using our CAMSAP code:- 

The code "Joint_estimation/single_run_one_bit_CAMSAP.m" performs joint CFO and channel estimation in an mmWave setup with one-bit ADCs. The parameters in the code are those used in [1]. Although the code is built using bilinear GAMP, it performs standard EM-GAMP with one-bit measurements. This was done by forcing one of the bilinear vectors to be the scalar 1; the other vector is the lifted vector to be estimated, i.e., x in the CAMSAP paper. 
The code "single_run_one_bit_CAMSAP.m" recovers the $b$ and $c$ in the CAMSAP paper and plots them for one channel and training realization at SNR=0 dB. You can see that the algorithm can recover the beamspace components from the output figures and the NMSE. Also, the DFT of the CFO error vector is also recovered approximately and is sufficient enough for interpolation based CFO estimation. 

Reproducing our results:-

After you run "single_run_one_bit_CAMSAP.m", you may have realized that the algorithm takes too long. It took about 15-20 sec on my MAC. Therefore, this approach is not very scalable to higher dimensional problems. The results in our CAMSAP paper were  obtained by running our algorithm on 3 machines for several days. I have included the data (.mat) files here to generate the plots in my CAMSAP paper. All plots in our paper can be generated by running "data_and_results/plots_includes_64_pilots/plot_all.m". Please set the plotflag in line 3 to {1,2 or 3} to get the three plots of our paper. The "plot_all.m" code also includes the CFO estimation algorithm. 

On the complexity of our algorithm:-

A main drawback of our joint estimation algorithm for one-bit ADCs (CAMSAP) is due to its high complexity and memeory requirement. This issue is explained clearly in Section III-B.2 of our work [2]. Our bilinear message passing based approach in [2] overcomes the lifting trick in [1] and performs significantly better in terms of joint estimation, computational complexity and memory footprint. For instance, for the parameters in [1], our algorithm in [2] took about 1 second including setting up the problem. The codes for [2] will be uploaded soon.

Our new algorithm called Swift-Link [3] approaches the joint estimation problem from a training design perspective. Swift-Link controls the impact of CFO on the beamspace estimate and has lower-complexity than [1] and [2]. Swift-Link runs as fast as a standard compressed sensing problem with partial DFT-based measurement matrices. Swift-Link's training and algorithm are very easy to implement when compared to those in [1] and [2]. Furthermore, it's extension to other architectures like hybrid beamforming, switching or one-bit receivers are straightforward. 

For more details on the algorithm and implementation, please contact me at nitinjmyers@utexas.edu 
I will post the codes for [2] and [3] as soon as they get published on IEEE Xplore. 

All of the following papers are also available on arxiv. 

[1] N.J. Myers and R. W. Heath Jr., "Joint CFO and Channel Estimation in Millimeter Wave Systems with One-Bit ADCs", in Proc. of IEEE CAMSAP 2017

[2] N.J. Myers and R. W. Heath Jr., "Message passing-based joint CFO and channel estimation in millimeter wave systems with one-bit ADCs", submitted to IEEE Transactions on Wireless Communications, March 2018 

[3] N.J. Myers, A. Mezghani and R. W. Heath Jr., "Swift-Link : A compressive beam alignment algorithm for practical mmWave radios", submitted to IEEE Transactions on Signal Processing, June 2018 
