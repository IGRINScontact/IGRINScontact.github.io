---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: page
title: The XMatch
permalink: /RRISA_xmatch/
---

<h1>Reduced & Crossmatched</h1>
For objects in the IGRINS sample that are searchable via SIMBAD, we cross-match with other catalogs to provide additional target information.
In RRISA v3 we support cross-matching with [2MASS](https://ui.adsabs.harvard.edu/abs/2003yCat.2246....0C/abstract), [APOGEE-2 DR17](https://ui.adsabs.harvard.edu/abs/2022ApJS..259...35A/abstract), [Gaia DR3](https://ui.adsabs.harvard.edu/abs/2023A%26A...674A...1G/abstract), and [PASTEL](https://ui.adsabs.harvard.edu/abs/2016A%26A...591A.118S/abstract).
For a more detailed description of the catalog information included in RRISA XMatch, check out the [RRISA_XMatch folder on our GitHub](https://github.com/IGRINScontact/RRISA/tree/main/RRISA_XMatch).
*Objects like subcomponents of multiple systems, unamed stars in crowded fields, planets, or other objects observed with IGRINS that are not searchable in SIMBAD are not present in RRISA XMatch.*


<h3>Object Matching</h3>
The cross-matching for RRISA errs on the side of caution in an effort to reduce misidentification of objects.
We cross-match the IGRINS sample using [astroquery](https://astroquery.readthedocs.io/en/latest/index.html) which allows us to search astronomy catalogs via Python.
The following flowchart explains our method of cross-matching in 3 primary steps for transparancy:

<center>
  <figure>
    <img src="/images/code_flowchart_remake.png" alt="Cross-matching code flowchart" width = "600"/>
  </figure>
</center>

We start with our list of IGRINS observations with names that are searchable in [SIMBAD](https://simbad.u-strasbg.fr/simbad/sim-fbasic) since all of these objects will have reliable coordinates.
Using astroquery, we cross-match the SIMBAD coordinates with all of the objects in each catalog (2MASS, APOGEE-2 DR17, Gaia DR3, or PASTEL) searching within 20 arcseconds of the SIMBAD coordinates.
The closest object found to the SIMBAD coordinate of the object is saved, along with all of the catalog information for that object.

SIMBAD has a primary identifer for each object in its catalog that is associated with an object regardless of what name a user inputs to find that object.
In the second step, we search the catalog identifiers for each object found in step one using SIMBAD (via astroquery) and save them for later use.

In the final step, we compare the primary identifers found from step 2 to the primary SIMBAD identifiers already associated with each IGRINS observation.
If the primary identifers match, we have a successful cross-match and if the primary identifiers do not match the object is removed from the cross-match.
Some of the catalogs have valid object identifiers that are not yet searchable in SIMBAD, if this is the case, the object is flagged to warn a user to verify the information from the cross-match independently.
There is a flag value for each of the objects in RRISA XMatch for each of the catalogs; if the flag value is equal to 1, the catalog identifier for an object is not SIMBAD searchable.

Below is a figure showing a summary of some of the cross-match parameters from each of the catalogs in RRISA XMatch.

<center>
  <figure>
    <img src="/images/xmatch_stats.png" alt="Cross-match statistics for each catalog for 2MASS H/K magnitude, effective temperature, surface gravity, and metallicity." width = "600"/>
    <figcaption><i><u>Left:</u></i> a color-magnitude diagram using 2MASS H- and K-magnitudes for 4042 unique objects in the IGRINS cross-matched sample. Darker colors are low density regions of the diagram while light colors are high density. <i><u>Right:</u></i> three histograms for surface density, effective temperature, and metallicity (iron abundance) from top to bottom. Each histogram includes a distribution from Gaia DR3, APOGEE2 DR17, and PASTEL (from darkest to lightest color) with the amount of unique objects from each catalog labeled. These plots include both target objects and standard stars from the IGRINS cross-matched sample.</figcaption>
  </figure>
</center>

<h3>RRISA XMatch</h3>

Downloadable from [our GitHub](https://github.com/IGRINScontact/RRISA.git) as a .csv. Users can also view on through [Google Drive](https://docs.google.com/spreadsheets/d/1DrvtlcKKayyM6fWljNG90Mj2-EqkaX7ZzwwxuedVK5E/edit?usp=sharing) or [explore the RRISA_v3 folder on Box](https://utexas.box.com/s/l7i5dbtss084mhxywmc6r8pl39bs1yhw)!

For a more detailed description of the information included in RRISA XMatch, check out the RRISA XMatch folder on [our GitHub](https://github.com/IGRINScontact/RRISA/tree/main/RRISA_XMatch).
