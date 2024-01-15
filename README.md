# test
test
install.packages("readxl")
library(readxl)
D <- read_excel("Организации.xlsx")
View(D)
R <- D$`Площадь помещений в собственности, кв.м`
sum(R)

install.packages("rpivotTable")
library(rpivotTable)

rpivotTable::rpivotTable(D,rows = 'Округ',
                         vals = 'Площадь помещений в собственности, кв.м',
                         aggregatorName='Sum')

Q <- read_excel('Конфеты.xls')
View(Q)

#Рассчитать суммарную стоимость конфет 
#в разбивке по сорту шоколада

rpivotTable::rpivotTable(Q,rows = 'Сорт шоколада',
      aggregatorName = 'Sum', vals = 'Стоимость')

#Рассчитать среднюю стоимость конфет 
#в разбивке по сорту шоколада с детализацией 
#по сорту начинки
rpivotTable::rpivotTable(Q,rows = c('Сорт шоколада','Сорт начинки'),
                         aggregatorName = 'Average', vals = 'Стоимость')

rpivotTable::rpivotTable(Q,rows = c('Сорт шоколада'),
                         cols = 'Сорт начинки',
                         aggregatorName = 'Average', vals = 'Стоимость')

#Рассчитать суммарную стоимость всех конфет
rpivotTable::rpivotTable(Q,
                         aggregatorName = 'Sum', 
                         vals = 'Стоимость')
sum(Q$Стоимость)

#Рассчитать среднюю стоимость конфет, 
# у которых нет начинки

sum(Q$Стоимость[Q$`Сорт начинки` == 'Нет'])

P <- data.frame(Q$Название[Q$`Сорт начинки` == 'Нет'],
                Q$Стоимость[Q$`Сорт начинки` == 'Нет'])
View(P)
colnames(P)<-c('Название', 'Стоимость')
