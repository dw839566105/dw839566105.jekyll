#### 0. Simulation  
+ Need simulation generated at different axes
> Random vertex and energy (Sim Real Situation)
> 1. Simulated particle $\alpha$, $\beta$
>> Almost finished in 5 kt, may be not need in 1t, just to demonstrate that GEANT4 is not suitable for decay time constant.
> 2. Simulated energy from 0.5 - 2.5 MeV
>> Random sampling
> 3. Simulated decay time constant
>> a. Default time profile ($\tau_d$ = 26 ns)
>> b. Energy dependent time profile ($\tau_d = f(E)$)
>>> i. Need makefile sed 'Energy' and 'Decay time constant' at the same time.
>>> ii. Makefile need a random generator when energy is not fixed.
>>> iii. An assumption of relationship between energy and $\tau_d$
>
> Fixed vertex and Energy (Templates)
>
> 4. Vertex at different position
>> a. Vertex is defined as $\vec{x} = \{r,\theta,\phi\}$
>> b. Simulated vertex is in the grid of $\{r,\theta,\phi\}$
>>> i. $r$ from $[-R,R]$, step ~ $R/50$
>>> ii. $\theta$ from $[-\pi/2, \pi/2]$, step $\pi/6$ (Need discussion)
>>> iii. $\phi$ from $[-\pi,\pi]$, step $\pi/3$
>>> iv. Energy can takes 1,1.5,2 MeV
>>> Total events $100*6*6 = 3600$
>>> Or the points are sparse in the center, but dense close to the boundry, total events < 1000.
>>> Each point 20000 beam. Per beam 1 event.
>>> Trigger: 10 PMTs. (Need to discuss when close to boundry)
>>> software: JSAP
#### 1. Program main framework: Reconstruction Program (This part is almost finished)
This part is theory.
Likelihood function is a Poisson distribution. 
$p\sim\mathrm{Poisson}(n_i,\lambda)$
+ $n_i$ is waveform reconstruction
+ $\lambda$ is expected photons to esitimate 
$\mathcal{L}=\log \prod_i p_i = \sum_i \log p_i$


##### 1.a Naive likelihood (100 %)
$\lambda_i = E\cdot Y(E) \cdot \frac{\Omega}{4\pi}\cdot \eta \cdot \exp\{-\frac{d_i}{L}\}$
##### 1.b Simulation templates (75 %)
$\lambda_i = \theta x_i $
#### 2. Processing Result (Both method)
##### Simulation data
##### 2.1 Map of Resolution Histogram
2-d Histogram $E$ vs $r$
> Simulated point at certain vertex.
##### 2.2 Map of Bias Histogram  
2-d Histogram $E$ vs $r$
> Slice of 1-d errorbar with bias and uncertainty
> * 5 kt 
>> Different energy at 0.5, 1, 2 MeV
>> Different radius at 0, 8, 10 m   
>
> * 1 t
>> Different energy at 0.5, 1, 2 MeV
>> Different radius at each step (0.01 m)

#### 3. Time infomation
$t_c = t_i - t_f - t_0 \sim \mathrm{Time\ profile}$ 
##### 3.1 Naive likelihood
Prior of time profile is known 
##### 3.2 Spherical Harmonics
+ Use template (Similar，have difficulties when photon scattered, only 1 value will be calculated but the arrive time may have many values.)
##### 3.3 Use EM
    1. Use reconstructed vertex get an prior of time distribution $E$ vs $\tau_d$
    2. Use mask as the input of next step

+ plot the energy spectrum
+ plot the $\alpha$, $\beta$ classification

##### Spherical Harmonics difficulties
    *1. difference of PMTs (calibration)
    *2. ignorance of PMTs (In simulation)