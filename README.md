# German Sustainability Code (DNK) data set

This repository contains the German Sustainability Code (DNK) data set used in the paper 
"sustain.AI: a Recommender System to analyze Sustainability Reports".

The `gzip` compressed `json` file contains 1779 German sustainability reports that we sourced from 
the publicly available database of the [German Sustainability Code](https://www.deutscher-nachhaltigkeitskodex.de/Home/Database) 
(in German: Deutscher Nachhaltigkeitskodex - DNK).

The platform is used by the majority of German companies to annually disclose their sustainability activities 
with respect to 33 requirements from 20 DNK criteria, e.g. usage of natural resources and human rights.

We accessed the database on February 25th, 2022, downloaded the raw reports in `html` format and saved them as `json` after finishing the parsing.
Each report is represented as a list of text segments where all segments are automatically annotated with their specific requirement label from the DNK checklist.
A segment can be a headline, paragraph or table.

Using `python` the `dnk_data.json.gz` file can be read like so:
```python
import gzip
import json

with gzip.open("path/to/file/dnk_data.json.gz", "rt") as fp:
    data = json.loads(fp.read())
```

The structure of the file is as follows:
```yaml
reports:  # List[Dict]
  - id_: report_id  # str
    split: train | validation | test  # str
    content:  # List[Dict]
      - id_: segment_id  # int
        type_: headline | paragraph | table  # str
        content: segment_text  # str
        requirement_id:  annotation id in checklist  # str
      - ...
  - ...

checklist:  # Dict
  description: description of checklist  # str
  requirements:  # List[Dict]
    - id_: requirement_id  # str
      description: definition of requirement  # str
      short_description: short definition  # str
    - ...
```

We publish this data set under the MIT license.
If you make use of it in your research, please consider citing.
```
@article{sustain_ai2023,
  title = {sustain.AI: a Recommender System to analyze Sustainability Reports},
  author = {Hillebrand, Lars and Pielka, Maren and Leonhard, David and Deu{\ss}er, Tobias and Dilmaghani, Tim and Kliem, Bernd and Loitz, R{\"u}diger and Morad, Milad and Temath, Christian and Bell, Thiago and Stenzel, Robin and Sifa, Rafet},
  booktitle={Proc. ICAIL},
  year = {2023}
}
```
