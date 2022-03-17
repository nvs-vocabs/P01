This is a repository for sharing and managing issues related to the BODC P01 Parameter Usage Vocabulary (PUV).

Below is a short introduction to the BODC PUV and its semantic model, along with some guidelines for searching the P01 PUV, and information about how to contribute.

# The BODC Parameter Usage Vocabulary (PUV) and its semantic model

## What is it?

The BODC PUV is a **controlled vocabulary** for labelling scientific variables in databases and data files. It is a collection of unique and persistent identifiers attached to structurally logical labels and textual definitions.

It is a SKOS (Simple Knowledge Organisation System) controlled vocabulary. This means that its structure is compliant with SKOS, a W3C recommendation for the representation of knowledge in a format understandable to computers. Each entry in P01 is associated with a 8-byte parameter code, a preferred label, an alternative label, a definition field, and a status (accepted or deprecated). Each label is time-stamped with its creation date and its last modified date. All intermediate versions are saved and are accessible from the publicly available record. A term is never deleted but can be made obsolete by deprecation.

One important feature of the BODC PUV is that it is based on a **semantic model**. The semantic model allows us to create complex information-rich labels that are syntactically and semantically consistent. [This presentation](https://github.com/nvs-vocabs/P01/blob/master/The_BODC_P01_PUV_semantic_model_Aug2019.pdf) explains how the semantic model works.

## How can I access it?

The P01 PUV is a very large collection containing over 40,000 terms. It can be accessed via the NERC Vocabulary Server (NVS) [here](http://vocab.nerc.ac.uk/collection/P01) (this will take a few seconds to load) and it can be searched or browsed using the following tools

- [The BODC Vocabulary Search Interface](https://www.bodc.ac.uk/resources/vocabularies/vocabulary_search/P01/)

- [The SeaDataNet semantic component facet search](http://seadatanet.maris2.nl/bandit/browse_step.php)

- [The SeaDataNet parameter thesaurus](http://seadatanet.maris2.nl/v_bodc_vocab_v2/vocab_relations.asp?lib=P08)

Each P01 concept is mapped to the semantic elements used to construct the preferred label (see below) as well as a unit of measurement from the BODC's units of measurement vocabulary (P06), a broader discovery term from the SeaDataNet Parameter Discovery Vocabulary (P02) and, when applicable, concepts from other related semantic resources.

For users with knowledge of SPARQL, the P01 and its mappings can also be searched via the [NVS SPARQL endpoint](https://vocab.nerc.ac.uk/sparql/).

## How can I find P01 codes for my data?

Remember that a P01 label is always constructed from the following association of concepts:

|The property or attribute | 'of' | an object of interest | in relation to | an environmental matrix | 'by' | a method (optional)|
|--------------------------|------|-----------------------|----------------|-------------------------|------|--------------------|


All fields apart from 'of' and 'by' are populated from NVS controlled vocabularies (see [this diagram](https://github.com/nvs-vocabs/P01/blob/master/P01_wheel.pdf) for simple visualisation or download it to use as a tool for quick access to the semantic components of a P01 concept).

The "property" (or "attribute") must be associated with either an object of interest or a matrix or both.

The "object of interest" can be a chemical object, a biological object, a physical phenomenon, or a material object. 

When looking for codes the key questions are:

1. **What are the properties measured or observed**?
What kind of properties are they? Concentrations? Abundances? Temperature? Uptake rates? pH?

2. **What are the objects of interest**? 
Are they chemical substances? biological organisms? material objects? physical phenomena? none of these?

Note that if the property is the property of the environment under study (e.g. "pH of the water body" or "Temperature of the atmosphere") then the object of interest is the environmental matrix and the field "object of interest" can be ignored.

3. **What is the environmental matrix**?
- Do I need one? You will for most environmental measurements.
- Why? This is to remove any ambiguity about what the value reported relates to.
- Take for example "Concentration of cadmium" - This is an ambiguous label if used to define a variable because it does not say concentration of cadmium in what? In the sediment? a water body? the atmosphere? a biological organism? If the former was it in the liquid phase or attached to particles? If the latter was it in the whole organism or one of its organs? 
- If the measurement relates to a water body or the atmosphere one needs to ask: Was the sample filtered? If it were, then the filter type or filter size is an important information to be stored close to the measurement value. In the P01 semantic model this is captured as part of the matrix definition. 

For example, when a dissolved quantity is measured in a water body, we apply the following rules

- Use "water body [dissolved plus reactive particulate phase]" if the sample was not filtered

- Use "water body [dissolved plus reactive particulate <GF/F phase]" if the sample was filtered through GF/F filter

- Use "water body [dissolved plus reactive particulate <0.4/0.45um phase]" if the sample was filtered through a 0.4/0.45 um membrane

- Use "water body [dissolved plus reactive particulate <unknown phase]" if the sample was filtered but the filter type is unknown.


4. **Do I need to specify the method?**
- This can be important for some measurements or if one wants to distinguish between quantities measured using different methods

- The method is specified to avoid ambiguity and minimise the need to refer to free-text documentation

- It can help with automated data compilation and aggregation and decrease the risk of data being misinterpreted

Take for example, chlorophyll-a. The output from an in situ fluorometer is often labelled as "Concentration of chlorophyll-a". However the values cannot be guaranteed to be an accurate representation of the real amount of chlorophyll-a in a water body without access to textual information about the method and knowing whether the data have been validated against chlorophyll-a measured by filtration, extracted in a solvent and analysed using either HPLC, fluorometry or photometric methods. Most users would require that an automated search of chlorophyll-a data be able to distinguish between these different methods. The P01 semantic model is built so that this information can be captured in the parameter code.

### Examples
Some examples are being compiled and will be provided shortly

## How can I contribute?
- New P01 codes based on combinations of existing concepts can be submitted via the [BODC Vocabulary Builder](https://www.bodc.ac.uk/resources/vocabularies/vocabulary_builder/) following registration and login 

- New compound matrices and biological entities can also be submitted using the BODC Vocabulary Builder.

- Requests for new concepts that require community review should be submitted as issues in this repository (or emailed to vocab.services -at- bodc.ac.uk if you do not have access to github)

- Reporting errors or suggestions for improving content or mappings can also be submitted as issues in this repository or emailed to vocab.services -at- bodc.ac.uk. 

- New terms for the P01 semantic model component vocabularies (for example a new matrix or a new property) can be made here or under the relevant github repository (e.g. https://github.com/nvs-vocabs/S06/issues for a new property term). They can also be made via the BODC Vocabulary Builder as part of a new term request.

Notice 2018/03/19: The P01 vocabulary is currently undergoing remodelling of some of its semantic elements. The meaning of the concepts will never be changed however users may notice some changes to the structure or to the wording of the preferred label. Please report any issues of concern by opening an issue ticket in this repository or email vocab.services -at- bodc.ac.uk.

Quick links to the semantic model component repositories in github/nvs-vocabs:

Link type | Properties | Statistical terms | Chemical entities | Biological entities | Physical entities | Measurement-matrix relationships | Matrices | Sample preparation methods | Analytical methods | Data processing methods |
-------|-------|-------|-------|-------|-------|-------|------|-------|-------|-------|
GitHub repo | [S06](https://github.com/nvs-vocabs/S06/) | [S07](https://github.com/nvs-vocabs/S07/) | [S27](https://github.com/nvs-vocabs/S27/) | [S25](https://github.com/nvs-vocabs/S25/) |[S29](https://github.com/nvs-vocabs/S29/)|[S02](https://github.com/nvs-vocabs/S02/) | [S26](https://github.com/nvs-vocabs/S26/) | [S03](https://github.com/nvs-vocabs/S23/)| [S04](https://github.com/nvs-vocabs/S04/)|[S05](https://github.com/nvs-vocabs/S05/)
NVS SKOS collection | [S06](https://vocab.nerc.ac.uk/collection/S06/) | [S07](https://vocab.nerc.ac.uk/collection/S07/) | [S27](https://vocab.nerc.ac.uk/collection/S27/) | [S25](https://vocab.nerc.ac.uk/collection/S25/) |[S29](https://vocab.nerc.ac.uk/collection/S29/)|[S02](https://vocab.nerc.ac.uk/collection/S02/) | [S26](https://vocab.nerc.ac.uk/collection/S26/) | [S03](https://vocab.nerc.ac.uk/collection/S23/)| [S04](https://vocab.nerc.ac.uk/collection/S04/)|[S05](https://vocab.nerc.ac.uk/collection/S05/)
NVS search UI | [S06](https://www.bodc.ac.uk/resources/vocabularies/vocabulary_search/S06/) | [S07](https://www.bodc.ac.uk/resources/vocabularies/vocabulary_search/S07/) | [S27](https://www.bodc.ac.uk/resources/vocabularies/vocabulary_search/S27/) | [S25](https://www.bodc.ac.uk/resources/vocabularies/vocabulary_search/S25/) |[S29](https://www.bodc.ac.uk/resources/vocabularies/vocabulary_search/S29/)|[S02](https://www.bodc.ac.uk/resources/vocabularies/vocabulary_search/S02/) | [S26](https://www.bodc.ac.uk/resources/vocabularies/vocabulary_search/S26/) | [S03](https://www.bodc.ac.uk/resources/vocabularies/vocabulary_search/S23/)| [S04](https://www.bodc.ac.uk/resources/vocabularies/vocabulary_search/S04/)|[S05](https://www.bodc.ac.uk/resources/vocabularies/vocabulary_search/S05/)
