# Pre-computed Selection Function for APOGEE DR17

Welcome! This is a small repository containing the **final selection function for the APOGEE survey**, along with some simple tutorials for how to apply it for your science case. 

If you have any questions, please reach out to me at [jimig@nmsu.edu](mailto:jimig@nmsu.edu)!


### Included Files
- `apogeeCombinedSF.dat` - the pre-computed raw (2D) selection function for APOGEE DR17 computed on *Decemer 16, 2022*.
- - Unfortuneately the selection function is TOO LARGE (4 GB) to host on github. Until I find a better location, you can download it [at this google drive](https://drive.google.com/drive/folders/1n-Twev-qElrCmVsKu5_OUMyS3j9_d0nV?usp=share_link).
- - **There is a minor known issue for 14 (out of 1937) fields in this selection function. A fix coming soon!!**
- `TUTORIAL1.ipynb` - a jupyter notebook tutorial for how to work with the raw selection function.
- `TUTORIAL2.ipynb` - a jupyter notebook tutorial for how to calculate the effective (3D) selection function from the raw selection function.

Additional Files Coming Soon: 

- `effective_selfunc.dat` (coming soon!) - the pre-computed effective selection function used in Imig et al. 2023 (in prep)


### Important Caveats
- **This selection function is only valid for APOGEE main survey targets**, stars that were targeted randomly from 2MASS. You can easily select main survey targets in the APOGEE `allStar` file using the criterion `allStar['EXTRATARG']==0`. Do not use this selection function for non-main survey targets, as it will be an underestimate of the true selection fraction for those stars.
- Some of the halo stars were not targeted on 2MASS photometry, but on additional Washington+DDO51 photometry [(more detail found here)](https://www.sdss4.org/dr17/irspec/targets/). Therefore, the 2MASS-based selection function here may not be accurate for all halo fields. If you plan to use this selection function to study the Galactic halo, be cautious of this! In most cases, this results in an overestimate of the selection fraction for halo fields, in a few cases even exceeding 100%. Relevant stars are flagged with the `APOGEE_TARGET1` targeting bits `APOGEE2_WASH_GIANT` or `APOGEE2_WASH_DWARF` ([documented more here](https://www.sdss4.org/dr17/irspec/apogee-bitmasks/#APOGEE2_TARGET1:APOGEE2targetingbitmask(1of3))) to easily identify the affected fields.


### How to Cite

If you use this selection function for published work, please cite Imig et al. 2023 (in prep) for this selection function, and [Bovy et al. 2016a](https://ui.adsabs.harvard.edu/abs/2016ApJ...823...30B/abstract) or [Bovy et al. 2016b](https://ui.adsabs.harvard.edu/abs/2016ApJ...818..130B/abstract) for the original `apogee` code used to calculate the selection function.

# Raw Selection Function

The **raw selection function**, which I like to think of as the 2D selection function, reflects the targeting strategies of APOGEE. Targets in APOGEE were selected randomly from the 2MASS catalog<sup>1</sup>, so the raw selection function is the ratio of the **number of observed stars in APOGEE** divided by the **total number of possible targets in 2MASS**, for each location on the 2D sky (APOGEE field).

1: This description is a vast oversimplification of the targeting strategies! For more detail, see the [APOGEE targeting webpage](https://www.sdss.org/dr17/irspec/targets/), or the citations [Zasowski et al. 2013](https://ui.adsabs.harvard.edu/abs/2013AJ....146...81Z/abstract), [Zasowski et al. 2017](https://ui.adsabs.harvard.edu/abs/2017AJ....154..198Z/abstract), [Beaton et al. 2021](https://ui.adsabs.harvard.edu/abs/2021AJ....162..302B/abstract), and [Santana et al. 2021](https://ui.adsabs.harvard.edu/abs/2021AJ....162..303S/abstract)

![Raw Selection Function](https://i.imgur.com/mrVAqCR.png)
*Figure 1: The raw selection function for APOGEE, showing the selection fraction of observations for each APOGEE field (location on the sky). Near the plane of the disk, the selection fraction is generally low, simply because there are more stars in those fields. Near the galactic poles in the halo, the selection fraction is generally high.*

# Effective Selection Function

The **effective (or 3D) selection function** is the ratio of the **observed number of stars in APOGEE** divided by the **intrinsic number of stars in the Milky Way** as a function of 3D Heliocentric position. This includes the effects of the raw selection function, with some additional ingredients of distances, isochrones (to assume some intrinsic distribution on the HR diagram) and a 3D Milky Way dust map. **This is a more complex application of the selection function and will largely depend on your planned science case.** 

For example, you may want to split up the effective selection for different metallicities (as done in [Mackereth & Bovy 2020](https://ui.adsabs.harvard.edu/abs/2020MNRAS.492.3631M/abstract)), or by both metallicity and stellar ages (as in [Mackereth et al. 2017](https://ui.adsabs.harvard.edu/abs/2017MNRAS.471.3057M/abstract)). You may want smaller or larger sized bins than adopted by previous work, or a different range of distances sampled. Depending on how you define your data sample in APOGEE (cuts in surface gravity, kinematics, etc.), this should also be reflected in the effective selection function for best results.  

![Effective Selection Function](https://i.imgur.com/fhIBdqG.png)

*Figure 2: The effective selection function for APOGEE, showing the selection fraction along different lines of sight. Generally, the selection fraction is larger close to the Sun, and decreases with distance.*

# Other Useful Resources

A collection of additional resources related to the APOGEE selection function.

### SDSS Webpages
- [APOGEE Targeting Description](https://www.sdss.org/dr17/irspec/targets/)
- [APOGEE Selection Function Description](https://www.sdss4.org/dr17/irspec/targets/selection-biases/)

### Papers Using the Selection Function (not a complete list!)
- [The Stellar Population Structure of the Galactic Disk (Bovy et al. 2016a)](https://ui.adsabs.harvard.edu/abs/2016ApJ...823...30B/abstract)
- [On Galactic Density Modeling in the Presence of Dust Extinction (Bovy et al. 2016b)](https://ui.adsabs.harvard.edu/abs/2016ApJ...818..130B/abstract)
- [Effects of the selection function on metallicity trends in spectroscopic surveys of the Milky Way (Nandakumar et al. 2017)](https://ui.adsabs.harvard.edu/abs/2017A%26A...606A..97N/abstract)
- [The age-metallicity structure of the Milky Way disc using APOGEE (Mackereth et al. 2017)](https://ui.adsabs.harvard.edu/abs/2017MNRAS.471.3057M/abstract)
- [Weighing the stellar constituents of the galactic halo with APOGEE red giant stars (Mackereth & Bovy 2020)](https://ui.adsabs.harvard.edu/abs/2020MNRAS.492.3631M/abstract)
- [The Milky Way tomography with APOGEE: intrinsic density distribution and structure of mono-abundance populations (Lian et al. 2022)](https://ui.adsabs.harvard.edu/abs/2022MNRAS.513.4130L/abstract)

### Additional code repositories & tutorials
- https://github.com/jobovy/apogee: original `apogee` code for computing the raw selection function
- https://github.com/jobovy/mwdust: repository containing several 3D dust maps for computing the effective selection function
- https://github.com/jmackereth/halo-mass: code for reproduction of [Mackereth & Bovy 2020](https://ui.adsabs.harvard.edu/abs/2020MNRAS.492.3631M/abstract)
