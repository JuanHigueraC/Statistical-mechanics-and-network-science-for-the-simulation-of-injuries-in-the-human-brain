# Statistical-mechanics-and-network-science-for-the-simulation-of-injuries-in-the-human-brain
This project was realized by

**Juan C Higuera C**

**Diego A Heredía F**

**Kevin N Ramos G**

**Cristian D Salazar G**

**Felipe R Amador G**


This project was presented for the course **Introduction To Theoretical Research** of the National University of Colombia. 


In this work we tried to predict the impact in the whole brain activity of injuries in particular brain regions with specifical integration/segregation properties using a statistical mechanical model.

## Abstract 
Using structural, diffusion, and functional MRI data from the HCP dataset for healthy young adults, we build network models in which nodes are brain regions and edges are anatomical connections or correlates in metabolic activity. We then simulated the correlation in metabolic activity using the Generalized Ising Model (GIM) in the anatomical network, this model presented the best fit with the metabolic activity of the healthy resting human brain in the maximum entropy regime, at the edge of the criticality. Subsequently, the anatomical network was modified with the aim of simulating a local brain injury, the impact of these local injuries on global activity was quantified by means of entropy (in this case a measure of the computational power of the network) and the difference with the empirical brain health metabolic correlations. We found that of the measures used, geodesic betweenness centrality and degree were the best predictors of the impact of local injury on simulated whole brain activity, however how whole brain activity is affected is dependent on topological properties. of the local injured region.

## Building Brain Networks
For the construction of brain networks its necessary define what entities are the nodes and what are the edges, this translating from the real brain to the mathematical network model is presented in this section.


### Nodes
The human brain has on the order of $10^{11}$ neurons and $10^{11} \times 10^5$ connections, this has undoubted implications, the network of the real human brain at this moment is not simulable. For this and other reasons its fundamental build low dimensional representations of the brain, this representations are knowed as parcellations. In this work the parcellation choosed was the Hammersmith parcellation, present in the recopilation of parcellation present in https://github.com/neurodata/neuroparc.

![image](https://github.com/JuanHigueraC/Statistical-mechanics-and-network-science-for-the-simulation-of-injuries-in-the-human-brain/blob/083983ed2c104290ca1ca5c9cad892a3e4828559/Images/parcellation.PNG)

**Figure 1. Parcellation of the humban brain**

### Structural Edges
The structural edges of the anatomical network was defined as the number of nervious tracts, number infered from **difusion magnetic resonance** data and **deterministic tractography algorithm**.

![image](https://github.com/JuanHigueraC/Statistical-mechanics-and-network-science-for-the-simulation-of-injuries-in-the-human-brain/blob/8272ed1223cd5a76251eeaf03fa0d49e19be387c/Images/tractografia.PNG)

**Figure 2. Nervious Tracts infered from difusion magnetic resonance data and deterministic tractography algorithm**

With this nervious tracts a network representation was builded, then a threshold was applied and a normalization of the strength of the ties of a node, with respect to the total strength of its ties. After this procedure the matrix representation of the anatomical network resulted in:

![image](https://github.com/JuanHigueraC/Statistical-mechanics-and-network-science-for-the-simulation-of-injuries-in-the-human-brain/blob/2f05373eb73032d86fc85a2e2eb5797561e219e9/Images/SC.PNG)

**Figure 3. Matrix representation of the anatomical network after the normalization and threshold procedure**

### Functional Edges

The functional information used was the mean BOLD signal within a brain region

![image](https://github.com/JuanHigueraC/Statistical-mechanics-and-network-science-for-the-simulation-of-injuries-in-the-human-brain/blob/2f05373eb73032d86fc85a2e2eb5797561e219e9/Images/bold%20parcel%20signa.PNG)

**Figure 4. BOLD signal averaged within a brain region**

Functional edges are defined as pearson linear correlation coefficient between metabolic activity time series of the brain regions, the matrix representation of the resulting network is presented below

![image](https://github.com/JuanHigueraC/Statistical-mechanics-and-network-science-for-the-simulation-of-injuries-in-the-human-brain/blob/2f05373eb73032d86fc85a2e2eb5797561e219e9/Images/FC.PNG)

**Figure 5. Matrix representation of the functional network**

## Maximum entropy model of discrete network(brain) states (Generalized Ising Model)

### Model

### Entropy and maximum similarity with the empirical correlations

## Results

### Simulated correlations 

### Conclusions

## References
