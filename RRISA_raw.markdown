---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: page
title: The Raw
permalink: /RRISA_raw/
---

<h1>Raw IGRINS Files</h1>
The Raw component of RRISA includes all of the frames IGRINS has ever observed before May 2021 including Flats, Darks, Arcs, Targets, and Telluric Standards.
Additionally, this includes the slit-viewer images from acquisition and guiding.
Some spectral files are not suitable for science. For example - exposures interrupted by weather, frames with incorrect exposure times, or mislabeled frames.
RRISA includes all of the night logs (digital and paper) for all of the IGRINS observations.
We highly recommend that users of the Raw archive consult the night logs for all observations to confirm which frames are suitable for science.

<h3>IGRINS Observations</h3>
Raw data from IGRINS includes the ‘SDCS’ slit-viewer images, ‘SDCH’ two-dimensional H-band echellogram, and ‘SDCK’ two-dimensional K-band echellogram.
IGRINS simultaneously observes the H and K spectra, and file numbers match for the two bands.
Slit-viewer images are generally saved during target acquisition and guiding.
The slit-viewer images are compressed to save hard drive space and are not appropriate for photometry.
The raw spectral frames for the IGRINS H- and K-band spectra can be seen below.

<center>
  <figure>
    <img src="/images/IGRINS_on_chip.png" alt="IGRINS H and K Band on Chip Spectra"/>
    <figcaption>An example of an AB sky-subtracted image of an emission line source observed with IGRINS
    for both H and K Band. Wavelengths increase from left to right and from top to bottom.</figcaption>
  </figure>
</center>

The IGRINS slit dimensions (width x length) in arcseconds are 0.34x5 at Gemini South, 0.63x9.3 at Lowell’s Discovery Telescope, and 1x15 at McDonald Observatory.
Point sources (anything with a seeing limited image on the slit-viewer) are generally observed in two positions on the slit.
The two positions, A and B, are separated by half a slit length.

__*Note:*__ _Data acquired between April 2018 and May 2019 was impacted by a slight K-band defocus. The details of the defocus are available at [the IGRINS@Gemini webpage](https://sites.google.com/site/igrinsatgemini/2018-k-band-resolution )._

<h3>RRISA Raw</h3>

Downloadable from [our GitHub](https://github.com/IGRINScontact/RRISA.git) as a .csv or .xlsx. Users can also view through [Google Drive](https://docs.google.com/spreadsheets/d/1jqbt4-Qqula0TP_iJfw7BqiYPfOMnCWdc5JiovziYp0/edit?usp=sharing) or [explore the RRISA_v0 folder on Box](https://utexas.box.com/v/RRISA-v0-July2014-May2021)!

For a more detailed description of the Raw RRISA header, check out the readme.md in the RRISA Raw folder on [our GitHub](https://github.com/IGRINScontact/RRISA.git).
