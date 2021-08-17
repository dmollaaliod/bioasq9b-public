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

* BioASQ9b paper (TBA)

## Examples of runs using pre-learnt models

To get the pre-learnt models used in the BioASQ8b runs, please email
diego.molla-aliod@mq.edu.au. The following models are available:
    * task8b_bert_model_32.pt - for neural classification with BERT 
    * task8b_biobert_model_32.pt - for neural classification with BioBERT 
    * task8b_distilbert_model_32.pt - for neural classification with DistilBERT 


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

| Method | Batch size | Dropout | Epochs | Mean SU4 F1 | Std SU4 F1 |
| --- | ---: | ---: | ---: | ---: | ---: |
| BERT  | 32 | 0.8 | 8 |  |  |
| BioBERT | 32 | 0.7 | 1 |  |  |
| DistilBERT | 32 | 0.6 | 1 |  |  |

## Reinforcement Learning (PPO)

Requires installing stable baselines (and huggingface transformers if using BERT)
```
pip install stable-baselines
pip install transformers
```

PPO (load best run bioasq8b from root directory):
```
python -m rl.ppo_stablebaselines --8b --observe EMBEDDINGS --model PPO2 --batch_size=1000 --append _best --bestaction --load TEST
```
PPO (generate best run bioasq8b from root directory):
```
python -m rl.ppo_stablebaselines --8b --observe EMBEDDINGS --model PPO2 --batch_size=1000 --append _best --bestaction
```
PPO (BERT bioasq8b):
```
python -m rl.ppo_stablebaselines --8b --observe BERT --model PPO2 --batch_size=1000 --bestaction
```


## Who do I talk to? ###

Diego Molla: [diego.molla-aliod@mq.edu.au](mailto:diego.molla-aliod@mq.edu.au)
