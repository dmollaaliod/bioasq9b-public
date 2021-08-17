# bioasq9b

## What is this repository for? ###

This code implements Macquarie University's experiments and
participation in BioASQ 9b.
* [BioASQ](http://www.bioasq.org)
* [Learn Markdown](https://bitbucket.org/tutorials/markdowndemo)

## How do I get set up? ###

Apart from the code in this repository, you will need the following files:

* `training9b.json` - available from [BioASQ](http://www.bioasq.org/)
* `rouge_9b.csv` - you can create it by running the following overnight:
```
>>> from regression import saveRouge
>>> saveRouge('training9b.json', 'rouge_9b.csv',
               snippets_only = True)
```

Read the file `Dockerfile` for an idea of how to install the dependencies and
set up the system.

## Reading

If you use this code, please cite the following paper:

D. Mollá, U. Khanna, D. Galat, V. Nguyen, M. Rybinski (2021). Query-Focused Extractive Summarisation for
Finding Ideal Answers to Biomedical and COVID-19
Questions. *CLEF2021 Working Notes*. [[local copy](CLEF2021Paper.pdf)]

## Examples of runs using pre-learnt models

To get the pre-learnt models used in the BioASQ8b runs, please email
diego.molla-aliod@mq.edu.au. The following models are available:

* task9b_bert_model_32.pt - for BERT 
* task9b_biobert_model_32.pt - for BioBERT 
* task9b_distilbert_model_32.pt - for DistilBERT 
* task9b_albert_model_32.pt - for ALBERT
* task9b_qaalbert9b_model_32.pt - for QA_ALBERT


### BERT

```
>>> from classificationneural import bioasq_run
>>> bioasq_run(test_data='BioASQ-task8bPhaseB-testset1.json', model_type='bert', output_filename='bioasq-out-bert.json')
```



## Examples of cross-validation runs and their results

Below are 10-fold cross-validation results using the BioASQ9b training data.

```
rm diego.out; for F in 1 2 3 4 5 6 7 8 9 10; do python classificationneural.py -t BERT --dropout 0 --nb_epoch 5 --batch_size 32 --fold $F >> diego.out; done
```

And similar for the other neural approaches.

| Method | Batch size | Dropout | Epochs | Mean SU4 F1 |
| --- | ---: | ---: | ---: | ---: |
| BERT  | 32 | 0.8 | 8 | 0.2779 |  
| BioBERT | 32 | 0.7 | 1 | 0.2798 |  
| DistilBERT | 32 | 0.6 | 1 | 0.2761 | 
| ALBERT | 32 |0.5 | 5 | 0.2866 |
| ALBERT-SQuAD | 32 | 0.7 | 5 | 0.2846 |
| QA_ALBERT | 32 | 0.4 | 5 | 0.2875 |

## Who do I talk to? ###

Diego Molla: [diego.molla-aliod@mq.edu.au](mailto:diego.molla-aliod@mq.edu.au)
