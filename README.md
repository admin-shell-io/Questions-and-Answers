<!-- last id: 46 -->
# Asset Administration Shell Frequently Asked Questions List 
## Disclaimer

This Q&A has been initially created by a Task Force of "ZVEI SG Modelle und Standards". It now is maintained by the IDTA Workstream "Best Modeling Practice".

Primary URI for end-user usage and references is: [https://admin-shell-io.github.io/questions-and-answers/](https://admin-shell-io.github.io/questions-and-answers/), cross-link single questions as follows [https://admin-shell-io.github.io/questions-and-answers/#id18](https://admin-shell-io.github.io/questions-and-answers/#id18)

Please address discussions and proposals via issues and pull requests in the github repository: [https://github.com/admin-shell-io/questions-and-answers/](https://github.com/admin-shell-io/questions-and-answers/)

## FAQ

### Assets and Asset Types
- [How to define the relationship between asset instance and asset type wrt. corresponding submodels?](#idgh13)

### Asset Administration Shell
- [What are best practices for creating a system of Asset Administration Shells?](#id42)
- [Where are examples of AAS available?](#id16)
- [Can RDF be used as an interchange format?](#idgh59)
- [Values for externalSubjectId within SpecificAssetId?](#idgh78)

### Submodels and Submodel Templates
- [How to define optional and mandatory elements for a submodel of kind=Template?](#id43)
- [How should submodel templates (kind=Template) and submodel instances (kind=Instance) be linked together?](#idgh37)
- [Which names are already defined for important submodels?](#id12)
- [Which submodel shall contain the serial number of a device?](#id23)
- [Is it allowed to have both, Submodel Templates and Submodel Instances, in the same AAS?](#id42)
- [Is there a comprehensive list of submodel templates available?](#idgh66)
- [Is there a submodel for modeling of kinematics?](#idgh73)
- [Is there an example using a Bill of Material (BOM) submodel to create an AAS for a product/machine which comprises several other assets?](#idgh64)
- [How to use different versions of the same submodel (e.g. different versions of the "digital nameplate") which share same IdShort?](#idgh72)

### SubmodelElements
- [How shall a link to a website be entered in an AAS, as File or as ReferenceElement object?](#id2)
- [If the same properties are used in several submodels, shall they also be entered several times or shall they be referenced?](#id5)
- [How to use physical units for quantifiable properties?](#id7)
- [How to treat values of Properties with values in multiple languages?](#id9)
- [How shall a document be handled which includes different content according to VDI 2770 and the related DocumentClassIDs?](#id10)
- [How to store certificates and conformance declarations within AAS/Submodels?](#id13)
- [Which mechanisms can be used to structure complex data?](#id15)
- [Are there any best practices how to choose the idShort of an element?](#id30a)
- [I need a speaking name on my dashboard - which attribute value shall I use?](#id30b)
- [Where shall images (products or icons) of an asset be stored, e.g., for the use in dashboards?](#id31)
- [How should I name a submodel element if there are more than one with the same semanticId?](#id43)
- [How should array data values within the AAS be represented if array elements have the same semantic ID?](#id45)
- [How to use qualifiers?](#id46)
- [How to use ValueIDs?](#idgh77)
- [How to deal with property values including multiple values?](#ghid36)

### Identification
- [What are best practices for creating custom IRI identifiers for generic concepts?](#id18)
- [Is the following IRI-based ID with a query parameter valid “http://vendor.com/suffx?a=abc&b=xyz”?](#id38)

### Infrastructure and Versioning
- [How does the version of a submodel impact referencing of a submodel?](#idgh14)
- [Is it possible to determine submodel kind (i.e., Template or Instance) from a Registry without loading the actual submodel from via AAS-repository API?](#idgh62)

### Semantics / ECLASS
- [How shall the ECLASS group “Zusatzdokumentation (e.g. IRDI 0173-1#02-ADN464#..)” be used for documentation?](#id8)
- [How to refer to semantic concepts of existing standards like VDI 2770 properties or OPC UA companion specifications (e.g. “Serial number” property from OPC UA DI companion spec)?](#id27)
- [How to use isCaseOf to indicate 'alternative' semanticIDs of AAS elements?](#id46)
- [What shall be entered for the semanticId attribute if a related concept description does not exist in ECLASS or IEC CDD?](#id3)
- [How shall properties be entered which are defined both in ECLASS and in CDD?](#id34)
- [Are semanticId(s) optional or mandatory?](#id40)
- [Can semantic ID(s) be used without defining a concept description within the AAS package?](#id41)
- [How to treat ECLASS Quantity Concept in AAS?](#id44)
- [Should one use ECLASS application classes in define semantics of a submodel?](#idgh33)
- [What are strategies to match semantic IDs?](#idgh54)

### Code Generation
- [Which code generators work for which programming language?](#id55)
- [Which code generators have known issues with the AAS?](#id56)

## Answers

**[How to define optional and mandatory elements for a submodel of kind=Template?](#id43)** <a id="id43"></a><!-- ID: 43 -->

Currently (September 2021) there is no clean solution for that. Plattform Industrie 4.0 is evaluating different modeling options.

As a *temporary workaround* we propose to use the qualifier name is "Multiplier" with values "One", "ZeroToOne", "ZeroToMany", "OneToMany" as done by many practitioners defining submodel templates.

**[How should submodel templates (kind=Template) and submodel instances (kind=Instance) be linked together?](#idgh37)** <a id="idgh37"></a><!-- ID: gh37 -->

The submodel template with kind=Template and the submodel instance with kind=Instance should have the same semanticID to indicate the applicability of the template on the instance. 

**[How does the version of a submodel impact referencing of a submodel?](#idgh14)** <a id="idgh14"></a><!-- ID: gh14 -->

AAS provides two approaches for versioning:

1) Versioning within semantic ID, e.g., for URIs "0173-xxx-zzz-zzz#version" or "https://admin-shell.io/sandbox/zvei/nameplate/0/1/Nameplate":
* Possibly, breaking semantic changes, i.e., other meaning
* Possibly, reverse-compatibility, e.g., extension
* Not clarified yet which meaning "major" and "minor" parts within the semantic ID are having. Currently they correspond to the version of the submodel spec, e.g., 2.0 or 2.1.

2) Changes within "administrative information" within AAS:
* Related to content within AAS, not to its "external-interface", therefore not necessary to standardize meanings of Major/Minor now.

As of now, references ignore versioning information. In case versioning is essential, the versioning information must be part of the element's ID.

**[How to use isCaseOf to indicate 'alternative' semanticIDs of AAS elements?](#id46)** <a id="id46"></a><!-- ID: 46 -->

[This AAS example](https://admin-shell-io.github.io/questions-and-answers/Examples/isCaseOf_Examples.aasx) contains a template of "Technical Data" submodel with two properties indicating how alterantive semantic IDs can be used in AAS modeling. For example, the "ManufacturerName" property, has a semantic ID "https://admin-shell.io/sandbox/SG2/TechnicalData/ManufacturerName/1/1" and two isCaseOf references to a ECLASS and a CDD IRDIs (the references are within the ConceptDescription).

**[What are best practices for creating a system of Asset Administration Shells?](#id42)** <a id="id42"></a><!-- ID: 42 -->

There are currently two ways to create/reference further AAS:
1) Using a BOM (Bill of Material) submodel, a dedicated submodel with self- or co-managed assets

  > Note: Scope of the BOM submodel are relations between *assets* and not *AASs*. BOM submodel defined “isPartOf” and “isIdentical” relation types between assets.

   *  Self-managed assets have own asset ID which can be used in AAS infrastructure (e.g., a registry) to query available AAS.
   *  Co-managed assets have no asset ID and own AAS.
 
&nbsp;&nbsp;&nbsp;&nbsp;*Advantages*: BOM-AAS is self-contained and has no “external” dependencies such as references to AAS, probably will be used as blueprint for further submodels.

&nbsp;&nbsp;&nbsp;&nbsp;*Disadvantages*: AAS infrastructure for resolution of asset ID to AAS is needed.

2)  Direct references to external AAS or Submodels using ReferenceElements or RelationshipElements. We currently do not recommend this method in case of lacking generalizability and creation of tight couplings between AAS (by taking over the “resolution” part).

(Answered: 2021-06-28)

**[How shall a link to a website be entered in an AAS, as File or as ReferenceElement object?](#id2)** <a id="id2"></a><!-- ID: 2 -->

Links to websites shall be entered as File object (physical reference). ReferenceElement  objects represent logical references.
A typical usage for logical references is in the description of a topology of the asset or „consist of” hierarchies.

(Answered: 2020-08-13)

**[If the same properties are used in several submodels, shall they also be entered several times or shall they be referenced?](#id5)** <a id="id5"></a><a id="id23"></a><!-- ID: 5, 23 -->

Submodels shall be as independent as possible so that they can be changed and developed separately.
Consequently, the same properties shall be copied to another submodel and references shall not be used in such case. 
The concept description referenced in semanticId, however, should be the same.

(Answered: 2020-08-13)

**[How to use physical units for quantifiable properties?](#id7)** <a id="id7"></a><a id="id20"></a><!-- ID: 7, 20 -->

AAS defines specific constructs of unit and unitID for concept descriptions (template DataSpecificationIEC61360).
We advise you to use unitIDs  that refer to pre-defined ECLASS IRDIs, e.g., 0173-1#05-AAA480#002  for millimeters. 
In a non-likely case of non-existent global IRDI for a unit, please [follow the general guidance for custom semantic IDs
to create a custom unitID](https://github.com/admin-shell-io/questions-and-answers/blob/master/README.md#id3).

(Answered: 2020-08-13)

**[What shall be entered for the semanticId attribute if a related concept description does not exist in ECLASS or IEC CDD?](#id3)** <a id="id3"></a><!-- ID: 3 -->

Besides ECLASS and IEC CCD also other domain specific dictionaries may be used. The only prerequisite is that the id can be uniquely resolved.

This also holds true for proprietary dictionaries. For example, the id of a proprietary concept description defined by your own company could be <CompanyName>/<FurtherHierarchicalName>/<PropertyName>”. This id is also used as semanticId of the property then.

Alternatively, an agile flexible approach using GITHUB has been defined. You may store your CDs there which are defined as “http://admin-shell.io/<sub-namespace>[/<version>[/<revision>]]/<ShortId>”. The working draft repository is placed at https://github.com/admin-shell-io/id.

(Answered: 2020-08-13)

**[How shall the ECLASS group “Zusatzdokumentation (e.g. IRDI 0173-1#02-ADN464#..)” be used for documentation?](#id8)** <a id="id8"></a><!-- ID: 8 -->

Please use the submodel template based on VDI 2770 for documentation instead. It will be released soon.

(Updated: 2020-08-14)

**[How to treat values of Properties with values in multiple languages?](#id9)** <a id="id9"></a><!-- ID: 9 -->

Details of the Asset Administration Shell Part 1 provides the **MultiLanguageProperty** entity for this case since version 2.0.

(Answered: 2020-08-13)

**[How shall a document be handled which includes different content according to VDI 2770 and the related DocumentClassIDs?](#id10)** <a id="id10"></a><!-- ID: 10 -->

Currently, VDI 2770 only allows exactly one DocumentClassID per document. A proposal has been already made to the VDI 2770 workgroup to extend this. In AAS it is suggested to list several properties with different DocumentClassIDs for such a multipurpose document.

(Answered: 2020-08-13)

**[Which names are already defined for important submodels?](#id12)** <a id="id12"></a><a id="id21"></a><a id="id24"></a><!-- ID: 12, 21, 24 -->

The following names shall be used for submodels:

- [**Nameplate**](https://www.plattform-i40.de/PI40/Redaktion/EN/Downloads/Publikation/Submodel_templates-Asset_Administration_Shell-digital_nameplate.html) defines digital nameplate
- **Identification** defines supplier and product, 
- [**TechnicalData**](https://www.plattform-i40.de/PI40/Redaktion/EN/Downloads/Publikation/Submodel_templates-Asset_Administration_Shell-Technical_Data.html) for technical data of a product,
- **ConfigurationData** for setpoints of a production process,
- **OperationalData** for actual values of a production process,
- **Documentation** to store documents for a product and to classify the documentation according to VDI 2770,
- **CertificatesAndDeclaration** for storing certificates and conformance classes.

(Answered: 2020-08-13)

**[How to store certificates and conformance declarations within AAS/Submodels?](#id13)** <a id="id13"></a><!-- ID: 13 -->

A dedicated submodel with IdShort “CertificatesAndDeclarations” with ID https://admin-shell.io/submodels/CertificatesAndDeclarations is proposed. This model shall contain boolean properties or text-properties indicating conformance to certificates. Actual certificate documents, e.g., scanned TÜV reports, shall be contained in the “Documentation” submodel and referenced from “CertificatesAndDeclarations” elements.

Examples are the boolean property **0173-1#02-BAF053#008** set to true if a CE qualification is present, or the text-property **0173-1#02-AAE327#001** for a textual name of the fulfilled conformance.

(Answered: 2020-08-13)

**[Which mechanisms can be used to structure complex data?](#id15)** <a id="id15"></a><!-- ID: 15 -->

Collections can be used to “physically” separate and structure submodel elements into different topics.

Qualifiers can be used to add additional meta-information to AAS elements that is not included in the model of AAS. 
Currently (Details of AAS Part 1 Version 2), concrete qualifiers are not specified, however the document provides some non-normative examples for qualifiers:
e.g. the indication of a lifecycle state of a value by “as-specified” or “as-measured”, or
e.g. the indication of multiplicity of allowed components for modelling by “greater than 0” and others.

(Answered: 2020-08-13)

**[Where are examples of AAS available?](#id16)** <a id="id16"></a><!-- ID: 16 -->

Examples of several suppliers are found at: http://admin-shell-io.com/samples/ 

(Answered: 2020-08-13)

**[What are best practices for creating custom IRI identifiers for generic concepts?](#id18)** <a id="id18"></a><!-- ID: 18 -->

What are best practices for creating custom IRI identifiers for generic concepts.
We advise using “https://admin-shell.io/” prefix for those identifiers (see guides via https://github.com/admin-shell-io/id/) for generic concepts. Note that we advise to use “https:” protocol and avoid adding “www.” subdomain into admin-shell.io naming scheme.
Furthermore, in practical implementations we advise to “filter” out protocol and schema for comparing IRI identifiers. For example, following IDs should be considered equal:
- https://admin-shell.io/some_id_example
- http://admin-shell.io/some_id_example
- ftp://admin-shell.io/some_id_example
- https://www.admin-shell.io/some_id_example
- http://www.admin-shell.io/some_id_example

(Answered: 2020-08-19)

**[Which submodel shall contain the serial number of a device?](#id23)** <a id="id23"></a><!-- ID: 23 -->

Serial number is a submodel element of “Identification” submodel referenced in AAS for an asset with assetKind=Instance, i.e. instance’s AAS. 

(Answered: 2020-08-19)

**[How to refer to semantic concepts of existing standards like VDI 2770 properties or OPC UA companion specifications (e.g. “Serial number” property from OPC UA DI companion spec)?](#id27)** <a id="id27"></a><a id="id28"></a><!-- ID: 27, 28 -->

Map concepts to “admin-shell.io” namespace (see [custom identifier best practices](#id18)). Within the concept description itself use “sourceOfDefinition” or “isCaseOf” to link to “original” concept. 

(Answered: 2020-08-24)

**[Are there any best practices how to choose the idShort of an element?](#id30a)** <a id="id30a"></a><!-- ID: 30a -->

For choosing an idShort value there are the following recommendations (rules and order can be used for automatically creation of an idShort):

- If an English shortname is available in the related concept description, the English shortName can be used as idShort. 
- If there is an English preferredName available in the related concept description, this name can be converted to idShort, e.g. the preferredName “Maximum rotation speed” can be converted to “maximumRotationSpeed”.

In case a submodel template specification is used as a base, the idShort defined in this submodel template shall be used.

Note: the isShort does not carry any semantic meaning. For speaking names the display name shall be used.

(Updated: 2021-05-17)


**[I need a speaking name on my dashboard - which attribute value shall I use?](#id30b)** <a id="id30b"></a><!-- ID: 30b -->

For speaking names (in different languages) the display name (Referable/displayName) shall be used.

If no display name is defined in the language requested by the application, then the display name is selected in the following order if available:
- the preferred name in the requested language of the concept description defining the semantics of the element
- If there is a default language list defined in the application, then the corresponding preferred name in the language is chosen according to this order.
- the English preferred name of the concept description defining the semantics of the element
- the short name of the concept description
- the idShort of the element

Note: DisplayName was introduced with Part 1, V3.0RC01. Display name is optional. 

(Updated: 2021-05-17)


**[Where shall images (products or icons) of an asset be stored, e.g., for the use in dashboards?](#id31)** <a id="id31"></a><!-- ID: 31 -->

With V3.0RC01 of Part 1 an optional attribute "assetInformation/defaultThumbnail" was introduced. The type of this attribute is "File".

The standardized [submodel template "Generic Frame for Technical Data for Industrial Equipment in Manufacturing" (Version 1.1)](https://www.plattform-i40.de/PI40/Redaktion/DE/Downloads/Publikation/Submodel_Templates-Asset_Administration_Shell-Technical_Data.html) allows to add as many product images as needed (https://admin-shell.io/ZVEI/TechnicalData/Productimage/1/1). Again, the type of these images is "File".

(Updated: 2021-02-08)

**[How shall properties be entered which are defined both in ECLASS and in CDD?](#id34)** <a id="id34"></a><!-- ID: 34 -->

If definitions for several product application areas are needed (e.g. ECLASS for factory automation and CDD for process automation), the related properties (e.g. ManufacturerName) shall be entered twice. At each of the properties one of the concept descriptions (ECLASS or CDD) is entered. The name of a property shall be either counted up (e.g. ManufactureName1) or extended by a suffix (e.g. ManufacturerNameCDD).

Alternatively an own concept description may be defined and "isCaseOf" may be used, so that both IRDIs can be entered in the concept description.

(Answered: 2020-09-21)

**[Is the following IRI-based ID with a query parameter valid “http://vendor.com/suffx?a=abc&b=xyz”?](#id38)** <a id="id38"></a><!-- ID: 38 -->

Yes, this is a valid ID.

(Answered: 2020-09-21)


**[Are semanticId(s) optional or mandatory?](#id40)** <a id="id40"></a><!-- ID: 40 -->

Although semanticIds are optional it is recommended to add a semantic reference (semanticId) whenever possible: without semanticId there is no semantic interoperability. IdShort of elements can be standardized as is done for some elements in submodel templates. However, this is not sufficient. Additionally, a semanticId is needed, for example to include version information or information about variants about the same element.

Sometimes there is no standardized concept description available in ECLASS or IEC CDD. See the [answer to this question](https://github.com/admin-shell-io/questions-and-answers#id3) for how to deal with this case. 

In AAS Part 1 V3.0RC01 semanticId(s) are not mandatory for submodels or submodel elements. SemanticId(s) are recommended to be added for submodel instances and submodel elements.

Up to AAS Part 1 V2.0 semanticId(s) were mandatory for submodel elements and were recommended for submodels with kind=Instance. For submodels with kind=Template the semanticId was optional.

(Updated: 2021-02-08)


**[Can semantic ID(s) be used without defining a concept description within the AAS package?](#id41)** <a id="id41"></a><!-- ID: 41 -->

 [update: In V3.0RC01 of part 1 of AAS in Detail the attribue "local" in References was removed]
  
Yes. Please use the following alternatives:
- Semantic ID reference type=ConceptDescription: the concept description is within the package or deployed on the same server like the element referring to it
- Semantic ID reference type=GlobalReference: a concept description object is not defined, just a reference to an external source is made

 Note: AASX Package Explorer will be updated to V3.0RC01 in the first half of 2022.
 
(Answered: 2021-12-13)

**[Is it allowed to have both, Submodel Templates and Submodel Instances, in the same AAS?](#id42)** <a name="id42"></a> 

Submodel Templates guide the creation of Submodel Instances. Although the specification does not restrict an Asset Administration Shell to contain both, Submodels with kind=Template and Submodels with kind=Instance, it is good practice to separate Submodel Templates from Submodel Instances. Typically, the owners of and the life cycle for creating and maintaining Submodel Templates are different from the owners of and from creating and operating Submodel Instances. 

(Answered: 2021-01-08)

**[How should I name a submodel element if there are more than one with the same semanticId?](#id43)** <a id="id43"></a>

There are several ways to deal with the topic of naming in the case that there is a set of elements (Referable/idShort), each with the same semanticId (for example in a SubmodelElementCollection with allowDuplicated=True):
* just number the elements (Example: Document01, Document02, Document{nn})
* assign a speaking name to each (Example: WheelFrontLeft, WheelFrontRight, WheelRearLeft, WheelRearRight)
Via display names (introduced in V3.0RC01 Referable/displayName, it is also possible to assign more speaking names in a later stage if needed)

Note: It is requested that the idShort of a non-identifiable is unique in its name space (for example in a Submodel or in a SubmodelElementCollection). This is not requested for the display names!

(Answered: 2021-01-11)

**[How to treat ECLASS Quantity Concept in AAS?](#id44)** <a id="id44"></a>

Example why quantities are needed additionally to units to automatically check compatibility of two properties: The unit "Newtonmeter" can be linked to the quantity "torque" but also to the quantity "energy". Only if the quantity is the same a conversion of the property value is possible.

The metamodel of the AAS (status: V3.0RC01) does not explicitly support the concept of quantities. This means, in case properties are not defined in ECLASS or in any other standardized dictionary it is not possible to specify the quantity of this proprietary property. In case the property is defined in ECLASS then the quantity is defined implicitly, because it is defined in ECLASS itself.

Future versions of the AAS might support quantities:

* by IRDI reference only in the concept description of a property (i.e. extending data specification DataSpecificationIEC61360)
* by additinally providing a corresponding data specification template for quantities conformant to IEC61360

Please be aware: the AAS does not support the concept of alternative units (as does IEC 61360 or ECLASS): it is assumed that the unit specified is also the unit that is used.

In general: The aim of the basic AAS concept is not about defining semantics, it is about referencing concept descriptions. Support of corresponding data specifciations is optional anyway.

(Answered 2021-01-11)
 
 **[How should array data values within the AAS be represented if array elements have the same semantic ID?](#id45)** <a id="id45"></a>

Pre 3.0 version of the metamodel:
Use "Blob"-element, e.g., "[1,2,3,4,5]" having a "serialized" JSON-value format (see upcoming time series submodel template). The data types of array's content, e.g. string, float or integer, can be defined using custom semantic ID of the submodel element.
(Design decision: take "Blob" instead of String in order not to overload generic UIs with representation of possibly long arrays.)

Since 3.0 verison of the meamodel:
Submodel Element List element should be used, cf. "5.3.7.17 Submodel Element List Attributes" of [AASiD Part 1 3.0](https://industrialdigitaltwin.org/wp-content/uploads/2023/04/IDTA-01001-3-0_SpecificationAssetAdministrationShell_Part1_Metamodel.pdf)
  
(Answered 2021-05-31, updated 2023-06-19)

 **[How to use qualifiers?](#id46)** <a id="id46"></a>

In this Repository, you can find a qualifier example in the folder "Examples". It contains an AAS (Qualifier_Examples.aasx) with a Submodel called "QualifierExampleSubmodel". 
1. In this Submodel the property "MaxRotationSpeed" has two example qualifiers (ExpressionSemantic=ASSURANCE_1 and PredicateRelation=GREATER_THAN_0). They are extracted from [DIN SPEC 92000](https://www.beuth.de/en/technical-rule/din-spec-92000/320981982) and state that the Submodel assures, that the asset's MaxRotationSpeed is greater than 30 1/min.
2. Besides that, the Submodel contains the Submodelelementcollection "Width_LifeCycle", which contains the Property width three times. Based on IEC 62569-1:2017, the property "width" might need different values during the assets life cycle. In the example, there are three slightly different values for "As Specified", "As Built" and "As Decomissioned" (life cycle qual=SPEC, life cycle qual=BUILT, life cycle qual=DECOM). You may find further information about this concept in the [IEC Common Data Dictionary](https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/e0e56d2682a34311c12575560058dc1c/20bf16149b5986a8c12586470047d709)

Further information on qualifiers and the usage in the AASx Package Explorer can be found in the specific [screencast on qualifiers](https://admin-shell-io.com/screencasts/aasx-package-explorer/en/Aasx_PackEx_Tutorial_-_EN_-_16_Working_with_qualifiers.mp4)

(Answered 2021-05-31)
  
 **[Is there a comprehensive list of submodel templates available?](#idgh66)** <a id="idgh66"></a>
  
 There is a list of submodels coming from IDTA (both finalized and under development) available here: https://industrialdigitaltwin.org/en/content-hub/submodels.
 
  (Answered 2022-03-21)
  
  **[Is it possible to determine submodel kind (i.e., Template or Instance) from a Registry without loading the actual submodel from via AAS-repository API?](#idgh62)** <a id="idgh62"></a>
  
  Currently submodel kind can not be retrieved using Registry-API. This issue will be addressed by standardization working groups. In the meantime, we propose to maintain a dedicated registry for submodel templates within the AAS-infrastructure. Submodel templates can be part of a "singleton-AAS" with a dedicated asset ID used to collect those.
  
  (Answered 2022-03-21)
  
 **[Is there a submodel for modeling of kinematics?](#idgh73)** <a id="idgh73"></a>
  
Q: Common file formats for this information already exist (e.g. URDF files) - so perhaps the intention is for this information to simply be referenced or added as supplementary files in the AAS? In any case, some guidance on the best practice would be useful.
  
A: We are not aware of any dedicated kinematic models within AAS.
Embedding files within submodels is always possible using "File" submodel elements with dedicated semantic IDs, as it is, for example, done within the MTP submodel proposal.
  
 Furthermore, kinimatics can be included as part of the "simulation handover" submodel, see [current state of the submodel definition](https://github.com/admin-shell-io/submodel-templates/tree/main/development/Simulation/).
 
  (Answered 2022-06-13)

 **[Is there an example using a Bill of Material (BOM) submodel to create an AAS for a product/machine which comprises several other assets?](#idgh64)** <a id="idgh64"></a>

An example of modeling is provided in the following [publication](https://www.plattform-i40.de/IP/Redaktion/EN/Downloads/Publikation/AAS_Reference_Modelling.pdf?__blob=publicationFile&v=5). Example submodels are available [here](http://liabroker.ddns.net:51001/). Note: currently the specification of BOM submodel is ongoing within IDTA's "Bill of Material" working group (reference available [here](https://industrialdigitaltwin.org/en/content-hub/submodels)). For additional information see also [another question](#id42).
  
  (Answered 2022-06-13)

**[How to deal with property values including multiple values?](#ghid36)**  <a id="ghid36"></a>
 
Q: How to deal with "property values" that include a set of values, e.g. seperated by comma? Examples are colors in RGB, coordinates, etc. Is there a specific format for these property elements? How can one transport that a specific format is required?
Could one use the formula qualifier as RegEx to describe the allowed format? What about more complex property values, i.e. structs?

A: Currently multi-value properties are not available in the metamodel. As option SME list can be used.
  
  (Answered 2022-08-12)


**[How to define the relationship between asset instance and asset type wrt. corresponding submodels?](#idgh13)** <a id="idgh13"></a>

For AAS, the relation "derivedFrom" should be used. For assets themselves, no such relation is currently available in the meta-model. If a reference to the asset type is needed, it can be solved by specifying some submodel elements (e.g. relation, property, or entity) which should be defined in context of a submodel template if needed.

  (Answered 2022-08-12)

  
**[Can RDF be used as an interchange format?](#idgh59)** <a id="idgh59"></a>
  
Q: RDF in the form of Turtle files is presented in the documentation as one option for presentation of AAS data for semantic purposes. However the "Details of the Asset Administration Shell" document refers to the AAS serializations packaged in an AASX file as "either json or xml". I would be interested in knowing if this is intentional or if RDF/Turtle should be considered equal to json or xml for exchange purposes.
  
A: To our knowledge, JSON/XML can be "lossless" converted to RDF. We consider RDF to be a suitable format for more enhanced applications, e.g. requiring complex queries. So it is just that the focus is a little bit different when to use which format.
  
The RDF scheme/OWL files (.ttl files) are maintained in the repository “aas-spec” of the github project  admin-shell-io: https://github.com/admin-shell-io/aas-specs/tree/master/schemas/rdf. The mapping rules how to derive the RDF schema from the technology neutral meta model as defined in this specification can be found here: https://github.com/admin-shell-io/aas-specs/tree/master/schemas/json#json-mapping-rules. Example files can be found here: https://github.com/admin-shell-io/aas-specs/tree/master/schemas/rdf/examples.
  
  (Answered 2022-08-15)
  
**[Values for externalSubjectId within SpecificAssetId?](#idgh78)** <a id="idgh78"></a>
  
Q: What values shall be used for externalSubjectId within SpecificAssetId?

A: Not all specific IDs shall be visible to all users when looking up Asset Administration Shells. For exam-ple, there typically is a manufacturer-part-ID, but several customer-part-IDs and only the customer shall be able to search for the digital twin via this specific asset ID. The term "subject" is taken from ABAC (Attribute Based Access Control). It is assumed that the "subject" can be described by a unique ID.

 ```
 {"name": "SerialNumber", "value": "12345678", "externalSubjectId": ""} //discoverable for everyone
{"name": "CustomerPartID", "value": "C1#7234", "externalSubjectId": "BPN_Company1"} //discoverable for Company 1
{"name": "CustomerPartID", "value": "0789_Company2", "externalSubjectId": "BPN_Company2"} //discoverable for Company 2
```


  (Answered 2023-06-18)
  
**[How to use ValueIDs?](#idgh77)** <a id="idgh77"></a>
  
Q: How should ValueIDs be using within Submodels to model to model ENUMS from IEC 61360-based semantic dictionaries like CDD and ECLASS?
  
A: In scope of AAS modeling, the concept of ValueIDs should be used to map those ENUMS. Typically enum values have a string representation and an IRDI for unique identification. AAS specs state the following usage guide:
  
```Constraint AASd-007: if both, the value and the valueId are present then the value needs to be identical to the value of the referenced coded value in valueId.```
  
Which can be seen in the example of "IP65" (IEC 61360 english preffered name) as value. Preferred name should be English only - translation can be done by a look-up of the IRDI if needed.
  
![example](https://user-images.githubusercontent.com/69786685/180196523-0ebc7827-cfd3-4ba1-91fd-42af476e926e.png)
  
We encourage using both the string value and the equivalent ValueID to provide best human and machine-readability. The IRDI of the value list itself should be used in submodel template definitions to restrict the allowed string values.
  
  (Answered 2022-08-15)

**[Should one use ECLASS application classes in define semantics of a submodel?](#idgh33)** <a id="idgh33"></a>
  
No, see the [cited document](https://eclass.eu/fileadmin/Redaktion/pdf-Dateien/Broschueren/2021-06-29_Whitepaper_PlattformI40-ECLASS.pdf) (page 29). New defined elements in ECLASS to define Submodels should be used once available. The only exception is to use application/classification classes in submodels is to denote the category of a product (see ProductClassId property example within the TechnicalData Submodel template).

 (Answered 2022-08-15)
 
 **[How to use different versions of the same submodel (e.g. different versions of the "digital nameplate") which share same IdShort?](#idgh72)** <a id="idgh72"></a>

 A: In the current API specification AAS Part 2 V1.0RC03 the unique Submodel Id is expected for a GET/submodels/{submodelIdentifier} and no longer the Submodel IdShort. This enables distinguishing between the particular submodel instance.

 (Answered 2022-11-21)
  
**[What are strategies to match semantic IDs?](#idgh54)** <a id="idgh54"></a>
  
Q: What are strategies to match semantic IDs?

 A: Please refer to section "4.4 Matching Strategies" of [AASiD part 1 v3.0](https://industrialdigitaltwin.org/wp-content/uploads/2023/04/IDTA-01001-3-0_SpecificationAssetAdministrationShell_Part1_Metamodel.pdf). Also, the consensus  of our group is that isCaseOf has no impact on semantic equivalence and can be ignored for automatic matching strategies.

 (Answered 2023-06-19)
  

**[Which code generators work for which programming language?](#id55)** <a id="id55"></a>
  
Q: Which code generators work for which programming language?

 A: Generally, the code generators for server- or client-side code as well for the different programming languages behave surprisingly different to each other. Even though the common foundation is OpenAPI, some used patterns work well for one generator while others cannot understand them. Therefore, this list is without any guarantuee of completeness and is only true for the currently available versions of both the API specification and the respective generators. Also note that even though the SwaggerHub code generation option is handy, it does not always work in the same way as the generators in their latest open source releases.

***Server-side:***

 | Language/Framework | Code Generator | API Versions | Comment |
 |:--|:--|:--|:--|
 | Spring (Java)|  | V3.0.1 | works |
 | jax-rs (Java)|  | V3.0.1 | works |
 | .NET |  | V3.0.1 | works |

***Client-side:***

 | Language/Framework | Code Generator | API Versions | Comment |
 |:--|:--|:--|:--|
 | jax-rs (Java)|  | V3.0.1 | works |
 | .NET |  | V3.0.1 | works |


 (Answered 2023-07-31)
  

**[Which code generators have known issues with the AAS?](#id56)** <a id="id56"></a>
  
Q: Which code generators have known issues with the AAS?

 A: 
***Server-side:***

 | Language/Framework | Code Generator | API Versions | Comment |
 |:--|:--|:--|:--|
 | Spring (Java)|  | V3.0.1 | response 'default' creates methods twice |
 | FLASK (Python) |  | V3.0.1 | throws internal exception |
 | |  |  |  |


***Client-side:***

 | Language/Framework | Code Generator | API Versions | Comment |
 |:--|:--|:--|:--|
 | |  | |  |
 | .NET |  |  | ??? |


 (Answered 2023-07-31)
 
  
## Asset Administration Shell in Detail Series

 [Overview over all parts and versions ](https://www.plattform-i40.de/PI40/Redaktion/EN/Standardartikel/specification-administrationshell.html)

