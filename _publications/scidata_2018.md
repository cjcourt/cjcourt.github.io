---
title: "Auto-generated Materials Database of Curie and Néel Temperatures via Semi-supervised Relationship Extraction"
collection: publications
permalink: /publication/scidata_2018
excerpt: 'Large auto-generated databases of magnetic materials properties have the potential for great utility in materials science research. This article presents an auto-generated database of 39,822 records containing chemical compounds and their associated Curie and Néel magnetic phase transition temperatures. The database was produced using natural language processing and semi-supervised quaternary relationship extraction, applied to a corpus of 68,078 chemistry and physics articles. Evaluation of the database shows an estimated overall precision of 73%. Therein, records processed with the text-mining toolkit, ChemDataExtractor, were assisted by a modified Snowball algorithm, whose original binary relationship extraction capabilities were extended to quaternary relationship extraction. Consequently, its machine learning component can now train with ≤ 500 seeds, rather than the 4,000 originally used. Data processed with the modified Snowball algorithm affords 82% precision. Database records are available in MongoDB, CSV and JSON formats which can easily be read using Python, R, Java and MatLab. This makes the database easy to query for tackling big-data materials science initiatives and provides a basis for magnetic materials discovery.'
date: 2018-06-19
venue: 'Nature Scientific Data'
paperurl: 'https://www.nature.com/articles/sdata2018111'
citation: 'Court C.J & Cole J.M "Auto-generated Materials Database of Curie and Néel Temperatures via Semi-supervised Relationship Extraction" <i>Scientific Data</i>. 5, 180111 (2018)'
---
# Description
This work develops a probabilistic approach to quaternary chemical relationship extraction from scientific text. Largely based on extensions to the Snowball Algorithm.

The tool was used to create a vast database of magnetic phase transition temperatures - the first auto-generated database of its kind. 

The resulting database was later used by others to discover novel magnetocaloric effects in $HoB_2$. You can read that work <a href="https://www.nature.com/articles/s41427-020-0214-y">here</a>
