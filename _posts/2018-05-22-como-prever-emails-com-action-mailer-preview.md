---
title: "Como visualizar e-mails com ActionMailer::Preview"
excerpt: "Com o ActionMailer::Preview você consegue visualizar como seus e-mails vão ficar após serem enviados."
header:
  teaser: "/assets/images/preview.jpg"
  og_image: "/assets/images/preview.jpg"
  overlay_image: "/assets/images/overlay_rails.jpg"

categories:
  - ruby-on-rails
tags:
  - ruby-on-rails
  - emails
  - test
---

Nós sabemos como é chato ficar testando nossos **e-mails** no ambiente de desenvolvimento. Pensando nisso, foi inserido na versão 4.1 do Rails o **ActionMailer::Preview**, tornando possível a visualização de e-mails sem que eles sejam de fato enviados. Vamos aprender como utilizar essa **ferramenta**?

Primeiramente, vamos gerar um novo mailer em nosso projeto

```
rails generate mailer Welcome
Running via Spring preloader in process 5087
      create  app/mailers/welcome_mailer.rb
      invoke  erb
      create    app/views/welcome_mailer
      invoke  test_unit
      create    test/mailers/welcome_mailer_test.rb
      create    test/mailers/previews/welcome_mailer_preview.rb
```

Veja que ele já criou dois arquivos dentro da pasta test: _test/mailers/welcome_mailer_test.rb_ e _test/mailers/previews/welcome_mailer_preview.rb_. Nesse caso, vamos utilizar o **_test/mailers/previews/welcome_mailer_preview.rb_** para podermos visualizar nossos templates.

Vamos agora criar um método dentro do **WelcomeMailer** que enviará um e-mail de boas vindas para os usuários que se cadastrarem em nosso sistema, supondo que temos um model User com atributo email. Para isso, vamos abrir o arquivo _app/mailers/welcome_mailer.rb_

```ruby
class WelcomeMailer < ApplicationMailer

  def send_welcome_email(user)
    @user = user
    mail({
      to: user.email,
      from: 'eu@mauricioackermann.com.br',
      subject: 'Seja bem-vindo ao sistema Maurício Ackermann'
      })
  end

end
```

Como **WelcomeMailer** está herdando de ApplicationMailer, ele utilizará o layout padrão que é o _mailer_
```ruby
class ApplicationMailer < ActionMailer::Base
  default from: 'from@example.com'
  layout 'mailer'
end
```

_app/layouts/mailer.html.erb_
```erb
<!DOCTYPE html>
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <style>
      /* Email styles need to be inline */
    </style>
  </head>

  <body>
    <%= yield %>
  </body>
</html>
```

Agora vamos criar um template de e-mail. Vamos criar um arquivo chamado __*send_welcome_email.html.erb*__ dentro de _app/views/welcome_mailer_ que será o html do nosso e-mail.

```erb
<p>Olá, <%= @user.name %></p>
<p><strong>Muito obrigado</strong> por se cadastrar em nosso sistema!</p>
```

Com o mailer criado e o template de e-mail pronto, vamos para a parte de testar. Os **previews de e-mails** ficam dentro da pasta _test/mailers/previews_. Vamos abrir o arquivo que foi criado pelo noso generator, **_welome_mailer_preview.html.erb_**.
```ruby
class WelcomeMailerPreview < ActionMailer::Preview

  def send_welcome_email
    WelcomeMailer.send_welcome_email(User.new(name: 'Maurício Ackermann', email: 'eu@mauricioackermann.com.br'))
  end

end
```

Agora pra visualizarmos o e-mail, ligamos iniciamos o servidor e acessamos o **link** _http://localhost:3000/rails/mailers/welcome_mailer/send_welcome_email_

![E-mail preview]({{ "/assets/images/email.png" | absolute_url }})

E ai, como isso pode ajudar vocês em seus **projetos**? Deixe seus comentários nos contando como você utilizou essa ferramenta.
