# The Experiment
As mentioned previously, the data collected comes from a UCDenver gamma spectroscopy lab. The lab involved taking data using a **spectrometer** which is fed from first a **scintillator** and a **photomultiplier tube** (PMT) to record the energy levels emitted by various radioactive sources. Let's go over the process of gamma decay as well as describe what the related instruments are so that you can understand better the data that we're looking at when we start plotting it.
## Gamma Decay
There are three main types of radioactive decay associated with emissions, alpha ($\alpha$), beta ($\beta$), and gamma ($\gamma$), named in increasing order of their matter-penetrating abilities. These three types of emissions are noteable also for their ability to be differentiated inside of an electromagnetic field. Radioactive decay can be observed in **all** isotopes of **all** elements of equal or greater atomic mass than bismuth.

1. Alpha ($\alpha$) Decay

This type of decay results in a postively charged **alpha particle**, consisting of two protons and two neutrons (a helium nucleus) being ejected from the nucleus of a heavier element (usually). This type of radiation is the least penetrating, stopped by centimeters of air, but is also the most destructive form of ionizing radiation. Because of their low penetrating power however, they are generally only harmful to life if the radioactive source is swallowed or inhaled.

2. Beta ($\beta$) Decay

This type of decay results in a negatively charged **beta particle**, which can be a high-speed electron ($\beta^-$ decay), or its antimatter counterpart the positron ($\beta^+$ decay). This type of radiation is inbetween the other two in terms of both ionization and penetrative power.

3. Gamma ($\gamma$) Decay 

Unlike the other two, gamma decay doesn't release a particle with mass, it instead releases electromagnetic radiation in the form of a **photon**, which has no charge. It differs from other forms of electromagnetic radiation that you may be familiar with (such as visible light or x-rays) only in that they have the shortest wavelengths and thus the highest energies of light. Gamma radiation has many possible sources, but in particle physics it normally occurs **after** a nucleus undergoes one of the other two types of decay. This decay leaves the nucleus in an excited state, and when the nucleons (nuclear particles) transition to a lower resting state they release one of these high energy photons. 

This transition is much like the process through which the more common types of light are emitted, where an electron will transition between energy levels and release a photon in the process. However, this transition operates using the **strong nuclear force**, producing a photon orders of magnitude more energetic than otherwise. The typical photon released through electric relaxation will be in the eV range, usually less than 100eV, while the typical photon released from an atomic nucleus will range from around 1KeV to 10MeV of energy.

Gamma radiation has the most ability to penetrate materials but is also the least ionizing of these three types of radiation.
# Instrumentation
Now that we've gone over the different types of radiation, let's go over how we can detect them experimentally, and then how we can use these detections to calibrate our instruments and determine the properties of an unknown isotope.
## Scintillator
The scintillator is the first step in our instrumentation. These devices utilize the properties of certain materials to **luminesce** when excited by radiation, causing them to **re-emit** light at a lower and more easily detectable wavelength. For gamma ray detection, photons **Compton scatter** off of electrons in the structure of the scintillator. 

Compton scattering describes the effect where high-energy photons interact with loosely-bound valence shell electrons, giving them enough energy to be released from their atoms, ionizing the atom in the process. Those free electrons then scatter off of other electrons, spreading the energy of the inital gamma ray across multiple electrons. As each of these electrons relax and are recaptured by the ionized atoms, they then release photons at a lower energy.

It is by this process that one high energy gamma ray can be turned into several lower energy photons which can then be detected using the second instrument in the experiment.
## Photomultiplier Tube (PMT)
A PMT is an incredibly sensitive photon detector, and they are normally designed to detect light specifically in the ultraviolet, visible, and near-infrared ranges of the electromagnetic spectrum (which is why we need the scintillator to step-down our photon energies).

They are typically constructed using an evacuated glass housing with a **photocathode** on one end which is engineered to use the **photoelectric effect**. This again uses light to release electrons, but now in the presence of an electric field. The electric field then accelerates the released electrons towards the back of the PMT, and along the way the electrons will strike against arrays of **dynodes**.

Each dynode has a higher potential difference (voltage) than the previous one, and they are designed so that with each electron that strikes them they release several more. This causes an exponential cascade of electrons to course through the system until they finally reach the **anode** at the end of the PMT. Here, the cascade of electrons results in a current which can be detected using a device such as an oscilloscope, or a spectrometer in the case of this experiment, and the results can then be recorded.
## Spectrometer
"Spectrometer" is a fairly broad class of instruments used for detecting and measuring the spectal components of light. The one used for this experiment was a **Universal Computer Spectrometer** (UCS). The UCS is the final component in the detection chain and serves as the interface between the analog signal produced by the PMT and the digital data we will analyze. This type of spectrometer is called "universal" as it can be configured for a wide range of radiation detection experiments, and "computer" as it can be integrated with a digital system capable of **binning**, **processing**, and **storing** pulse data. 

It works by monitoring the voltage pulses generated at the anode of the PMT. Each pulse corresponds to a single photon event detected by the scintillator and converted to a current by the PMT. The one used in this experiment contained 2048 **channels**, with the higher channels corresponding to higher detected currents.
# Data Analysis
The next step in this process is to take the data from the radioactive sources and feed them into a computer using software. As decay events occur in relation to the the associated element's half life, it is necessary to run the detection software for several minutes for each element in order to collect as much data as possible. 

After an event is measured by a specific channel, that channel's **count** number is increased by one. This eventually results in noticeable peaks which correspond with the given isotope's emission energy. 

However, due to the steps of the scintillator and PMT, it is not possible to immediately directly correlate a specific channel with a specific energy. It is because of the steps required to be able to detect the gamma rays in the first place that we must also perform significant data analysis to associate channel numbers with emission energies. The resulting relationship between channel numbers and emission energies is **linear**. Each channel should correspond to a specific range of gamma energies.

This is then limited by the fact that the gamma events aren't being fed directly into the scintillator and PMT. They are placed underneath the detector setup and then allowed to radiate spherically. Some of these emissions will hit the detectors with a glancing blow, meaning that they'll have less detected energy than the others, while a small amount of particles actually **will** be sent straight up the detector, resulting in a higher detected energy than average. This distribution of energies will result in a **Gaussian curve**, where the center of the curve will correspond to the average detected energies of the emitted particles, but with a margin of error.

So, in order to determine what element our unknown radioactive source is, it will be necessary to first perform a curve fit for each one of the peaks detected, and then use the known values for their emissions to perform a second curve fit to relate the channel numbers with their actual energies. 

---

Let's get going, then! [Click here to continue to the next section](04_data_analysis.md) where we'll learn how to use the `scipy` library to perform these curve fits.