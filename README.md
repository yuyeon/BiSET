# BiSET: Bi-directional Selective Encoding with Template for Abstractive Summarization (ACL 2019)

This paper contains three basic module: **Retrieve**, **FastRerank**, **Bi-selective Encoding**. The following is the usage. 

## Retrieve
The Retrieve module is based on [Apache Lucene](http://lucene.apache.org/), an open source search library. You should first download the core library from the website, and then build the java project. After that, you can index and search on the dataset by following steps:
1. Change the path in the ```Constants.java``` to your directory.
2. Run ```Indexer.java``` to build the index of the trainning set. (This process may cost several days, but only need once.)
3. Run ```Searcher.java``` to search for the candidates and generate the template index files.

## FastRerank
The FastRerank module is implemented with pytorch, before run it, you should first prepare all the data (template index retrieved by **Retrieve** module and the raw dataset).
1. Run ```python config.py --mode preprocess``` to preprocess the data.
2. Run ```python config.py --mode train``` to train the model or ```python config.py --mode train --model modelname``` to finetune a model.(eg. ```python config.py --mode train --model model_final.pkl```)
3. Run ```python config.py --mode dev --model modelname``` to evaluate or test the model and the template with highest score will be stored.

## Bi-selective Encoding
The Bi-selective Encoding module is integrated with [OpenNMT](https://github.com/OpenNMT/OpenNMT-py). Now it only has the bi-selective encoding layer, I will add other three interaction methods (concate, multi-head attention, DCG attention) later. You can directly train it end to end by following steps:
1. Run ```python preprocess.py``` to prepare the data.
2. Run ```python train.py``` to train the model.
3. Run ```python translate.py``` to generate the summaries.

## Notice
1. I have added some comments in the code to help you better understand it. 
2. I refactor my code for clearity and conciseness (rename the variables or class), but I don't have enough time to do a thorough test. If the code has some problems or you have any questions, please raise an issue, I will figure it out whenever I'm
available.
3. For personal communication related to BiSET, please contact me (```wangk73@mail2.sysu.edu.cn```).  
