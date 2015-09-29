# Online-FLORS

Brief Intro: 

   FLORS performs good for domain adaptation. Its online version first trains a model on some training data (with optionally auxiliary
   labeled or unlabeled data only for robust representation learning); during predicting, for an incoming sentence, the 
   model updates word representations based on the info of that sentence, then predicts this sentence. 

Usage:

    -h: for help
		-mode: 'train' or 'predict'
		-trainFile: the names or paths for the training labeled files, separated by space
		-labeledData: optional; supporting tagged files for making the model more robust, separated by tab
		-unlabeledData: optional; supporting untagged files for making the model more robust, separated by tab
		-bigData: optional; supporting untagged files for making the model more robust, separated by space
		-window: optional; length of window (default is '5')
		-sampleNo: (any number vs. 'all'); optional; the number of tokens you want to use for training; default is 'all'
		-labeled: (1 vs. 0); optional; predict the POS taggs for tagged data? Default is '0'
		-predictFile: the name or path of the corpus to be predicted
		-update: (1 vs. 0); optional; whether to incrementally update; default is '1'
		-pre: (any string); for both train and predict; optional; to mark the prefix of files to be written; default is empty string
		-out: (any string); only for predict; optional; the path of output file; default is output.txt




Command example for training (replicate the results on dev sets of SANCL):

    java -jar train_20150414.jar -mode train -trainFile ontonotes-wsj-train -unlabeledData wsj_ul.100k gweb-newsgroups.unlabeled gweb-reviews.unlabeled gweb-weblogs.unlabeled gweb-answers.unlabeled gweb-emails.unlabeled gweb-wsj.unlabeled -labeledData gweb-newsgroups-test gweb-reviews-test gweb-weblogs-test gweb-answers-test gweb-emails-test gweb-wsj-test -bigData English_Gigawords_500k.txt -pre prefix_

Command example for online predicting (replicate the results on dev sets of SANCL):

    java -jar predict_online_1.jar -mode predict -predictFile labeled_to_be_predict.txt -labeled 1 -update 1 -pre prefix_ -out output.txt

Data format:

1) labeled file, e.g., "ontonotes-wsj-train" after "-trainFile" or "gweb-newsgroups-test" after "-labeledData" in above command line

The standard format in SANCL and WSJ. i.e., file contains two columns, first column is single words, second column is gold tag, word and tag are separated by a \tab. There is one empty line between sentences. For example:

				of	IN
				the	DT
				entire	JJ
				center	NN
				.	.
				
				The	DT
				combined	VBN
				operations	NNS
				had	VBD
				1988	CD
				revenue	NN
				of	IN
				about	RB
				$	$
				100	CD
				million	CD
				.	.
				
				In	IN
				fact	NN
				,	,
				he	PRP
				liberated	VBD
				the	DT

2) Unlabeled Data. e.g., "wsj_ul.100k" after "-unlabeledData" 

				File with sentences, each sentence lies in one row, and words are separated by one \tab. 

3) unlabeled big data. e.g., "English_Gigawords_500k.txt" after "-bigData"

				The same with "Unlabeled Data", except for replacing \tab with a space


4) The format of "output.txt" in prediction, i.e., "-out output.txt"

				shellac	0	NN	NN	0
				78's	0	NNS	NNP	0	wrong
				through	1	IN	IN	k
				this	1	DT	DT	k
				little	1	JJ	JJ	k
				integrated	1	JJ	JJ	k
				-	1	,	HYPH	u	wrong

This file contains multiple columns: rowToken, known?, goldTag, predictedTag, tagFlag, wrong; separated by \tab

		known?=0 or 1, "0" means unkown word, "1" means known word.
		tagFlag=u or k or 0, "u" means unknown tag for a known word, "k" means known tag for known word, "0" means tag for unknown word.
		wrong="wrong" or empty. "wrong" means false prediction. Otherwise, the column is left empty

Citation:
 
          @inproceedings{wenpeng-2015-flors,
          title={Online Updating of Word Representations for Part-of-Speech Taggging},
          author={Yin, Wenpeng; Schnabel, Tobias; Schütze, Hinrich},
          booktitle={Proceedings of the 2015 Conference on Empirical Methods in Natural Language Processing (EMNLP)},
          year={2015}
          }




Contact:
             Wenpeng Yin (mr.yinwenpeng@gmail.com)
