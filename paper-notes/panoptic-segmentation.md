# Panoptic segmentation

1. Stuff vs things - stuff: not: countable and things: countable
2. Scene parsing, image parsing, holistic scene understanding


Panoptic segmetnation
1. Both stuff and things
2. Simple but general output format
3. Simple uniform evaluation metric


## Label format
Targets:
1. Semantic id and instance id

Challenges:
1. Each pixel can have only have instance
2. Instances must be non-overlapping


Good thing:
1. Evaluation with human performance easy


## Comparison to other approaches
1. Not multi-task! Rather, it's unified
2. Semantic segmentation: this has instances
3. Instance segmentation: there


### Datasets already supported
1. Cityspaces


### Output format
1. Tuple: semantic label x instance id
2. If the semantic label is from one of the "stuff" classes, ignore instance id
3. Drop the classification scores

How is the tuple predicted?
- is it classification or regression? How to know how many instances
    are there?


### Metric
1. Segment matching
    1. Pick 0.5 IoU threshold for the intersection so that there is only
        one matching
2. Panoptic Quality measurement
    1. All segments receive equal weights regardless of the area
    2. Similar to F1 score
