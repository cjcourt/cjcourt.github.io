---
title: "The ChemDataExtractor Toolkit"
excerpt: "A chemistry aware toolkit for extraction of chemical relationships from scientific documents<br/><br/><img src='/images/cde_logo.svg'>"
collection: projects
---
# Overview
The ChemDataExtractor toolkit (CDE) is a complete natural language processing pipeline, designed to automatically extract chemical properties from scientific documents (journal articles, patents etc.). This allows the user to analyse thousands of documents and create large databases of material properties. These data can then be used to for data-driven materials discovery. Cool right?

I have worked on CDE for the past 4 years as part of my MPhil and PhD, developing the toolkit for use on magnetic materials.

# Related Work
The original toolkit was developed by [Matt Swain](https://github.com/mcs07) in the [Cambridge Molecular Engineering group](https://mole.phy.cam.ac.uk). The original publication is [here](https://pubs.acs.org/doi/full/10.1021/acs.jcim.6b00207) and the corresponding web interface is [here](http://chemdataextractor.org).

A number of papers have since been published demonstrating and extending the capabilities of CDE:

[A database of battery materials auto-generated using ChemDataExtractor]()

[ChemSchematicResolver: A Toolkit to Decode 2D Chemical Diagrams with Labels and R-Groups into Annotated Chemical Named Entities]()

[Magnetic and superconducting phase diagrams and transition temperatures predicted using text mining and machine learning]()

[Comparative dataset of experimental and computational attributes of UV/vis absorption spectra]()

[ImageDataExtractor: A Tool to extract and quantify data from microscopy images]()

[Dye‐Sensitized Solar Cells: Design‐to‐Device Approach Affords Panchromatic Co‐Sensitized Solar Cells]()

[Auto-generated materials database of Curie and Néel temperatures via semi-supervised relationship extraction]()


In summary, the toolkit is very general, and can therefore be applied in any domain.

# How it works

This figure gives an overview of the CDE pipeline.

![CDE_overview](/images/system_overview.png)

The <i>Document Processors</i> break down the input documents into their constituent elements (text, tables, figures etc), and these are passed through separate relationship extraction pipelines for identifying chemical relationships.

The <i>Interdependency Resolver </i> links the relationships together to resolve dependencies across different document elements. E.g. linking chemical labels to the correct chemical formula.

The result is a set of mutually consistent chemical records that can be placed into a database.

This is probably best explained through an example.

## An Example - Extracting Melting Points

Let's say we have the following (contrived) example document*:

> <b><center> On the Melting Point of Water </center></b>
<b>Abstract</b>
In this work we analyse the melting point of water. Specifically, the temperature at which solid water (also known as ice), undergoes a transition to liquid form.<br>
<b>Results</b>
This section describes the results of our experiments on Sample 1 ($H_2O$). It was found that Sample 1 underwent the solid-liquid phase transition under heating at 273.15 K.

<i><small>* Note that this above work is highly propietary research and should not be stolen under any circumstances...</small></i>

Firstly, CDE breaks this document down into sections:
1. Title
2. Heading
3. Paragraph
4. Heading
5. Paragraph

The sentences are further tokenized down to word tokens.

The key information is contained in a few sentences:

> "This sections describes the results o our experiments on Sample 1 ($H_2O$)"

This identifies two entities, a chemical formula and a corresponding label. This effectively creates the link that Sample 1 == $H_2O$.

> "...Sample 1 underwent the solid-liquid phase transition ... 273.15 K"

This finds a melting point relationship of (melting point, 273.15, Kelvin, Sample 1)

Finally the interdependency resolvers link the two records to give a final record:

Melting Point
    * Compound: $H_2O$
    * labels: Sample 1
    * Value: 273.15
    * Unit: Kelvin

Voila!

# Further Reading
I have written some blog posts on how to use CDE in more detail. You can also clone the [repository](https://github.com/CambridgeMolecularEngineering/chemdataextractor) and have a play with it yourself!

Happy extracting.