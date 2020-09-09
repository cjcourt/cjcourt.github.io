---
title: "MagneticMaterials.org"
excerpt: "A web-application for magnetic materials discovery <br/><br/><img src='/images/MLogo.png' width='150'>"
collection: projects
---

# Overview
[MagneticMaterials.org](http://magneticmaterials.org) is a web application for analysing magnetic phase transition data that I have mined using [ChemDataExtractor](cde.md).


# How it works
## Mining Magnetic Phase Transitions
The first step is to automatically mine scientific articles for the values of magnetic and superconducting phase transitions. These properties are realy important for materials used in a variety of applications, such magnetometers, regrigerators, power converion devices, spintronics and more!

Specifically, we used ChemDataExtractor to mine a corpus of 74,000 articles to create a database of 20,000 phase transitions, with an estimated precision of 82%.

## Reconstructing phase diagrams
Phase diagrams are essentially plots of a materials magnetic phase versus other interesting properties, such as composition or pressure. These diagrams tell us a huge amount about how a material will behave under different conditions, and therefore how well it will perform in applications.

Unfortunately, phase diagrams in the literature are extremely sparse, and often not very specific. Therefore, our idea was to use our database to automatically reconstruct, and ultimately predict, the phase transitions of magnetic materials.

# Results

We can see how well our tool does via some case-studies.

## Perovskite Oxides
The perovskite-type oxides are inorganic compounds with general formula $ABO_3$ where  A is a large 12-coordinated cation and B is a smaller 6-coordinated cation.
The generic perovskite structure is cubic; however, this form is rarely found due to structural deformation. These deformations cause the perovskites to exhibit a wide variety of interesting and useful properties including ferroelectricity, piezoelectricity, superconductivity and magnetism. As such, perovskite materials are found in a vast number of applications.

The properties and phase diagrams of the common perovskite series have been widely reported, and as such, these materials make great candidates as case studies to validate the performance of our database and phase-diagram phase transition prediction toolkit.

Magnetism in perovskites arises through the incorporation of paramagnetic cations. Commonly, cationic species are lanthanides or transition metals, who have partially filled d and f orbitals. Through the crystal-field interaction, local-coordination environments determine the orbital energy levels and hence the spin state and magnetic moment of the cation. The large dependence of the magnetic properties on the crystal-field interaction leads to a huge variation in magnetic state with temperature and composition. With only minor changes in doping concentration of the A-site and B-site cations, the material undergoes transitions between multiple different magnetic phases. A classic example of this is the $La_{1-x}Sr_xMnO_3$ system which displays a bulk metallic ferromagnetic phase and 4 different antiferromagnetic phases with varying Sr composition.

Using our toolkit and the excellent visualisation tools provided by [Plotly](https://Plot.ly) the auto-generated phase diagram below clearly distinguishes the ferromagnetic phase (0.1 ≤ x ≤ 0.6) and the antiferromagnetic phases (x ≤ 0.1 and x ≥ 0.5).

![LSMO](/images/lsmo.png)

## Antiferromangetic Perovskites

Antiferromagnetic interactions in perovskites originate from the superexchange mechanism. This is defined as an indirect exchange interaction between non-neighbouring magnetic cations mediated by a non-magnetic anion.

In the orthorhombic perovskite structure, which displays 180$^\circ$ superexchange, the geometry favours antiferromagnetic alignment, and thus the orthorhombic perovskites typically demonstrate a clear Néel transition. Such examples include the rare-earth orthochromite series $LNCrO_3$
where LN is a lanthanide ion. The theory of superexchange indicates that the strength of the antiferromagnetic interaction, and hence the Néel temperature of the material, depends on the degree of overlap between the cations and their mediating anion. This in turn indicates that the transition temperature should be highly dependent on the properties of the LN
 cation.

Panels (a) and (b) in the figure below show the auto-generated and reported Néel phase for the $LNCrO_3$ series. As predicted, these show a strong linear dependence of the Néel temperature on the ionic radius of the LN cation.

We note that the auto-generated diagram is missing its Ce-member, $CeCrO_3$. Making use of the available auto-generated data and machine-learning techniques, we can attempt to make a prediction of the Néel temperature, and compare this to the reported value of ~260 K.

Using the prediction and feature selection methods of the phase-transition toolkit outlined in the Methodology, we predicted the Néel temperature of $CeCrO_3$ to be in the range of 250-270 K, very close to the manually reported experimental value of 260 K. The optimal features for the model were determined to be the ionic radius and Pauling electronegativity of the LN ion, both of which can be directly related to the theory of superexchange that depends primarily on the overlap of the LN and O orbitals.

![antiferro](/images/fig_3.png)

## Rare-earth Manganites

Other antiferromagnetic perovskite oxides include the rare-earth manganite series 
$LNMnO_3$. The auto-generated Néel temperature as function of ionic radius of the LN ion is given in panel (c) above. Again, the auto-generated temperatures match closely to the values from manually curated experimental reports. However, in contrast to the orthochromites, the relationship between Néel temperature and ionic radius is non-linear for $LNMnO_3$ compounds. This non-linearity results from a structural phase transition within this series. For LN = Ho, Er, Yb, Lu the compounds typically crystallise in a stable hexagonal structure. In hexagonal perovskites the linkage between the cations can be either 180$^\circ$ or 90$^\circ$, yielding very different superexchange mechanisms to those of orthorhombic $LNMnO_3$ compounds with 
thus their different dependence on the Néel temperature. These orthorhombic compounds have similar structures and magnetic behaviour to rare-earth orthochromites, given their common crystal system.

## Barium Ferropnictides

The theory of superconductivity in Barium ferropnictides diverges from the conventional Bardeen-Cooper-Schrieffer (BCS) model in which superconductivity arises as a direct result of electron-phonon coupling. Instead, ferropnictide superconductivity is caused by electron-electron Coulomb interactions. This unconventional superconductivity is indicated in the phase diagrams of the $BaFe_{2-x}Ni_xAs_2$ class of ferropnictide materials, since the superconducting state arises near the onset of antiferromagnetic order in metals with very low electrical conductivity.
These are 1222-type superconductors and the end member $BaFe_2As_2$ exhibits antiferromagnetism up to around 140 K. Above this temperature it is a paramagnetic `bad-metal' due the high resistivity. As the $Ni$ content, x, is increased, the Néel temperature decreases until a superconductivity phase begins to emerge below 20 K. At a certain critical doping concentration $x_c = 0.07$, the antiferromagnetic and superconducting states coincide at ~40 K. For higher concentrations, the Néel phase is suppressed and superconductivity below 20 K is observed. For doping concentrations above x = 0.20, the system returns to a non-superconducting paramagnet. This is reflected clearly in the auto-generated and reported phase diagrams, shown below.

![Barium](/images/fig_5.png)

# Further Reading
The paper corresponding to this work is available [here](https://pubs.acs.org/doi/10.1021/acs.jcim.0c00464). The toolkit is [here](http://magneticmaterials.org/analysis/) and a demo of the phase diagram toolkit can be found [here](http://magneticmaterials.org/demo/)


