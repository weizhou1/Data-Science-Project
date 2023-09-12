# About the Data
## COMP2420 Semester 1, 2020
## Assignment 1

The following document is designed to give you an introduction to the data you
are working with, including the references for data generation.

## Data Table
The below table provides an outline of the data, broken down into the columns
the dataset features. Additional information regarding the schemas and sets used
will be provided in the next section.

| Column Name    | Description    |
| :------------- | :------------- |
| product.name   | The name of the affected product       |
| cve.id         | The CVE identifier for the vulnerability |
| product.versions | List of the affected product versions |
| vendor.name    | The name of the vendor who produces the product |
| cwe.id         | The CWE identifier of the vulnerability |
| product.description | A description of the vulnerability |
| reference.url  | A url link to the initial posting of the vulnerability |
| v3_attackComplexity | CVSSv3 field, identifier for the difficulty of performing an attack using the vulnerability |
| v3_attackVector | CVSSv3 field, identifier for how the vulnerability would be used in an attack |
| v3_availabilityImpact | CVSSv3, field, identifier for the impact upon the availability of information in the product/service after using the vulnerability |
| v3_confidentialityImpact | CVSSv3 field, identifier for the impact upon the confidentiality of information in the product/service after using the vulnerability |
| v3_integrityImpact | CVSSv3 field, identifier for the impact upon the integrity of information in the product/service after using the vulnerability |
| v3_baseScore | CVSSv3 field, the score (out of 10) given to the vulnerability |
| v3_privilegesRequired | CVSSv3 field, an identifier for the privileges required in the system to use the vulnerability successfully |
| v3_scope | CVSSv3 field, an identifier for whether the scope of an item changes when using the vulnerability. EG: whether a regular user becomes a superuser. |
| v3_userInteraction | CVSSv3 field, an identifier for whether a user needs to actively interact for the vulnerability to be exploited or not |
| v2_accessComplexity | CVSSv2 field, identifier for the difficulty of using the vulnerability |
| v2_accessVector  | CVSSv2 field, identifier for how the vulnerability would be used |
| v2_authentication | CVSSv2 field, measures the number of times an attacker must authenticate to a target in order to exploit a vulnerability |
| v2_availabilityImpact | CVSSv2 field, identifier for the impact upon the availability of information in the product/service after using the vulnerability |
| v2_confidentialityImpact | CVSSv2 field, identifier for the impact upon the confidentiality of information in the product/service after using the vulnerability |
| v2_integrityImpact | CVSSv2 field, identifier for the impact upon the integrity of information in the product/service after using the vulnerability |
| v2_baseScore | CVSSv2 field, the score (out of 10) given to the vulnerability |
| capec.classes | A list of the potential attack vectors that could be used to exploit this CVE, based on the CWE. |


**Note:** While this data should have 24 columns, your version only has 22. `v3_baseScore` and `v2_baseScore` have been purposely omitted (see Question 2 of the Assignment).


## Schema Descriptions
In the table above, a large number of schemas (such as CVE, CWE, CVSS) are
referenced. The following is designed to give you an introduction to these
systems and links for further reading as required.

### Common Vulnerability and Exposure (CVE)
The CVE system was developed by MITRE almost 20 years ago, and is now
the de-facto system for providing identifiers for vulnerabilities in various
systems. For the purposes of this assignment, the data is a CVE-variant form,
however the CVE identifier (in the data as `cve.id`) is still present. Note that
multiple rows can have the same `cve.id`, as a row is unique to a product and
CVE.id.

A CVE can affect multiple products and multiple software versions of a product,
and therefore the data is split to have the key `(product.name, cve.id)`. All
instances of `(product.name, cve.id)` are unique.

Further reading on the CVE system can be found on
[Mitre's CVE website](https://cve.mitre.org/).

### Common Weakness Enumeration (CWE)
The CWE system is used to define the weakness a vulnerability/exposure exploits.
Also developed by MITRE in the early 2000s, the system itself is used to
manually determine the weakness a vulnerability uses. (Yes, manually. We might
come back to this later)

Each CWE identifier is related to a specific weakness, which will have it's own
unique characteristics. More information on the CWE system can be found on
[Mitre's CWE website](https://cwe.mitre.org/).

Note that while over 1000 CWE identifiers exist, only a small subset will be
present within our dataset. This is due to the NVD using their own subset of
them, which can be found on the
[NVD website](https://nvd.nist.gov/vuln/categories)


### Common Vulnerability Scoring System (CVSS)
The CVSS system is the de-facto scoring system for determining the impacts
of vulnerabilities in the CVE system. Developed by the Forum of Incident
Response and Security Teams (FIRST), the CVSS system is now in it's
3<sup>rd</sup> major iteration (version 3). However, since the 3<sup>rd</sup>
iteration came out only recently (~2015) and adoption is slow, there are still
instances of version 2 in the wild. Therefore, both versions are present in
our dataset.

Note that we only use the base metrics of the CVSS system. While there are
additional metrics that can be applied, most are variants.
Therefore, we will use the base metrics.

Some entries will have scoring in the version 2 (v2) and version 3 (v3) systems.
Further information on the scoring systems can be found at the following:
- [Version 2 Schema](https://www.first.org/cvss/v2/guide#Metric-Groups)
- [Version 3 Schema](https://www.first.org/cvss/v3.0/specification-document#Base-Metrics)

Note: CVSS is currently at v3.1, however the dataset we use are on v3.0.
Therefore, v3.0 applies.

### Common Attack Pattern Enumeration and Classification (CAPEC)
Lastly, the CAPEC system. The CAPEC system was (also) developed by MITRE,
and provides identifiers for the types of attacks that can be performed. This
is currently linked through the CWE system, as no one (as of yet) has ever tried
to document the CAPEC identifier for CVE entries. (If you're interested in this,
talk to Alex or Ramesh regarding individual projects)

More information on the CAPEC system can be found on
[Mitre's CAPEC website](https://capec.mitre.org/index.html).


## Miscellaneous References

- The data was originally scraped from the National Vulnerability Database on the 11<sup>th</sup> of February, 2020. The dataset used in this piece is restricted to a subset of 8,000 records.
- Data Scraping and modelling tools were developed by Alex Niven in 2019 in the project _Scientific Rigour in Cryptographic Evaluations_
