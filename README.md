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

Contact:
             Wenpeng Yin (mr.yinwenpeng@gmail.com)
