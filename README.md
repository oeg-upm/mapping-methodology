# mapping-methodology
This repository contains a script to create a crosswalk between Codemeta and another specification or vocabulary, as well as some examples of generation.

The methodology for generating the files required to create the crosswalk is as follows:
1. **Identify the Terms to Map**<br>
Identify the terms you want to map in both semantic artifacts (source and target).
2. **Create a YAML Metadata File**<br>
Create a YAML metadata file that contains the metadata of the mapping using the provided template: mapping-template.yml.
Name the file appropriately, for example, codemeta-bibtext-mapping.yml.
3. **Complete the Required Metadata Fields**<br>
- mapping_date: The date when the mapping was created (use ISO XXXX format).
- mapping_set_description: A description of the mapping, including references to the involved domains and the purpose of the mapping.
- mapping_provider: Information about the entity responsible for the mapping. Include a URI if possible.
- mapping_set_id: The URI of the mapping (see next step). Consider using persistent identifiers instead of standard URIs. A persistent identifier can be minted using the w3id.org project. Please, add it in the project codemeta/crosswalks
- object_source: The URI of the specification or vocabulary. Use persistent identifiers whenever possible.
4. **Create the Data File (CSV Format)**<br>
Name the CSV file appropriately, for example, codemeta-bibtext-mapping.csv.
The CSV file should contain the following columns:
source_term: The term in CodeMeta.
target_term: The corresponding term in the target specification or vocabulary.
type_relation: The type of relation between the two terms. Possible values:
same_as: The terms are equivalent concepts.
part_of: The target concept is part of the source concept (e.g., a publication year in the target vocabulary is part of a publication date in the source vocabulary).
Important Note: Each line in the CSV file should represent only one relation between terms.
For example, if the source vocabulary has the concept date, and the target vocabulary has year and month, the CSV should contain two separate lines:
date -> year (with the part_of relation)
date -> month (with the part_of relation)
5. **Generate the SSSOM File**<br>
Execute the script (generate_crosswalk.py) to generate an .sssom.tsv file from the CSV.
```bash
python .\generate_crosswalk.py examples/bibtex-codemeta-mappings.yaml examples/bibtex-codemeta-mappings.csv