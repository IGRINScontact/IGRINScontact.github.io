---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: page
title: The Reduced
permalink: /RRISA_reduced/
---

<h1>Reduced Data Products</h1>
All of IGRINS data included in the Reduced version of RRISA have been reduced using the [v3 of the IGRINS PLP](https://github.com/igrins/plp/tree/v3.0.0). 
The Reduced version of RRISA includes three names for each of the targets: the hand corrected name, the superlog name which can be used to link individual files from the Raw component of RRISA its reduced counterpart and the recipe name which is the name associated with the reduced file, usually manually input often given by the observer.
The superlog name and the recipe name will not always match, but usually they are similar or alternate identifiers for the same object.
If users find anything that appears to be a misidentification we ask that they report it by raising a [GitHub issue](https://github.com/IGRINScontact/RRISA/issues) or contacting us at igrins.contact[at]gmail.com.
Finally, __not all of the reduced IGRINS data is necessarily good quality.__
_If you use the reduced data products, consult the observing logs and reach out to the IGRINS team if you have questions!_

<h3>Data Reduction</h3>
IGRINS reduced data have been processed with the [IGRINS Pipeline Package (PLP) v3](https://github.com/igrins/plp) from [Kaplan+ 2024](https://zenodo.org/records/11080095).
The PLP follows standard reduction techniques for echelle spectra including flat fielding, readout pattern removal, cosmic ray removal, combining individual exposures, rectification, and extraction of the individual echelle orders.

The PLP v3 introduces a new method of flexure correction that improves the OH sky line background subtraction and reduces the telluric residuals that appear when stacking individual frames and when dividing a target spectrum by its standard star. 
In a night of observing, we compare the location of the OH sky lines in each raw frame (with OH sky lines) used in reduction to the location of the OH sky lines in the first sky frame of the night to measure the flexure in each frame. 
After measuring the flexure in each of the frames used in the reduction, the PLP continues through the various recipe steps but both cosmic ray masks and flexure corrects the frames used in the recipe before stacking them.
An example of the difference between the new and old pipeline reduction for a night with high flexure is shown below for a few orders in K-band.

Originally, IGRINS used a calibration unit installed that permitted nightly observations of ThAr arc lamps for wavelength calibration.
Since IGRINS has no moving optics, it has a fixed spectral format that changes on the order on <1 pixel per night and <5 pixels over a year.
The wavelength solution for IGRINS data comes from an initial guess based on the historical wavelength solution.
This initial guess is then refined using sky OH emission features in a 300s sky frame taken each night on the telescope.
Sky frames from adjacent nights also provide reliable wavelength solutions and are sometimes used when no sky frame is avalible for a night.
<!---(this is apparently not true in v3 anymore) The wavelength solution is further refined by using telluric absorption features in the A0V standard at wavelengths greater than 2.1μm.
The dependence of the refinement on the telluric A0V means that the wavelength solution for each target is that copied from the associated telluric star.--->

Telluric standards are generally A0V stars, which are Vega corrected using a [model of the Vega spectrum](http://kurucz.harvard.edu/stars.html) ([see the file in the PLP](https://github.com/igrins/plp/blob/v3.0.0/master_calib/A0V/vegallpr25.50000resam5.npy), but also stored in each spec_a0v.fits file as an extension) to remove the deep and broad H2 absorption features.
This process is not perfect and can leave residual features due to differences in the line widths and radial velocities of the telluric stars relative to the Vega model.
Additionally, the model Vega spectrum is not meant for careful flux calibration science cases, but is appropriate for science cases where the target spectrum is continuum normalized.
When using PLP data for science pertaining to individual line strengths, users should compare the spectrum to that of the A0V, the Vega model and [the Earth transmittance spectrum](https://psg.gsfc.nasa.gov/index.php).
<!---
If the spectrum has significant telluric residuals, we provide Python based tools on the Tutorial page for how to help remove these features. 
If the spectrum has excess A0V residuals, the Vega model and A0V spectrum from the PLP can be used to perform an improved telluric correction. 
Additional A0V observations from the same night might also improve corrections.
--->

<center>
  <figure>
    <img src="/images/20161013_0254.png" alt="A few K-band orders reduced using the old and new pipeline."/>
    <figcaption>A comparison of the same data reduced with IGRINS PLP v2.2.0 (grey) and IGRINS PLP v3 (blue) for a few orders in K-band for V383 Lac. The flexure on this particular night was on the extreme end which caused large telluric residuals in the v2.2.0 data reduction. There are still some telluric residuals present in the v3 reduction which are likely due to a difference in airmass between the target and standard star.</figcaption>
  </figure>
</center>

The PLP v3 output has changed when compared to past versions of the PLP.
The most signification change affects the spec_a0v.fits files, where more extensions are included to reduce the number of files a user needs to keep on their device.
For consistency with legacy codes, several of the extensions in spec_a0v.fits are also included as individual files.
When downloading reduced data using RRISA, the following files are included in each zip file (for H- and K-band) corresponding to a particular file number:
1. **spec_a0v.fits:** The target spectrum telluric corrected by the Vega corrected A0V. This FITS file includes the original data used to create the reduced spectrum. Each extension is a 2048x28 array with the same header. The differences between each of the EXTNAMEs are:
  - _[0]-Primary:_ Only contains the header with information about the observation
  - _[1]-SPEC_DIVIDE_A0V:_ The corrected target spectrum = (TGT_SPEC/A0V_SPEC)*VEGA_SPEC. This spectrum is roughly telluric corrected and relatively flux calibrated.
  - _[2]-SPEC_DIVIDE_A0V_VARIANCE:_ The variance of SPEC_DIVIDE_A0V (per pixel) propgated from the variance in the individual target and standard spectrum.
  - _[3]-WAVELENGTH:_ The wavelength solution from the OH sky lines (in um)
  - _[4]-TGT_SPEC:_ The extracted target spectrum (same as in spec.fits file)
  - _[5]-TGT_SPEC_VARIANCE:_ The variance of TGT_SPEC (per pixel).
  - _[6]-A0V_SPEC:_ The extracted A0V spectrum used for the standard star division. The observation ID (file number) for the A0V used is avalible as the 'OBSID' keyword in the header for this extension.
  - _[7]-A0V_SPEC_VARIANCE:_ The variance of A0V_SPEC (per pixel).
  - _[8]-VEGA_SPEC:_ A model of the Vega spectrum ([see the file in the PLP](https://github.com/igrins/plp/blob/master/master_calib/A0V/vegallpr25.50000resam5.npy) or for more detailed info regarding the file see this [link](http://kurucz.harvard.edu/stars.html)).
  - _[9]-SPEC_DIVIDE_CONT:_ Similar to SPEC_DIVIDE_A0V, but the target spectrum is divided by the estimated continuum of the A0V star instead of the A0V spectrum itself. The resulting spectrum is relativly flux calibrated but _not_ telluric corrected.
  - _[10]-SPEC_DIVIDE_CONT_VARIANCE:_ The variance of SPEC_DIVIDE_CONT (per pixel).
  - _[11]-MASK:_ The pixels used in the A0V star continuum fit for SPEC_DIVIDE_CONT. A value of 1 is not used in the continuum fit.
2. **sn.fits:** The signal-to-noice (per resolution element) for the extracted 1D spectrum. We reccomend using .variance.fits for the uncertainty. Columns are x pixel position on the detector and rows are echelle orders.
3. **spec.fits:** The extracted 1D spectra. Columns are x pixel position on the detector and rows are echelle. The pixel values are the extracted counts.
4. **spec2d.fits:** The 2D spectrum stored as a data-cube of the rectified echelle orders. The x-axis is pixel across the detector and y-axis is the spatial axis along the IGRINS slit. The pixel values are detector counts.
5. **var2d.fits:** The variance (per pixel) of the 2D spectrum. The x-axis is pixel across the detector and y-axis is the spatial axis along the IGRINS slit.
6. **variance.fits:** Variance for the 1D spectra in spec.fits. Columns are x pixel position on the detector and rows are echelle order. The pixel values are the extracted counts.
7. **slit_profile.json:** The average measured slit profile for a target AB nodded on the slit. The array labeled "profile_x" is the fractional distace across the slit and "profile_y" is the slit profile of the target. This is the slit profile used for optimal extraction explained more [here](https://github.com/igrins/plp/wiki/One-dimensional-spectra-extraction).
8. **1d_plots.pdf:** The SPEC_DIVIDE_A0V extension of spec.a0v.fits plotted by order. The y-axis limits of each order are set using the 99th flux percentile of the trimmed order, but usually this is not ideal for anything other than quick-looking the quality of the telluric correction. 

There are additional files output by the IGRINS PLP avalible upon request detailed [here](https://github.com/igrins/plp/wiki/PLP-Data-Reduction-Products).

<!---
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
--->

__*Note:*__ _The output files from the IGRINS PLP are an in vacuum wavelength solution. Fit models are offset from expected line positions by 80-120 km/s the models are likely in air and not vacuum. The IAU standard conversion for air to vacuum wavelengths is given by [Morton 1991](https://ui.adsabs.harvard.edu/abs/1991ApJS...77..119M/abstract). For vacuum wavelengths (VAC) in Angstroms and convert to air wavelength (AIR) via:_
<center>
<em>AIR = VAC / (1.0 + 2.735182E-4 + (131.4182 / VAC^2) + (2.76249E8 / VAC^4))</em>
</center>

<!---
<h3><b>New in RRISA v1: Rtell Data Products & File Format</b></h3>

<center>
  <figure>
    <img src="/images/SZ_Cha_rtell.png" alt="A comparison between the original IGRINS data product and the rtell IGRINS data product for SZ Cha."/>
    <figcaption>A comparison between the SZ Cha IGRINS spectrum from the IGRINS PLP and from rtell. The IGRINS PLP spectrum is shown in black and the rtell spectrum is shown in red.</figcaption>
  </figure>
</center>

The rtell data products take the original reduced spectra output from the IGRINS PLP and improve the pixel alignment between the A0V standard star spectrum and the target spectrum using a strong telluric sky line (between 16452-16458 and 21740-21752 Angstroms in H- and K-Band respectively) featured in the spectra.
We identify the center of the telluric feature in both the standard and target spectra by fitting a gaussian.
The shift between the two centers is identified and the standard star spectrum is shifted in pixel space to align with the center of the target spectrum.
The rtell spectrum is produced by dividing the original target spectrum by the shifted standard spectrum and multiplying by the Vega model.
Unlike the IGRINS PLP data products, the divided spectrum, wavelength solution, target spectrum, shifted standard spectrum, Vega model, and SNR per resolution element are available in one FITS file as separate extensions.
Additionally, when an rtell file is available for an object, we provide three additional files in RRISA:
1. plots showing the initial sky-line gaussian guess and the final gaussian fit for the telluric line in the target spectrum
2. plots showing the initial sky-line gaussian guess and the final gaussian fit for the telluric line in the standard spectrum (see Figure below)
3. a text file with information about both the target and standard spectrum, the shift implemented, and the filename for the rtell spectrum

<center>
  <figure>
    <img src="/images/SZ_Cha_standard.png" alt="The standard star spectrum telluric line fits for an SZ Cha rtell file."/>
    <figcaption>The K-Band telluric feature fits for a standard star used in an SZ Cha IGRINS rtell reduction. The right shows the 'close' initial priors fed into scipy.curve_fit, the left shows the final gaussian from scipy.curve_fit with the center pixel labeled in the legend.</figcaption>
  </figure>
</center>

The new rtell file is supported through the most recent version of [muler](https://github.com/OttoStruve/muler) and we provide the code that produces the rtell data products for reference in the rtell folder in the RRISA repository.
--->

<h3>RRISA Reduced</h3>
Downloadable from [our GitHub](https://github.com/IGRINScontact/RRISA.git) as a .csv. Users can also view through [Google Drive](https://docs.google.com/spreadsheets/d/1ZTmKkj0kcbhqytVKipsXUQKgHRDkYTIiN4yyNEH3lAM/edit?usp=sharing) or [explore the RRISA_v3 folder on Box](https://utexas.box.com/s/l7i5dbtss084mhxywmc6r8pl39bs1yhw)!

For a more detailed description of the information included in RRISA Reduced, check out the the RRISA Reduced folder on [our GitHub](https://github.com/IGRINScontact/RRISA/tree/main/RRISA_Reduced).
