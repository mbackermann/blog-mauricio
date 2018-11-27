---
title: "Possíveis novidades do Ruby 2.6"
excerpt: "Quais são os destaques da nova versão do Ruby 2.6 que deve ser lançado agora no final do ano"
header:
  teaser: "/assets/images/ruby-2-6.jpg"
  og_image: "/assets/images/ruby-2-6.jpg"
  overlay_image: "/assets/images/overlay_ruby.jpg"

  categories:
    - ruby
  tags:
    - ruby
    - ruby-2-6
---

Acompanhando os últimos anos, podemos observar que as novas versões do Ruby são lançadas anualmente próximas ao natal.

Tendo isso em vista, levantamos algumas das principais *features* novas que devem aparecer no patch do final do ano.

## MJIT: O compilador JIT (Just in Time) do Ruby

Como sabemos, o Ruby é uma linguagem interpretada, ou seja, o código é executado em tempo de execução através dos interpretadores carregados em memória. Já o C, por exemplo, é uma linguagem compilada. Ou seja, antes de executarmos o código, precisamos compilá-lo, transformando-o em código de máquina, para que os computadores possam executá-lo. As linguagens compiladas tendem a ter uma performance superior a linguagens interpretadas, como o Ruby, PHP e o Python.

Recentemente na RubyKaigi (conferência de ruby japonesa) foi proposto o desenvolvimento de um JIT para a Ruby VM. A ideia é que o compilador JIT inspecione o código em tempo de execução e otimize-o de maneira inteligente, diferentemente do compilador Ahead of Time.

Em suma, a idéia é utilizar compiladores C já presentes nas máquinas (gcc ou clang) como compilador e transformar o bytecode em C e depois, compilá-lo.

Alguns testes indicaram que em alguns casos, o MJIT consegue ser até 4x mais rápido que a implementação original.

O Heroku fez um post bem explicativo sobre o funcionamento (em inglês) que pode ser acessado <a href="https://blog.heroku.com/ruby-mjit" target="_blank_">aqui.</a>

### Array#union e Array#difference

Um jeito mais simples de achar a união e a diferença entre Arrays

```ruby
[4,5,6,6,7,9].difference([4,5,7]) #=> [ 6,6,9 ]
["a", "b", "c"].union(["c", "d", "a"])          #=> [ "a", "b", "c", "d" ]
["a"].union([["e", "b"], ["a", "c", "b"]])      #=> [ "a", "e", "b", "c" ]
```

### Endless ranges

Será introduzido o (0..) range, o que tornará possível:

```ruby
ary[1..]                            # idêntico ao ary[1..-1]
(1..).each {|index| ... }           # loop inifinito iniciando em index 1
ary.zip(1..) {|elem, index| ... }   # ary.each.with_index(1) { }
```

### Enumerable#to_h agora aceita um bloco de código que mapeia chave para valores

A partir do Ruby 2.6 será possível fazer:

```ruby
(1..5).to_h { |x| [x, x ** 2] } #=> {1=>1, 2=>4, 3=>9, 4=>16, 5=>25}
```

Dessa maneira, eliminamos o array temporário que era comumente utilizado nos seguintes casos, por exemplo

```ruby
(1..5).map { |x| [x, x ** 2] }.to_h  #=> {1=>1, 2=>4, 3=>9, 4=>16, 5=>25}
(1..5).each_with_object({}) { |x, h| h[x] = x ** 2 } #=> {1=>1, 2=>4, 3=>9, 4=>16, 5=>25}
```

### Array#filter como alternativa ao Array#select

Seguindo outras linguagens como o Javascript, agora poderemos utilizar o filter em nossos Arrays

```ruby
[:foo, :bar].filter { |x| x == :foo } # => [:foo]
```

### Hash#merge agora aceita múltiplos argumentos, evitando chamadas após chamadas

Não precisaremos utilizar o merge diversas vezes quando formos combinar diversos hashes. Basta passarmos todos os hashes que desejarmos como parâmetros

```ruby
hash1.merge(hash2, hash3, hash4)
```

### Random.bytes

Agora bytes é um método estático da classe Random, podendo ser evocado diretamente

```ruby
Random.bytes(5) # => "\xC4\x14{\xBC\x94"
```

O que vocês acham dessas novidades do Ruby 2.6 que deve chegar no final do mês de dezembro? São bem-vindas? Como vocês imaginam utilizar essas novas novidades em seus projetos? Deixe seus comentários e não esqueça de me acompanhar nas redes sociais. Um abraço e até o próximo post!
