---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: page
title: The Raw
permalink: /RRISA_raw/
---

<h1>Raw IGRINS Files</h1>
The Raw component of RRISA is a list of all of the H-band frames (SDCH_[YYYYMMDD]_[frameno].fits) IGRINS has ever observed before May 2023 including flats, darks, arcs, targets, and telluric standards.
IGRINS takes H- and K-band spectra simultaneously, so each of the logged H-band frames will have K-band (SDCK_[YYYYMMDD]_[frameno].fits) companion with an identical file number.
The link corresponding to each file number will take users to a UT Box folder with all of the raw files taken on a given night which can be downloaded individually by file number or for the entire night.
Silt-viewer camera images (SDCS_[YYYYMMDD]_[frameno].fits) for acquisition and guiding are not currently avalible for download through RRISA.
If a user would like to obtain the slit-viewer camera images for a particular night they can reach out to the IGRINS team directly.
*Please note that the slit-viewer camera images are not appropriate for photometry.*

Some spectral files are not suitable for science. For example - exposures interrupted by weather, frames with incorrect exposure times, or mislabeled frames.
RRISA includes all of the night logs (digital and paper) for the IGRINS observations which can be found [here](https://utexas.box.com/s/wnkqbgf5atxx1hy1ejiou1r2avdcx4c3).
We _highly recommend_ that users of the Raw archive consult the night logs for all observations to confirm which frames are suitable for science if users choose to reduce IGRINS raw data using their own pipeline.

An example of the raw spectral frames for the IGRINS H- and K-band spectra can be seen below.

<center>
  <figure>
    <img src="/images/IGRINS_on_chip.png" alt="IGRINS H and K Band on Chip Spectra"/>
    <figcaption>An example of an AB sky-subtracted echellogram of an emission line source observed with IGRINS for both H and K Band. Each IGRINS order forms one of the curved rows we see in the images, the orders are curved before they are rectified (straightened) by a reduction pipeline. Within each order the x-axis is the dispersion direction and the y-axis is roughly the position on the slit. Wavelength increases from left to right within each order and from top to bottom on the echellogram. The position of different excited states of molecular hydrogen are annotated on both of the echellograms.</figcaption>
  </figure>
</center>

The IGRINS slit dimensions (width x length) in arcseconds are 0.34x5 at Gemini South, 0.63x9.3 at Lowell’s Discovery Telescope, and 1x15 at McDonald Observatory.
Point sources (anything with a seeing limited image on the slit-viewer) are generally observed in two positions on the slit.
The two positions, A and B, are separated by half a slit length.

__*Note:*__ _Data acquired between April 2018 and May 2019 was impacted by a slight K-band defocus. The details of the defocus are available at [the IGRINS@Gemini webpage](https://sites.google.com/site/igrinsatgemini/2018-k-band-resolution)._

<h3>RRISA Raw</h3>

Downloadable from [our GitHub](https://github.com/IGRINScontact/RRISA.git) as a .csv. Users can also view through [Google Drive](https://docs.google.com/spreadsheets/d/1_3g4A6mzZj2BrMh821_DAExuZAhACohHGKobc0Tn9ME/edit?usp=sharing) or [explore the RRISA_v3 folder on Box](https://utexas.box.com/s/l7i5dbtss084mhxywmc6r8pl39bs1yhw)!

For a more detailed description of the information included in RRISA Raw, check out the RRISA Raw folder on [our GitHub](https://github.com/IGRINScontact/RRISA/tree/main/RRISA_Raw).
