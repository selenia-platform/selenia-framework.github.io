# Selenia Website

> Nota: Este repositório contém os ficheiros source do website da framework Selenia e necessita de Sculpin para funcionar.

> O Sculpin é o static site generator escrito em PHP. Converte Markdown, Twig templates ou standard HTML num site estático de HTML.

## Instalação

### Instalação do Sculpin

A melhor forma de instalar o Sculpin é fazer o download do PHAR.

Na linha de comandos:

```shell
curl -O https://download.sculpin.io/sculpin.phar
chmod +x sculpin.phar
```

Poderá ser útil correr o Sculpin de qualquer directoria. Assim sendo, deverá move-lo para a sua directoria bin.

```shell
mv sculpin.phar ~/bin/sculpin
```

Neste ponto já deverá ser capaz de executar o Sculpin de qualquer directoria, escrevendo `sculpin` na linha de comandos. Se não conseguir, o mais provável é que não tenha a directoria `bin` assignada à variável `PATH` da shell. Para resolver:

```shell
PATH=$PATH:$HOME/bin
```

## Correr o Sculpin

Depois de instalado, já poderá gerar ficheiros estáticos, ligar um "watcher" e correr um local web server:

```shell
sculpin generate --watch --server
```

Verifique o endereço `http://localhost:8000/`

Mais informações sobre Sculpin:

[Documentação de Sculpin](https://sculpin.io/getstarted/)

## Adicionar conteúdo

Na directoria `source/documentation` encontram-se os ficheiros de markdown que serão mostrados na secção "Documentation". Os ficheiros markdown deverão ter o seguinte header:

```shell
---
title: Content types
slug: content-types
layout: itemdoc
use: [docs]
---
```

O `title` e o `slug` deverão corresponder à referência no ficheiro `sculpin_site.yml` em `app/config`:

```shell
name: Content Types
url: documentation/content-types/
slug: content-types
id: contenttypes
```


Também existem ficheiros de markdown na raiz do projecto que correspondem ás outras secções do website. Todos eles contém um header que faz referência ao template usado e pode-se adicionar conteúdo usando esses mesmos ficheiros de markdown.


```shell
---
layout: texto
title: About
---

#Página About
```

O markdown inserido nestes ficheiros corresponde a uma parte do conteúdo, já que a outra parte está em HTML. Por exemplo, o header e o footer desses ficheiros estão sempre no template e em alguns casos o ficheiro de markdown só existe para dar existência ao respectivo ficheiro de HTML, como acontece com o `index.md`.

Contudo o conteúdo pode ser adicionado nos ficheiros:

*   `documentation.md` --> Página principal da documentação
*   `about.md`
*   `download.md`
*   `readme.md`
*   `404.md`

## Adicionar documentação com scrollspy

Poderão existir ficheiros de markdown bastante extensos, para isso foi criado um submenu auxiliar para navegar entre ancoras e com scrollspy. Para este menu auxiliar existir, é preciso conter no topo, por baixo do header de sculpin o seguinte:


```html
---
layout: itemdoc
title: Documentation
use: [docs]
---

  <div id="navbar-scrollselenia">
    <ul class="nav nav-tabs" role="tablist">
      <li class="title">SubMenu</li>
      <li><a href="#overview">Overview</a></li>
      <li><a href="#html">HTML</a></li>
      <li><a href="#list">List</a></li>
      <li><a href="#code">Code</a></li>
    </ul>
  </div>

```

Além da navegação, será necessário adicionar as ancoras no markdown.
Para isso usamos o próprio markdown, tendo em conta que o ID será o titulo mas em minúsculas.

```shell
##Overview
```

Será renderizado em html da seguinte forma:

```html
<h2 id="overview">Overview</h2>
```

Se o titulo contiver várias palavras, as mesmas serão separadas por `-`:

```shell
##Overview from space
```
Será renderizado em html da seguinte forma:

```html
<h2 id="overview-from-space">Overview from space</h2>
```

> Nota: O scrollspy só funcionará no âmbito do template `docs.twig.html` ou seja, na documentação.

**Selenia framework** - Copyright &copy; 2015 Impactwave, Lda.
