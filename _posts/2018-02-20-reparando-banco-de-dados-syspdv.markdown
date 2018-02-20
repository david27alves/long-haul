---
layout: post
title:  "Reparando banco de dados Syspdv"
date:   2018-02-20
---

Bom dia leitores, últimamente estou tentando escrever para o blog, já que criei ele e sempre tive preguiça de escrever. :p <br>
Atualmente trabalho em uma assistência que dá suporte no Syspdv, um sistema de automação comercial desenvolvido pela [Casa Magalhães](https://www.casamagalhaes.com.br/), e como forma de documentação dos problemas que encontro no dia, resolvi escrever aqui no blog, pois serve pra mim fazer consultas futuras e pra outras pessoas que enfrentem o mesmo problema.

Atenção: antes de realizar todo esse processo faça um backup do banco de dados!
 
 
O primeiro passo é entrar no diretório bin do Firebird
{% highlight ruby %}
C:\Program Files\Firebird\Firebird_2_5\bin
{% endhighlight %}
 
Ex.: C:\Program Files (x86)\Firebird\Firebird_2_5\bin OU C:\Program Files\Firebird\Firebird_2_5\bin

Nesta pasta você irá copiar os arquivos `gfix.exe`, `gbak.exe`, `fbclient.dll` e colar na pasta do Syspdv `C:\Syspdv`
 
O segundo passo é renomear o banco de dados de syspdv_srv.fdb para 1syspdv_srv.fdb 

Abra o prompt de comando, clique no menu iniciar, digite cmd e execute. Quando abrir a tela do prompt navegue até a pasta do Syspdv.

O prompt de comando irá iniciar no diretório "C:\Users\Usuario".
O comando cd serve para voltar um nível na árvore de diretórios, digite cd .. e o prompt irá para o diretório "C:\Users", digite cd .. novamente e valtará para a raiz, agora navegue até a pasta do Syspdv digitando o comando cd Syspdv. Agora iremos iniciar o processo de reparação do banco.

Digite os seguintes comando no prompt.

{% highlight ruby %}
C:\Syspdv>set isc_user=sysdba
C:\Syspdv>set isc_password=masterkey
 
C:\Syspdv>gfix -user sysdba -password masterkey -mo read_only C:\Syspdv\1syspdv_srv.fdb  //marca o banco como somente leitura
 
 
C:\Syspdv>gfix -v -f 1syspdv_srv.fdb                   // verificar se tem erro no banco
C:\Syspdv>gfix -m -f -i 1syspdv_srv.fdb                // corrigi erros do banco
C:\Syspdv>gbak -b -v -g -i -l 1syspdv_srv.fdb srv.fbk  // backup do banco
C:\Syspdv>gbak -c -v -i srv.fbk syspdv_srv.fdb         // restaurar banco
C:\Syspdv>gbak -c -v -i -n srv.gbk syspdv_srv.fdb      // desconsidera os 'null'
 
 
C:\Syspdv>gfix -user sysdba -password masterkey -mo read_write C:\Syspdv\Syspdv_srv.fdb  //marcar o banco com permissão de "escrita"

{% endhighlight %}

Caso não dê certo, use os seguintes comandos

{% highlight ruby %}
C:\SYSPDV>gbak -b -v -g -i -l -o 1syspdv_srv.fdb srv.fbk
C:\SYSPDV>gbak -c -v -i -o srv.fbk syspdv_srv.fdb

{% endhighlight %}
