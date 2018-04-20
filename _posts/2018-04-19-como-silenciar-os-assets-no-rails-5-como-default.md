---
title: "Silenciando os logs de assets no Rails 5 por padrão"
excerpt: "Aprenda como configurar os logs de assets no ambiente de desenvolvimento a partir do Rails 5."
categories:
  - javascript
tags:
  - ruby-on-rails
  - web
  - rails-5
---

Quem programa rails há algum tempo já deve ter se deparado com esses logs no terminal enquanto o servidor está ligado no ambiente de desenvolvimento.
```
Started GET "/assets/projeto-647fc4d3536f3802f102686cfc41681d6ad8dd0037939f999167d80cc42d3d8e.png" for 127.0.0.1 at 2018-04-19 14:39:08 -0300
Started GET "/assets/font-awesome/fontawesome-weont-3c4a1bb7ce3234407184f0d80cc4dec075e4ad616b44dcc5778e1cfb1bc24019.woff2" for 127.0.0.1 at 2018-04-19 14:39:08 -0300
"/assets/projeto20e3234407184f0d80cc4dec075e4ad616b44dcc5778e1cfb1bc24019.png" for 127.0.0.1 at 2018-04-19 14:39:08 -0300
```
Para acabar com isso, a gem `quiet_assets` foi criada, deixando nossos logs muito mais limpos para podermos debugar o que realmente é importante em nossas aplicações.

### Quiet Assets no Rails 5

A partir do Rails 5, a gem foi incorporada no core do Rails, facilitando muito mais as nossas vidas e nos deixando menos dependente de mais uma gem.

Agora existe uma nova configuração que podemos mexer em nosso `development.rb`, chamada `config.assets.quiet`.

Essa configuração, se definida como `true`, carrega um rack middleware [Sprockets::Rails::QuietAssets](https://github.com/rails/sprockets-rails/pull/355){:target="blank"}, incluso no `sprockets-rails 3.1`, que verifica se a chamada tem um prefixo de `asset` e silencia ao encontrar.

Por padrão, `config.assets.quiet` tem o valor `true`, portanto, não devemos nos preocupar. Se por algum motivo necessitarmos ver os logs de assets, basta alterar o valor para `false`.
