

The R development environment is implemented using Docker.


NOTICE 1: Titanic_data.txt (CSV and DOC) is from https://vincentarelbundock.github.io/Rdatasets/datasets.html.

NOTICE 2: The DecisionTree (iris) example is found in http://www.rdatamining.com/examples/decision-tree.


Please follow the instructions below to run the example (titanic_dt.r).

[1] download (or git clone ) this source code folder.

[2] cd downloaded-source-code-folder

[3] sudo make BIND_DIR=.  shell

	wait ... wait ... then a bash shell will be ready (root@054d8a617a6d:/#)

[4] root@054d8a617a6d:/# cd /home/ml/R/

[5] root@054d8a617a6d:/home/ml/R# cd R-3.3.2/

[6] root@054d8a617a6d:/home/ml/R/R-3.3.2# ./configure

[7] root@054d8a617a6d:/home/ml/R/R-3.3.2# make

[8] root@054d8a617a6d:/home/ml/R/R-3.3.2# make install

[9] root@054d8a617a6d:/home/ml/R/R-3.3.2# ln -s /usr/local/bin/R /usr/bin/R 

[10] root@054d8a617a6d:/home/ml/R/R-3.3.2# cd ..

[11] root@054d8a617a6d:/home/ml/R# R CMD INSTALL mvtnorm_1.0-6.tar.gz

[12] root@054d8a617a6d:/home/ml/R# R CMD INSTALL modeltools_0.2-21.tar.gz

[13] root@054d8a617a6d:/home/ml/R# R CMD INSTALL zoo_1.7-14.tar.gz  

[14] root@054d8a617a6d:/home/ml/R# R CMD INSTALL sandwich_2.3-4.tar.gz 

[15] root@054d8a617a6d:/home/ml/R# R CMD INSTALL strucchange_1.5-1.tar.gz

[16] root@054d8a617a6d:/home/ml/R# R CMD INSTALL TH.data_1.0-8.tar.gz

[17] root@054d8a617a6d:/home/ml/R# R CMD INSTALL multcomp_1.4-6.tar.gz

[18] root@054d8a617a6d:/home/ml/R# R CMD INSTALL coin_1.1-3.tar.gz

[19] root@054d8a617a6d:/home/ml/R# R CMD INSTALL ./party/ 

[20] root@054d8a617a6d:/home/ml/R# cd examples/

[21] root@054d8a617a6d:/home/ml/R/examples# Rscript ./titatic_dt.r

[22] The output looks like


	... entering the main-loop ...

 	... in mainloop ... 

 	... in setup_Rmainloop ... 

 	... in run_Rmainloop ... 
  	Class Age Sex Survived
	1     1   1   1        1
	2     1   1   1        1
	3     1   1   1        1
	4     1   1   1        1
	5     1   1   1        1
     	Class Age Sex Survived
	2197     0   1   0        1
	2198     0   1   0        1
	2199     0   1   0        0
	2200     0   1   0        0
	2201     0   1   0        0
	'data.frame':	2201 obs. of  4 variables:
	 $ Class   : int  1 1 1 1 1 1 1 1 1 1 ...
	 $ Age     : int  1 1 1 1 1 1 1 1 1 1 ...
	 $ Sex     : int  1 1 1 1 1 1 1 1 1 1 ...
	 $ Survived: int  1 1 1 1 1 1 1 1 1 1 ...
	Loading required package: methods
	Loading required package: grid
	Loading required package: mvtnorm
	Loading required package: modeltools
	Loading required package: stats4
	Loading required package: strucchange
	Loading required package: zoo

	Attaching package: 'zoo'

	The following objects are masked from 'package:base':

    	as.Date, as.Date.numeric

	Loading required package: sandwich

	 ... in C_TreeGrow ... 

	 ... in C_TreeGrow ... 

	 ... in C_TreeGrow ... 

	 ... in C_TreeGrow ... 

	 ... in C_TreeGrow ... 

	 ... in C_TreeGrow ... 

	 ... in C_TreeGrow ... 

	 ... in C_TreeGrow ... 

	 ... in C_TreeGrow ... 

	 ... in C_TreeGrow ... 

	 ... in C_TreeGrow ... 

	 ... in C_TreeGrow ... 

	 ... in C_TreeGrow ... 

	 ... in C_TreeGrow ... 

	 ... in C_TreeGrow ... 

	 	Conditional inference tree with 8 terminal nodes

	Response:  Survived 
	Inputs:  Class, Age, Sex 
	Number of observations:  2201 

	1) Sex <= 0; criterion = 1, statistic = 456.667
  		2) Class <= 2; criterion = 1, statistic = 105.253
    			3)*  weights = 274 
  		2) Class > 2
    			4)*  weights = 196 
	1) Sex > 0
  		5) Age <= 0; criterion = 1, statistic = 23.112
    			6) Class <= 2; criterion = 1, statistic = 21.731
      				7)*  weights = 16 
    			6) Class > 2
      				8)*  weights = 48 
  		5) Age > 0
    			9) Class <= 1; criterion = 0.998, statistic = 12.1
      				10) Class <= 0; criterion = 0.989, statistic = 8.446
        				11)*  weights = 862 
      				10) Class > 0
        				12)*  weights = 175 
    			9) Class > 1
      				13) Class <= 2; criterion = 0.965, statistic = 6.329
        				14)*  weights = 168 
      				13) Class > 2
        				15)*  weights = 462 


[23] To disable the message that says "... in run_Rmainloop ...", open R-3.3.2/src/main/main.c in the local machine (or in Docker) and comment out line #1059 printf("\n ... in run_Rmainloop ... \n");.

[24] To disable "... in C_TreeGrow ...", open party/src/TreeGrow.c in the local machine and comment out line #30  printf("\n ... in C_TreeGrow ... \n");.

[25] Repeat the steps [7], [8], and [19].
 

The example R script is as follows.


	#!/usr/local/bin Rscript

	data <- read.table("./data/titanic_data.txt", sep = "" , header = F, na.strings ="", stringsAsFactors= F)

	colnames(data) <- c("Class", "Age", "Sex", "Survived")
	head(data, n = 5)
	tail(data, n = 5)

	str(data)

	library("party")
	titanic_ctree <- ctree(Survived ~ Class + Age + Sex, data=data)

	print(titanic_ctree)

