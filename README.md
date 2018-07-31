This is an open source implementation of the Bilingual Distributed
Representations without Word Alignments method described in the
paper cited below.


http://arxiv.org/abs/1410.2455

BilBOWA: Fast Bilingual Distributed Representations without Word Alignments

Stephan Gouws, Yoshua Bengio, Greg Corrado


We introduce BilBOWA ("Bilingual Bag-of-Words without Alignments"),
a simple and computationally-efficient model for learning bilingual
distributed representations of words which can scale to large datasets
and does not require word-aligned training data. Instead it trains
directly on monolingual data and extracts a bilingual signal from a
smaller set of raw text sentence-aligned data. This is achieved using
a novel sampled bag-of-words cross-lingual objective, which is used to
regularize two noise-contrastive language models for efficient
cross-lingual feature learning. We show that bilingual embeddings
learned using the proposed model outperforms state-of-the-art methods
on a cross-lingual document classification task as well as a lexical
translation task on the WMT11 data. Our code will be made available as
part of an open-source toolkit.

arXiv:1410.2455
Submitted on 9 Oct 2014


## Compiling and using `Bilbowa`
To compile, do the following

    cd bilbowa
    make all

This creates `bilbowa` and `bidist` in the `bin` directory. 
Run `bilbowa` to see the list of command line options.
`bidist` is a modification of the distance module in the [word2vec package](https://github.com/danielfrg/word2vec). It receives 2 binary vectors (let's say English and French) as input, and for any given English word returns the list of the similar French words. Note that similar to the original distance module, it only works with the binary vectors (use `-binary 1` switch when calling `bilbowa` to train the system.)

## Generation result

```bash
$ ./bilbowa -mono-train1 endata.txt -mono-train2 esdata.txt -par-train1 enes.en -par-train2 enes.es -output1 envec.txt -output2 esvec.txt -size 300 -window 5 -sample 1e-4 -negative 5 -binary 0 -adagrad 1 -xling-lambda 1 -epochs 10 -threads 3 -negative 5 -save-vocab1 en.vocab -save-vocab2 es.vocab -min-count 1
Learning Vocab
pre SortVocab
Vocab size: 3378
Words in train file: 1174846
Done learning vocab
Saving vocab
Saving vocabulary with 3378 entries to en.vocab
Initializing net....done.
Initializing unigram table....done.
Learning Vocab
pre SortVocab
Vocab size: 2985
Words in train file: 1086334
Done learning vocab
Saving vocab
Saving vocabulary with 2985 entries to es.vocab
Initializing net....done.
Initializing unigram table....done.
Starting training.
Alpha: 0.025000  Progress: 99.12%  (epoch 9) Updates (L1: 11.73M, L2: 11.75M) L1L2grad: 0.1533 Words/sec: 2.99K  
Saving model to file: envec.txt

Saving model to file: esvec.txt
TrainModel() took 2136.58 seconds to execute 
```