---
title: "Date#prev_ocurring e Date#next_ocurring - Como achar o último e o próximo dia específico da semana"
excerpt: "No Rails 5.2, foram adicionados dois novos métodos no modulo DateAndTime: next_occurring e prev_occurring"
categories:
  - ruby-on-rails
tags:
  - ruby-on-rails
  - web
  - rails-5-2
---
No rails 5.2 foram adicionados dois novos métodos no modulo DateAndTime: next_occurring e prev_occurring.
Com esses novos métodos, nós conseguimos localizar um dia da semana anterior e do futuro.

Antes desses novos métodos, se nós quisessemos achar a última segunda-feira e a próxima terça-feira baseando-se no dia de hoje, faríamos:
```ruby
hoje = Date.today
# Fri, 20 Apr 2018
ultima_segunda = hoje.yesterday.beginning_of_week(:monday)
# Mon, 16 Apr 2018
proxima_terca = hoje.tomorrow.end_of_week(:wednesday)
# Tue, 24 Apr 2018
```
Isso parecia uma enorme gambiarra e era bem feio, tinha que fazer cálculos.

Agora com o Rails 5.2 podemos fazer da seguinte maneira:

```ruby
hoje = Date.today
# Fri, 20 Apr 2018
ultima_segunda = hoje.prev_occurring(:monday)
# Mon, 16 Apr 2018
proxima_terca = hoje.next_occurring(:tuesday)
# Tue, 24 Apr 2018
```

 Muito melhor, não é mesmo?

 O que vocês acharam desses novos métodos? Vão ajudar em seus projetos? Deixe seu comentário.
