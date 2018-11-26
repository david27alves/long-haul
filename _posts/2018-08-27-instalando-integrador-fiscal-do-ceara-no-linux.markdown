---
layout: post
title:  "Instalando Integrador Fiscal do Ceará no Linux"
date:   2018-08-27
comments: true
---

O Integrador Fiscal é uma aplicação desenvolvida pela Sefaz do Ceará que tem como finalidade gerenciar as informações que serão processadas pelo MFE (Módulo Fiscal Eletrônico). O MFE é semelhante ao SAT que é usado no estado de São Paulo, porém com algumas diferenças e bem menos estável, quem já trabalhou com ele sabe do que estou falando. 
Atualmente ele pode ser instalado tanto no Windows quanto no Linux, a versão que usamos para testes foi o Ubuntu 16.04 32 bits, pode ser instalado no 64 bits também, instalando os devidos pacotes para a arquitetura.
Os comandos devem ser executados na ordem como está descrito aqui, caso contrário corre o risco de não funcionar.

## Comando ldd
{% highlight ruby %}
$ ldd --version
{% endhighlight %}

Primeiro passo é executar o comando acima, ele serve para listar a versão do ldd, caso seja menor que 2.12 ele não irá funcionar.

## Instalação do Mono
{% highlight ruby %}
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
echo "deb http://download.mono-project.com/repo/ubuntu xenial main" | sudo tee /etc/apt/sources.list.d/mono-official.list
sudo apt update
apt list --upgradable
sudo apt-get update
sudo apt-get install mono-complete uuid-runtime axel
{% endhighlight %}

{% if page.comments %} {% endif %}
