library(dplyr)

df1<-read.csv(file.choose(),header = TRUE, na.strings = "NA",",")
View(df1)

df2<-read.csv(file.choose(),header = TRUE, na.strings = "NA",",")
View(df2)

df4<-left_join(df1, df2, by ='gene')
df4
View(df4)

#to drop NA

library(tidyr)
df5<-df4[!is.na(df4$symbol),]
View(df5)


write.csv(df5,file ="1sar1y3snp.csv" )
#write.csv(df5,"C:\\Users\\Computer\\Desktop\\People_3.csv", row.names = FALSE)

#to drop rows with zeros in all colums

df5 <- df5 %>% 
  rowwise() %>% 
  filter(sum(c(variants_effect_missense_variant,variants_effect_splice_acceptor_variant,variants_effect_splice_donor_variant,variants_effect_start_lost,variants_effect_stop_gained,variants_effect_stop_lost)) != 0)
View(df5)


write.csv(df5,file ="SAR1_snp.csv" )
