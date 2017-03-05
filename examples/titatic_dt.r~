#!/usr/local/bin Rscript

data <- read.table("./data/titanic_data.txt", sep = "" , header = F, na.strings ="", stringsAsFactors= F)

colnames(data) <- c("Class", "Age", "Sex", "Survived")
head(data, n = 5)
tail(data, n = 5)

str(data)

library("party")
titanic_ctree <- ctree(Survived ~ Class + Age + Sex, data=data)

print(titanic_ctree)
