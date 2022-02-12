# MyScRiPtt
this is my last work script, ENJOY!!!!!
install.packages("plyr")
options(digits = 2)
data <- read.delim("clipboard", header = TRUE)
data_sorted 		<- data[order(data$Member),]
data_sorted$Member	<- as.numeric(data_sorted$Member)
library(plyr)
data_sorted
View(data_sorted)
data_itemList <- ddply(data,"Member", 
                       function(df1)paste(df1$Item, 
                                          collapse = ","))
write.csv(data_itemList,"ItemList.csv", quote = FALSE, row.names = TRUE)
install.packages("arules")
install.packages("arulesViz")
View(data_itemList)

library(arules)
library(arulesViz)
txn = read.transactions(file="ItemList.csv", rm.duplicates= TRUE, format="basket",sep=",",cols = 1);
txn@itemInfo$labels <- gsub("\"","",txn@itemInfo$labels)
apriori(txn)
inspect()
write.csv(data_itemList,"D:/Skripsi/APRIORI/data data/dataitemlist.csv", quote = FALSE, row.names=TRUE)
########################## pembentukan Frequent Itemsets ################################################

basket_rules <- apriori(txn,parameter = list(sup = 0.01,minlen=1, conf = 0.8,target="frequent itemsets"))
basket_rules_2 <- apriori(txn,parameter = list(sup = 0.01,minlen=2, conf = 0.8,target="frequent itemsets"))
basket_rules_3 <- apriori(txn,parameter = list(sup = 0.01,minlen=3, conf = 0.8,target="frequent itemsets"))
basket_rules_4 <- apriori(txn,parameter = list(sup = 0.01,minlen=4, conf = 0.8,target="frequent itemsets"))
basket_rules_5 <- apriori(txn,parameter = list(sup = 0.01,minlen=5, conf = 0.8,target="frequent itemsets"))

######################### Pembentukkan Rules ############################################################
basket_rules_AR <- apriori(txn,parameter = list(sup = 0.01,minlen=1,conf = 0.8,target="rules"))
write.csv(df_basket,"D:/Skripsi/APRIORI/data data/rules1.csv", quote = FALSE, row.names=TRUE)
basket_rules_3 <- apriori(txn,parameter = list(sup = 0.01,minlen=3, conf = 0.5,target="rules"))
basket_rules_777 <- apriori(txn,parameter = list(sup = 0.01, conf = 1 ,target="rules"))

inspect(basket_rules)
inspect(basket_rules_AR)
inspect(basket_rules_2)
inspect(basket_rules_3)
inspect(basket_rules_4)
inspect(basket_rules_5)
inspect(basket_rules_777)
################################################################################################
df_basket <- as(basket_rules,"data.frame")
df_basket_AR <- as(basket_rules_AR,"data.frame")
df_basket_rs <- as(basket_rules_rs,"data.frame")
df_basket_2 <- as(basket_rules_2,"data.frame")
df_basket_3 <- as(basket_rules_3,"data.frame")
df_basket_4 <- as(basket_rules_4,"data.frame")
df_basket_777 <- as(basket_rules_777,"data.frame")


df_basket <- as(basket_rules,"data.frame")
write.csv(df_basket,"D:/Skripsi/APRIORI/data data/frequent 1.csv", quote = FALSE, row.names=TRUE)

df_basket_2 <- as(basket_rules_2,"data.frame")
write.csv(df_basket_2,"D:/Skripsi/APRIORI/data data/frequent 2.csv", quote = FALSE, row.names=TRUE)

df_basket_3 <- as(basket_rules_3,"data.frame")
write.csv(df_basket_3,"D:/Skripsi/APRIORI/data data/frequent 3.csv", quote = FALSE, row.names=TRUE)

df_basket_4 <- as(basket_rules_4,"data.frame")
write.csv(df_basket_4,"D:/Skripsi/APRIORI/data data/frequent 4.csv", quote = FALSE, row.names=TRUE)
###############################################################################################

df_basket_777$confidence <- df_basket_777$confidence*100
df_basket_777$support <- df_basket_777$support*100
View(df_basket)
View(df_basket_AR)
View(df_basket_rrr)
write.csv(df_basket_777,"D:/Skripsi/APRIORI/data data/rules.csv", quote = FALSE, row.names=TRUE)
View(df_basket_2)
View(df_basket_3)
View(df_basket_4)
View(df_basket_777)
itemFrequencyPlot(txn, topN = 10)

