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
Using structural, diffusion, and functional MRI data from the HCP dataset for healthy young adults, we build network models in which nodes are brain regions and edges are anatomical connections or correlates in metabolic activity. We then simulated the correlation in metabolic activity using the Generalized Ising Model (GIM) in the anatomical network. This model presented the best fit with the correlations of metabolic activity of the healthy resting human brain in the maximum entropy regime, at the edge of criticality. Subsequently, the anatomical network was modified with the aim of simulating a local brain injury. The impact of these local injuries on global activity was quantified by means of the entropy (in this case, a measure of the computational power of the network) and the difference in metabolic activity correlations between the empirical data of a healthy brain and the simulated injured brain. Among the measures we analyzed, geodesic betweenness centrality and degree emerged as the best predictors of the impact of local injury on simulated whole brain activity. However, the effect of local injury on whole brain activity depends on the topological properties of the injured region.

## Building Brain Networks
For the construction of brain networks its necessary define what entities are the nodes and what are the edges, this translating from the real brain to the mathematical network model is presented in this section.


### Nodes
The human brain has on the order of $10^{11}$ neurons and $10^{11} \times 10^5$ connections, this has undoubted implications, the network of the real human brain at this moment is not simulable. For this and other reasons its fundamental build low dimensional representations of the brain, this representations are knowed as parcellations. In this work the parcellation choosed was the Hammersmith parcellation, present in the recopilation of parcellations present in https://github.com/neurodata/neuroparc.

