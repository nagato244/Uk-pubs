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



# mad questionary

install.packages("tidyverse")

library("tidyverse")

library(ggplot2)

read.csv("mad_questionary.csv")

data <- read.csv("mad_questionary.csv")

data$sex <- tolower(data$sex)

data$sex[data$sex %in% c('ж', 'женский', 'жен', 'женщина')] <- 'женский'

data$sex[data$sex %in% c('м', 'мужской')] <- 'мужской'

data$age <- as.numeric(data$age)

non_numeric_ages <- data[is.na(as.numeric(data$age)), "age"]

non_numeric_ages

data <- data[!is.na(as.numeric(data$age)), ]

data$age <- trimws(data$age)

data$age <- as.numeric(data$age)

ggplot(data, aes(x = age, fill = sex)) 
+ geom_dotplot(binwidth = 1, method = "histodot", stackgroups = TRUE)
+ scale_fill_manual(values = c("женский" = "salmon", "мужской" = "skyblue"))
+ labs(x = "Age", fill = "Sex") + theme_minimal()
+ scale_y_continuous(NULL, breaks = NULL) + theme(axis.text.y = element_blank(), axis.ticks.y = element_blank())

![image](![mad questionary](https://github.com/user-attachments/assets/bf7e521b-b6b7-4617-8583-4ce972efd04d)
