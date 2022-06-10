---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: page
title: The Reduced
permalink: /RRISA_reduced/
---

<h1>Reduced Data Products</h1>
All of the existing IGRINS data has been hand reduced using the [(IGRINS plp)](https://github.com/igrins/plp). The Reduced version of RRISA includes different names for targets than the Raw component.
These are names that have been painstakingly corrected by manually searching through the IGRINS paper logs for handwritten coordinates and names, through SIMBAD for nomenclature corrections and coordinate offsets.
Targets that are subcomponents of systems or extended sources keep their identifier, and if not SIMBAD searchable, do not have any additional information added in the XMatch component of RRISA.
The original names for all of the targets in both the recipe files and the Raw component of RRISA remain for reference.
If users find anything that appears to be a misidentification we ask that they report it by raising a GitHub issue.

Additionally, we provide all of the SIMBAD IDs for objects observed every night in an additional file.
This file can effectively be used to search for the nights specific objects were observed for easier manipulation of the RRISA components.

<h3>Data Reduction</h3>
IGRINS reduced data have been processed with the [IGRINS Pipeline Package (PLP)](https://github.com/igrins/plp) see [Lee+ 2017](https://zenodo.org/record/845059#.Yolg-C-cawA).

The PLP optimally extracts 1D spectra, telluric corrects, and provides 2D rectified spectra for post-processing. Wavelength solutions are determined using OH emission lines, and are then refined using telluric absorption lines in the telluric standard.
Telluric standards were generally A0V stars, which are Vega corrected using a [model of the Vega spectrum](http://kurucz.harvard.edu/stars.html.) ([see the file in the PLP](https://github.com/igrins/plp/blob/master/master_calib/A0V/vegallpr25.50000resam5.npy)).

<center>
  <figure>
    <img src="/images/trappist-1_CO.png" alt="The Trappist-1 CO lines as seen by IGRINS plotted with muler."/>
    <figcaption>A snippet of the Trappist-1 CO absorption lines from an IGRINS spectra reduced using IGRINS PLP and plotted using muler.</figcaption>
  </figure>
</center>

The PLP outputs several files for each reduction:
1. **spec_A0v.fits:** The target spectrum telluric corrected by the Vega corrected A0V. This FITS file includes the original data used to create the reduced spectrum. Each extension is a 2048x28 array with the same header. The differences between each of the EXTNAMEs are:
  - _[0]-Primary:_ The corrected target spectrum = (TGT_SPEC/A0V_SPEC)*VEGA_SPEC
  - _[1]-Wavelength:_ The wavelength solution - in um (so 1.42um for instance)
  - _[2]-TGT_SPEC:_ The extracted target spectrum (from the target spec.fits file)
  - _[3]-A0V_SPEC:_ The extracted A0V spectrum (from the A0V spec.fits file)
  - _[4]-VEGA_SPEC:_ A model of the Vega spectrum ([see the file in the PLP](https://github.com/igrins/plp/blob/master/master_calib/A0V/vegallpr25.50000resam5.npy) or for more detailed info regarding the file see this [link](http://kurucz.harvard.edu/stars.html)).
2. **sn.fits** (for both target and A0): Signal-to-Noise per pixel matching to the spec.fits output.
3. **variance.fits** (for both target and A0): Variance per pixel matching spec.fits output.
4. **spec.fits** (for both target and A0): The source spectrum. It says the spectral unit is ADUs.
5. **spec_flattened.fits** (A0): The flattened A0 spectrum.
6. **spec2d.fits** (for both target and A0): the two dimension spectrum
7. **var2d.fits** (for both target and A0): the two dimensional variance
8. **wave.fits** (for both target and A0): The vacuum wavelength solution for a given source, in nm (so 1429nm for instance).

The wavelength solutions for PLP reduced spectra are derived in a multi-step process.
Originally, IGRINS had a calibration unit installed that permitted nightly observations of ThAr arc lamps for wavelength calibration.
Since IGRINS has no moving optics, it has a fixed spectral format that changes on the order on <1 pixel per night and <5 pixels over a year.
The calibration unit still provides wavelength calibration for IGRINS in the laboratory.
In the RRISA reduced files the wavelength solution comes from an initial guess based on the historical wavelength solution.
This initial guess is then refined using sky OH emission features in a 300s SKY frame taken each night on the telescope.
SKY frames from adjacent nights also provide reliable wavelength solutions.
The wavelength solution is further refined by using telluric absorption features in the A0V standard at wavelengths greater than 2.1μm.
The dependence of the refinement on the telluric A0V means that the wavelength solution for each target is that copied from the telluric star.

The telluric standard is divided by a Vega model to remove the deep and broad H2 absorption features in the A0V - leaving behind the telluric spectrum.
This process is not perfect and can leave residual features due to differences in the line widths and radial velocities of the telluric stars relative to the Vega model. When using PLP data for science pertaining to individual line strengths, users should compare the spectrum to that of the A0V, the Vega model and [the Earth transmittance spectrum](https://psg.gsfc.nasa.gov/index.php). If the spectrum has significant telluric residuals, we provide Python based tools on the Tutorial page for how to help remove these features. If the spectrum has excess A0V residuals, the Vega model and A0V spectrum from the PLP can be used to perform an improved telluric correction. Additional A0V observations from the same night might also improve corrections.

__*Note:*__ _The output files from the IGRINS PLP are an in vacuum wavelength solution. Fit models are offset from expected line positions by 80-120 km/s the models are likely in air and not vacuum. The IAU standard conversion for air to vacuum wavelengths is given by [Morton 1991](https://ui.adsabs.harvard.edu/abs/1991ApJS...77..119M/abstract). For vacuum wavelengths (VAC) in Angstroms and convert to air wavelength (AIR) via:_
<center>
<em>AIR = VAC / (1.0 + 2.735182E-4 + (131.4182 / VAC^2) + (2.76249E8 / VAC^4))</em>
</center>

<h3>RRISA Reduced</h3>
Downloadable from [our GitHub](https://github.com/IGRINScontact/RRISA.git) as a .csv or .xlsx. Users can also view through [Google Drive](https://docs.google.com/spreadsheets/d/1RCxGboICnKQeD1suKG6CeGgSrZLGFYbiuVFF_uxNbUg/edit?usp=sharing) or [explore the RRISA_v0 folder on Box](https://utexas.box.com/v/RRISA-v0-July2014-May2021)!!

For a more detailed description of the Reduced RRISA header, check out the readme.md in the RRISA Reduced folder on [our GitHub](https://github.com/IGRINScontact/RRISA.git).