![image](https://github.com/JuanHigueraC/Statistical-mechanics-and-network-science-for-the-simulation-of-injuries-in-the-human-brain/blob/083983ed2c104290ca1ca5c9cad892a3e4828559/Images/parcellation.PNG)

**Figure 1. Parcellation of the humban brain**

### Structural Edges
The structural edges of the anatomical network was defined as the number of nervious tracts, number infered from **difusion magnetic resonance** data and **deterministic tractography algorithm**.

![image](https://github.com/JuanHigueraC/Statistical-mechanics-and-network-science-for-the-simulation-of-injuries-in-the-human-brain/blob/8272ed1223cd5a76251eeaf03fa0d49e19be387c/Images/tractografia.PNG)

**Figure 2. Nervious Tracts infered from difusion magnetic resonance data and deterministic tractography algorithm**

With this nervious tracts a network representation was builded, then a threshold was applied and a normalization of the strength of the ties of a node, with respect to the total strength of its ties. After this procedure the matrix representation of the anatomical network resulted in:

![image](https://github.com/JuanHigueraC/Statistical-mechanics-and-network-science-for-the-simulation-of-injuries-in-the-human-brain/blob/2f05373eb73032d86fc85a2e2eb5797561e219e9/Images/SC.PNG)

**Figure 3. Matrix representation of the anatomical network after the normalization and threshold procedure. The colorbar are proportional to the normalized thresholded number of tracts between brain regions**

### Functional Edges

The functional information used was the mean BOLD signal within a brain region

![image](https://github.com/JuanHigueraC/Statistical-mechanics-and-network-science-for-the-simulation-of-injuries-in-the-human-brain/blob/2f05373eb73032d86fc85a2e2eb5797561e219e9/Images/bold%20parcel%20signa.PNG)

**Figure 4. BOLD signal averaged within a brain region. Colorbar are proportional to the pearson correlation coefficient between brain regions**

Functional edges are defined as pearson linear correlation coefficient between metabolic activity time series of the brain regions, the matrix representation of the resulting network is presented below

![image](https://github.com/JuanHigueraC/Statistical-mechanics-and-network-science-for-the-simulation-of-injuries-in-the-human-brain/blob/2f05373eb73032d86fc85a2e2eb5797561e219e9/Images/FC.PNG)

**Figure 5. Matrix representation of the functional network**

## Maximum entropy model of discrete brain states
What we want to model are the correlations in metabolic activity brain, measured by fMRI. For this we consider that each brain region can only have two activation states, +1 and -1; +1 corresponding to when the brain region presents a value higher than its mean in the BOLD signal and -1 when it has a lower value, in this way we associate a state of net spin of the network to each state of brain activation. The interaction between brain regions is considered linear and such that seeks to align neighboring nodes. This is consistent with the observation in neuroscience that regions that are intensely connected to other tend to exhibit coactivation patterns.

### Model

The interaction rule between nodes, and the associate energy for each activation pattern of the brain network are established by the next hamiltonian:

$$H = \frac{1}{2}\Theta \sum_i S_i - \frac{1}{2}W \sum_{i,j}C_{i,j}S_iS_j$$

where $S_i$ are the activation state of the node i, $\Theta$ the energy cost associate with the activation of the brain region, **W** the global coupling of the network and **T** the parameter that modulate the magnitude of thermal noise.

Once established a hamiltonian, we use de Maximum Entropy Principle to infer probability of ocurrency of the brain states, this resulted in the next expression

$$P_i = \frac{e^{-\frac{H_i}{T}}}{Z}$$

with this, the ensemble of brain states are defined, and the correlation between states of brain regions in the ensemble can be calculated. For the numerical approximation of this correlations we used a monte carlo approach, in particular the metropolis hasting algorithm.

### Entropy and maximum similarity with the empirical correlations
Once established the model its neccesary found the optimal parameters that allow us simulate the functional connectivity, for this reason we run multiple simulations with different temperatures and compare their entropys and similarity with the empirical correlations.

![image](https://github.com/JuanHigueraC/Statistical-mechanics-and-network-science-for-the-simulation-of-injuries-in-the-human-brain/blob/71824983dc0aa48b80b9d9114c417e11c25605e5/Images/FC%20with%20differents%20temperatures.PNG)

**Figure 6. Simulated functional connectivity with different temperatures.**

![image](https://github.com/JuanHigueraC/Statistical-mechanics-and-network-science-for-the-simulation-of-injuries-in-the-human-brain/blob/71824983dc0aa48b80b9d9114c417e11c25605e5/Images/entropy%20and%20fit.PNG)

**Figure 7. Entropy values for different temperatures. The vertical red line point to the value in which the similarity with empirical correlations are maximum.**

As show, the maximum similarity between simulated and empirical correlation its presented in the maximum entropy regime, just at the edge of criticality.

## Selected regions to injurie
Using network topological measures we quantified integration and segregation of the brain regions, and then we selected six brain regions to injurie, this regions was:

**L Superior Frontal Gyrus** This region was the most important in degree and betweenness centrality.

**L and R Superior Parietal Gyrus** This regions was the second and third regions with most betwennes centrality and are within the top five in the Degree rank.

**L Lateral Remainder Occipital Lobe** This region was selected because have the most correlations with the rest of the network and are within the top three in Eigenvector Centrality rank.

**L posterior temporal lobe** This region was selected because have the biggest value in Eigenvector Centrality and have hight values in other measures of centrality.

So far, all regions are selected because ther integrator properties. The next region was selected by their segregator properties.

**L Cuneus** This region was very interesting because have a hight Clustering and a hight Eigenvector Centrality, for this reason was selected.


## Results

### Simulated correlations 

![image](https://github.com/JuanHigueraC/Statistical-mechanics-and-network-science-for-the-simulation-of-injuries-in-the-human-brain/blob/5e9f812ad425e84a212ffc13522cc873b617c639/Images/FC%20with%20lesions.PNG)

**Figure 8. Simulated functional connectivity before and after the simulated local brain injuries.**

In this statistical mechanical model of brain states, local brain injurie has a effect in the global activity, this can see in the change of correlations(color) in the functional connectivity matrix after the injurie. Note that not all injuries affected the global correlations in the same way.

### Conclusions

**1.** Through the definition of links such as the number of nerve tracts, the tractography algorithm reproduces the structure of communities for the two hemispheres of the brain, and is also capable of predicting, with respect to topological measurements of the structural network, a large part of the most important nodes in functional activity at rest. This thus reflects part of the direct relationship between the structural environment with the count of tracts, and the dynamics of the brain described with linear correlations.

**2.** It can be concluded that the Ising model applied to the structural matrix is ​​a valid approach that reflects the main characteristics that the brain at rest acts as a maximum entropy system. However, given the complexity of the study system, a greater computational capacity and an approach that can integrate a greater number of characteristics of brain connectivity, such as the size of the brain regions, as well as an approach from the point of view of action potentials with the local chemical environment, so that the modeling more accurately reflects brain behavior.

**3.** Of the measures considered, it was found that geodesic intermediation in the structure is the one that best predicts which injury will have the most impact at the functional level, consistent with what is reported in the literature. However, what was observed with the functional graph for intermediation was that this measure fails to quantify aspects of brain functioning with certainty, because the intermediation measure has a nature immersed in the structural connectivity of the system, where the importance of the nodes based on their position, but for this case, in functional connectivity two regions can be correlated regardless of their distance in the cortex.

**4.** Of the lesions considered, those in the parietal gyrus were determined to be the most impactful and those in the left cuneus as the least impactful. Injuries can affect the properties of the network in different ways, increasing or decreasing integration or segregation depending on the topological properties of the injured nodes.

**5.** After injury, the entropy tended to increase, this is related to a decrease in the restrictions on the possible states of the system. However, this behavior should be further evaluated with more diverse and larger lesions. It is necessary to improve the sensitivity of the entropy measure if we want to distinguish more clearly between lesions, using, for example, another parcelling, more iterations or directly another way of calculating entropy.

## References

**[1]** Gustavo Deco, Mario Senden, and Viktor Jirsa. How anatomy shapes dynamics: a semianalytical study of the brain at rest by a simple spin model. Frontiers in computational
neuroscience, 6:68, 2012.

**[2]** Mario Senden, Gustavo Deco, Marcel A De Reus, Rainer Goebel, and Martijn P Van
Den Heuvel. Rich club organization supports a diverse set of functional network
configurations. Neuroimage, 96:174–182, 2014.

**[3]** Gustavo Deco and Maurizio Corbetta. The dynamical balance of the brain at rest.
The Neuroscientist, 17(1):107–123, 2011.

**[4]** Joana Cabral, Etienne Hugues, Olaf Sporns, and Gustavo Deco. Role of local network
oscillations in resting-state functional connectivity. Neuroimage, 57(1):130–139, 2011.

**[5]** Olaf Sporns. Networks of the Brain. MIT press, 2010.

**[6]** Hannelore Aerts, Wim Fias, Karen Caeyenberghs, and Daniele Marinazzo. Brain
networks under attack: robustness properties and the impact of lesions. Brain,
139(12):3063–3083, 2016.

**[7]** TK Das, Pubuditha M Abeyasinghe, JS Crone, A Sosnowski, S Laureys, AM Owen,
and A Soddu. Highlighting the structure-function relationship of the brain with the
ising model and graph theory. BioMed research international, 2014, 2014.


**[8]** Miguel A Munoz. Colloquium: Criticality and dynamical scaling in living systems.
Reviews of Modern Physics, 90(3):031001, 2018.

**[9]** oss M Lawrence, Eric W Bridgeford, Patrick E Myers, Ganesh C Arvapalli, Sandhya C Ramachandran, Derek A Pisner, Paige F Frank, Allison D Lemmer, Aki Nikolaidis, and Joshua T Vogelstein. Standardizing human brain parcellations. Scientific
data, 8(1):1–9, 2021.

**[10]** Karl J Friston. Functional and effective connectivity in neuroimaging: a synthesis.
Human brain mapping, 2(1-2):56–78, 1994.


**[11]** Angélica Gelover-Santiago. Simulación del modelo de Ising con el método de Monte
Carlo. Facultad de Ciencias, UNAM, 2 edition, 2005


