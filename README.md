# Dirty-Data
Cleaning Dirty Data
#Anu assignment

getwd()
dirty_data=read.csv("dirty_data.csv")
str(dirty_data)
summary(dirty_data)

#Populate the missing values in the 
#Area variable with an appropriate values (Birmingham, Coventry, Dudley, Sandwell, Solihull, Walsall or Wolverhampton)

#dirty_data = dirty2
dirty_data$`Strange HTML`= NULL

library(sqldf)



#Fn to change the 1st later to Upper case in Street column
capFirst <- function(s) {
  paste(toupper(substring(s, 1, 1)), substring(s, 2), sep = "")
}

dirty_data$Street <- capFirst(dirty_data$Street)
dirty_data$`Street 2` <- capFirst(dirty_data$`Street 2`)


#to remove special characters in Street and Street2
dirty_data$Street <- gsub("[^[:alnum:]///' ]", " ", dirty_data$Street)
dirty_data$`Street 2` <- gsub("[^[:alnum:]///' ]", " ", dirty_data$`Street 2`)

#dirty_data$Street = gsub("\U0334", " ", dirty_data$Street)

#to remove Strange HTML column
dirty_data$`Strange HTML`<-NULL



#removing data in street 2 which has same the data as street column

for(i in 1:nrow(dirty_data))
{
  if(dirty_data$Street[i] == dirty_data$`Street 2`[i])
  {
    dirty_data$`Street 2`[i]=""
  }
  
} 


#To Standardize the street denominations

dirty_data$Street <- gsub(" road", " Road ", dirty_data$Street)
dirty_data$Street <- gsub(" rd", " Road ", dirty_data$Street)
dirty_data$Street <- gsub(" Rd", " Road ", dirty_data$Street)
dirty_data$Street <- gsub(" RD", " Road ", dirty_data$Street)
dirty_data$Street <- gsub(" Raod", " Road ", dirty_data$Street)

dirty_data$Street <- gsub(" lane", " Lane ", dirty_data$Street)
dirty_data$Street <- gsub(" Avenue", " Ave ", dirty_data$Street)
dirty_data$Street <- gsub(" ave", " Ave ", dirty_data$Street)
dirty_data$Street <- gsub(" avenue", " Ave ", dirty_data$Street)

dirty_data$Street <- gsub(" street", " Street ", dirty_data$Street)
dirty_data$Street <- gsub(" STREET", " Street ", dirty_data$Street)
dirty_data$Street <- gsub(" st", " Street ", dirty_data$Street)
dirty_data$Street <- gsub(" St", " Street ", dirty_data$Street)
dirty_data$Street <- gsub(" ST", " Street ", dirty_data$Street)

dirty_data$Street <- gsub("Street reet", " Street ", dirty_data$Street)

dirty_data$Street <- gsub("area", " Area ", dirty_data$Street)



















