# Not-A-Blog

Blog para começar no mundo de ricing em distribuições Linux.

## Como funciona?

Utilizo o [Jekyll](http://jekyllrb.com/), um static generator em Ruby, para criar esse blog.

## Primeiros passos

1. Instale o [Git](http://git-scm.com/downloads) e o [Ruby](http://www.ruby-lang.org/pt/downloads/), caso você não os tenha ainda.

2. Uma vez tendo instalado essas dependências, abra o terminal e instale o [Jekyll](http://jekyllrb.com/) através do comando:

```sh
gem install jekyll
```

3. Agora clone o projeto:

```sh
git clone git@github.com:ricebr/Not-A-Blog.git
```
4. Depois vá para pasta do projeto:

```sh
cd Not-A-Blog
```

5. E finalmente rode:

```sh
jekyll serve
```

Agora você irá ver o site rodando em `localhost:4000` :D

## Estrutura

A estrutura básica do projeto se dá na seguinte forma:

<pre>
.
|-- _includes
|-- _layouts
|-- _site
|-- assets
|-- _config.yml
`-- index.html
</pre>

### [_includes](https://github.com/ricebr/Not-A-Blog/tree/gh-pages/_includes)

São blocos de código utilizados para gerar a página principal do site ([index.html](https://github.com/ricebr/Not-A-Blog/blob/gh-pages/index.html)).

### [_layouts](https://github.com/ricebr/Not-A-Blog/tree/gh-pages/_layouts)

Contém o template padrão da aplicação.

### _site

É onde os arquivos gerados são armazenados, uma vez que o Jekyll tenha sido rodado. Porém, esse diretório se torna desnecessário no nosso modelo, por isso está ignorado ([.gitignore](https://github.com/ricebr/Not-A-Blog/blob/gh-pages/.gitignore)).

### [_config.yml](https://github.com/ricebr/Not-A-Blog/blob/gh-pages/_config.yml)

Armazena de forma fácil a maior parte das configurações da aplicação.

### [index.html](https://github.com/ricebr/Not-A-Blog/blob/gh-pages/index.html)

É o arquivo que importa todas as seções da aplicação.

*Mais informações sobre a estrutura de arquivos do Jekyll, [clique aqui](https://github.com/jekyll/jekyll/wiki/How-Jekyll-works).*
