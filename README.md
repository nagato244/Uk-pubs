# Uk-pubs
install.packages("tidyverse")

library("tidyverse")

library(ggplot2)

library(ggrepel)

read.csv("UK_pubs.csv")

uk_pubs <- read.csv("UK_pubs.csv")

pub_counts <- as.data.frame(table(uk_pubs$pub_name))

colnames(pub_counts) <- c("pub_name", "count")

pub_counts$name_length <- nchar(as.character(pub_counts$pub_name))

top_pub_counts <- pub_counts[order(-pub_counts$count), ][1:50, ]

ggplot(top_pub_counts, aes(x = name_length, y = count)) 
+ geom_point(color = "black", size = 3)
+ geom_text_repel(aes(label = pub_name), size = 3, max.overlaps = 50)
+ labs(title = "Most Frequent Pub Names in the UK", x = "Number of Characters in Pub Name", y = "Frequency of Pub Name")
+ theme_minimal()
+ theme(plot.title = element_text(hjust = 0.5))
+ annotate("text", x = max(top_pub_counts$name_length), y = 1, label = "Source: UK Pubs Dataset", hjust = 1, size = 3, color = "grey")

![image](![Uk pubs](https://github.com/user-attachments/assets/d85b5bcc-b0de-4987-b983-f172f8e5cc62)
