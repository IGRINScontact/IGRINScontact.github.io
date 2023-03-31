---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: page
title: The XMatch
permalink: /RRISA_xmatch/
---

<h1>Reduced & Crossmatched</h1>
For objects in the IGRINS sample that are searchable via SIMBAD, we can crossmatch with other catalogs to provide additional information.
In the beta version of RRISA we support crossmatching with [2MASS](https://ui.adsabs.harvard.edu/abs/2003yCat.2246....0C/abstract), [APOGEE](https://ui.adsabs.harvard.edu/abs/2020AJ....160..120J/abstract), [Gaia EDR3](https://ui.adsabs.harvard.edu/abs/2020yCat.1350....0G/abstract), [Gaia DR2](https://ui.adsabs.harvard.edu/abs/2018A%26A...616A...1G/abstract), and [PASTEL](https://ui.adsabs.harvard.edu/abs/2016A%26A...591A.118S/abstract).
For a more detailed description of the XMatch RRISA header, check out the readme.md in the RRISA_XMatch folder on [our GitHub](https://github.com/IGRINScontact/RRISA.git).


<h3>Object Matching</h3>
The crossmatching for RRISA errs on the side of caution in an effort to reduce misidentification of objects.
Crossmatching is possible through [xMatch Queries](https://astroquery.readthedocs.io/en/latest/xmatch/xmatch.html) via [astroquery](https://astroquery.readthedocs.io/en/latest/index.html) and is undertaken through the following:
- Using xMatch Queries to find objects in the corresponding catalog within 1 arcsec of the object's SIMBAD coordinates
- With the identifiers returned from the above step, query SIMBAD
- Compare the names of the objects from the two queries and remove catalog results for objects without matching names.

The flag column for each catalog will either have a value of NaN or 1.
A flag of 1 means that the identifier returned from the xMatch Query is not SIMBAD searchable.
In this case the objects could match, but we suggest that the user manually check to confirm.

<h3><b>New in RRISA v1: Rtell Data Products & File Format</b></h3>
See the RRISA Reduced website tab for more information about the new rtell data products!

<h3>RRISA XMatch</h3>

Downloadable from [our GitHub](https://github.com/IGRINScontact/RRISA.git) as a .csv or .xlsx. Users can also view on through [Google Drive](https://docs.google.com/spreadsheets/d/1EOHGfJ5Huic9o9eKsXrEgZnt7W0QX9xbKj3oDGxQ9kA/edit?usp=sharing) or [explore the RRISA_v1 folder on Box](https://utexas.box.com/s/w3i7rya83lmgkiqkg79w85b7wrra90m5)!

For a more detailed description of the XMatch RRISA header, check out the readme.md in the RRISA XMatch folder on [our GitHub](https://github.com/IGRINScontact/RRISA.git).
