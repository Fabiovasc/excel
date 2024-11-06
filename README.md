# excel

install.packages('tidyverse')
library(tidyverse)

starwars

#excluir colunas
starwars %>%
  select(-films,-vehicles,-starships)

#selecionar colunas 
starwars %>%
  select(name,height,mass)

#selecionar sequencia de colunas 

starwars %>%
  select(name : mass)

#começa com
starwars %>%
  select(starts_with('films'))


#contem um determinado

starwars %>%
  select(contains('color'))

#pegar dentro de uma linha multiplos
starwars %>%
  filter(name == 'C-3PO')

starwars %>%
  filter(sex == 'female', eye_color == 'blue')

#usando OU
starwars %>%
  filter(sex == 'female' | eye_color == 'blue')

#INFORMAÇÃO FALTANDO

starwars %>%
  filter(is.na(homeworld))

#olhos azuis ou verdes

starwars %>%
  filter(eye_color %in% c('blue','brown'))

#inverso da condição usa !

#converter de centimetros p altura
starwars %>%
  mutate(
    height = height/100
  )


#sim ou nao peso acima de 100kg

starwars %>%
  mutate(
    peso_100 = ifelse(mass>100,'S','N')
  ) %>%
  select(name,peso_100)

#troca NA por algo

starwars %>%
  mutate(
    hair_color = ifelse(is.na(hair_color),'desconhecido',hair_color)
  )

#ordenar por ordem crescente ou decrescente
starwars %>%
  arrange(height)

starwars %>%
  arrange(-height) ##ordem decrescente

#ordenar por multiplas colunas

starwars %>%
  arrange(hair_color,height)

#selecionar os 3 mais baixos
starwars %>%
  arrange(height) %>%
   slice_head(n=3)

#selecionar os 3 mais altos
starwars %>%
  filter(!is.na(height)) %>%
  arrange(height) %>%
  slice_tail(n=3)

#selecionar aleatorios
starwars %>%
  slice_sample(n=7)

#agregar todos os dados da tabela

starwars %>%
  summarise(
    personagens = n(),
    altura_media = mean(height, na.rm = T), #tirar os na
    personagem_maisleve = min(mass, na.rm = T),
  )

#agregrar os grupos tipo um excel

starwars %>%
  group_by(eye_color) %>%
  summarise(
    personagens = n()
  )

#qual a media da altura por especie

starwars %>%
  group_by(species) %>%
  summarise(
    altura_media = mean(height, na.rm = T)
  ) %>%
  arrange(desc(altura_media)) #desc decrescente, sem nada crescente 

#quantos personagens cor de cabelo

starwars %>%
  group_by(hair_color) %>%
  summarise(
    personagens = n()
  )  %>%
  arrange(desc(personagens))

#se tem mais robos ou humanos

starwars %>%
  group_by(species) %>%
  summarise(
    personagens = n()
  ) %>%
  filter(species %in% c('Human','Droid'))


library(lubridate)

data <- '2024-10-30'
ymd(data)

data2 <- ymd_hms('2024-10-30 16:49:10')

tempo <- '16:45:30'
hms(tempo)

month(data)

year(data)

#semana do ano
week(data)

#dia da semana
weekdays(data)

hour(data2)
