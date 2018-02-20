---
layout: post
title:  "Reparando bando de dados Syspdv"
date:   2018-02-20
---

ANTES DE TUDO FAÇA UM BACKUP DO BANCO!!!!!!!!!!!!!!!!!!!!!
 
 
primeiro passo> ENTRAR NA PASTA C:\ARQUIVOS DE PROGRAMAS\FIREBIRD\FIREBIRD(VERSAO)\BIN
 
EX.: C:\Program Files (x86)\Firebird\Firebird_2_5\bin OU C:\Program Files\Firebird\Firebird_2_5\bin
 
 
NESSA PASTA VOCÊ IRA COPIAR OS ARQUIVOS
1º GFIX
2º GBAK
3º FBCLIENT.DLL
 
E COLAR NA PASTA DO SYSPDV - C:\SYSPDV
 
segundo passo> RENOMEAR BANCO DE SYSPDV_SRV.FDB PARA 1SYSPDV_SRV.FDB
 
 
ABRA O PROMPT DE COMANDO
NO INICIAR>EXECULTAR> DIGITE CMD E EXECULTE
QUANDO ABRIR A TELA DO PROMPT ENTRE NA PASTA DO SYSPDV
 
VAI ESTAR ASSIM: C:\USERS\NOMEDOUSUARIO>
DIGITE CD.. PARA RETORNAR UM DIRETORIO
FICARÁ ASSIM: C:\USERS>
NOVAMENTE CD..
FICARÁ ASSIM: C:\>
VC DIGITA: CD SYSPDV
FICARÁ ASSIM: C:\SYSPDV>
VOCÊ IRA AGORA INICIAR O PROCESSO DE REPARAÇÃO

{% highlight ruby %}
C:\SYSPDV>set isc_user=sysdba
C:\SYSPDV>set isc_password=masterkey
 
C:\Syspdv>gfix -user sysdba -password masterkey -mo read_only C:\Syspdv\1syspdv_srv.fdb  //marca o banco como somente leitura
 
 
C:\SYSPDV>gfix -v -f 1syspdv_srv.fdb                //verificar se tem erro no banco
C:\SYSPDV>gfix -m -f -i 1syspdv_srv.fdb                    // corrigi erros do banco
C:\SYSPDV>gbak -b -v -g -i -l 1syspdv_srv.fdb srv.fbk                  //backup do banco
C:\SYSPDV>gbak -c -v -i srv.fbk syspdv_srv.fdb                               //restaurar banco
C:\SYSPDV>gbak -c -v -i -n srv.gbk syspdv_srv.fdb    <========> Desconsidera os 'null'
 
 
C:\Syspdv>gfix -user sysdba -password masterkey -mo read_write C:\Syspdv\Syspdv_srv.fdb  //marcar o banco com permissão de "escrita"

{% endhighlight %}

==========================================================================
CASO NÃO DÊ CERTO, USE ESSES COMANDOS
==========================================================================

{% highlight ruby %}
C:\SYSPDV>gbak -b -v -g -i -l -o 1syspdv_srv.fdb srv.fbk
C:\SYSPDV>gbak -c -v -i -o srv.fbk syspdv_srv.fdb

{% endhighlight %}
