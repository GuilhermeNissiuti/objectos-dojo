---
layout: post
title: "Eclipse :: Instalação"
author: "Hellen Carla Paixão Escarate"
user: "hescarate"
date: "2011-07-11"
published: true
partof: eclipse
num: 0
---

##Instalação 

O Eclipse faz parte do KDO. Ele já deve estar instalado em sua máquina abra um terminal e verifique
se o Eclipse está corretamente instalado.

    $ ls -l /opt/kdo/
    total 8
    drwxr-xr-x 9 root root 4096 Mai 15 13:10 eclipse
    drwxr-xr-x 8 root root 4096 Set  7  2010 iReport-3.7.4

Obs: Não esqueça de digitar a última `/` após "kdo" `ls -l /opt/kdo/`, caso contrário aparecerá 
como está abaixo: 

    $ ls -l /opt/kdo
    lrwxrwxrwx 1 root root 14 Jun 27 19:35 /opt/kdo -> /opt/kdo-1.4.0
     
Como visto, o eclipse já está instalado.

##Lançador GNOME

Você baixou o eclipse e descompactou, agora vamos fazer um lançador para que você possa sempre 
acessar o Eclipse mais rapidamente sem precisar ficar procurando. Para facilitar a inicialização
do Eclipse, a criação de um lançador Gnome será feito. 

Em uma área vazia do seu Desktop, clique com o botão direito do mouse. O menu abaixo vai aparecer: 

![lancador_gnome] (http://i1245.photobucket.com/albums/gg582/img_repo/lancador_gnome-1.jpg)  

No nome coloque Eclipse, e no comando clique em "Navegar". Abrirá uma janela, onde você deve selecionar o
arquivo Eclipse que está do diretório `/home/seulogin/kdo/eclipse/`.

![criar_lancador] (http://i1245.photobucket.com/albums/gg582/img_repo/Captura_de_tela-Criar_lanador.png)  

Para mudar o ícone, basta clicar nele e procurá-lo no endereço `/home/seulogin/kdo/eclipse/icon.xpm`
Criado o lançador, você pode também criar um link para deixar no painel. Para isso, clique com o
direito do mouse no ícone e selecione "Criar link". Arraste esse link até o painel onde está os
outros ícones, de preferência deixe num lugar que esteja vago e solte.

Pronto, agora você tem como acessar o ícone pelo desktop e pelo painel. 

##Iniciando o Eclipse, Área de trabalho

Quando você inicializa o Eclipse, ele pede o caminho onde você quer armazenar seus projetos. Por isso
que criamos dentro de /kdo um diretório chamado projetos, para que todos os projetos que iremos
implementar, sejam guardados nesse diretório. Por isso, o padrão deve ser `/home/seulogin/kdo/projetos/`.

Segue o exemplo abaixo:  

![init_eclipse] (http://i1245.photobucket.com/albums/gg582/img_repo/workspace.png)

No caso da figura acima ele pergunta se eu quero usar o endereço como padrão e não perguntar novamente.
Para que você não tenha o trabalho de dar ok nessa tela toda vez que abrir o Eclipse, deixe essa 
opção habilitada e clique em ok. 

##Padronização

Como já mencionado, a idéia do [KDO](http://rio.objectos.com.br/twiki/bin/view/Objectos/ObjectosKDO) 
é a padronização. Assim, as preferências do Eclipse, em especial as de formatação de arquivos, também
devem ser padronizadas.

Faça o download dos arquivos listados abaixo: 

[objectos-clean-up.xml] ({{site.baseurl}}/caixa/eclipse/objectos-clean-up.xml)

[objectos-codetemplates.xml] ({{site.baseurl}}/caixa/eclipse/objectos-codetemplates.xml)

[objectos-formatter.xml] ({{site.baseurl}}/caixa/eclipse/objectos-formatter.xml)

[objectos-import.importorder] ({{site.baseurl}}/caixa/eclipse/objectos-import.importorder)

[objectos-java-script-formatter.xml] ({{site.baseurl}}/caixa/eclipse/objectos-javascript-formatter.xml)

(caso encontre dificuldade em baixar esses arquivos, clique com o botão direito no link, e escolha a
opção **Salvar link como**).

No Eclipse, clique em **Window** > **Preferences**. Selecione as opções: **Java** > **Code Style** >
**Clean Up**, conforme a figura abaixo: 

![clean_up] (http://i1245.photobucket.com/albums/gg582/img_repo/pref-2.png)

Clique no botão Import e busque o arquivo `objectos-clean-up.xml`, clique em `Apply` e depois
em `Ok`.  

Agora, faça o mesmo para as opções que seguem abaixo de `Clean Up`: 

+ Code Templates
+ Formatter
+ Organize Imports

Ainda em **Window** > **Preferences**, na opção **Java**, escolha agora **Editor** > **Save Actions**, e
verifique também se todas as opções do Save Actions estão habilitadas, conforme a figura abaixo. 

![save_actions] (http://i1245.photobucket.com/albums/gg582/img_repo/Save_action.jpg)

Pronto, suas preferências, inclusive as de formatação de arquivos, devem estar padronizadas. 

###Personalização de Autoria

Se você ainda não sabe o que é, pesquise sobre [Accountability](http://pt.wikipedia.org/wiki/Accountability).
Por isto, é necessário configurar a autoria dos arquivos Java.

Esse procedimento faz com que cada classe nova que você criar, apareça sua identificação.

Vá para **Window->Preferences**, 

![autoria] (http://i1245.photobucket.com/albums/gg582/img_repo/personalizacaodeautoria.png)

Em **Java** > **Code Style** > **Code Templates** edite o comentário padrão de **Comments** > 
**Types**, clicando no botão Edit. No caso, abrirá uma nova janela com o seguinte conteúdo padrão:

    /**
     * @author marcio.endo@objectos.com.br (Marcio Endo)
    */

Você deverá editar esse comentario substituindo pelo seu email da Objectos e seu nome do lado.

![autoria_2] (http://i1245.photobucket.com/albums/gg582/img_repo/personalizacaodeautoria2.png)

Clique em Ok nessa janela, retornará na janela de Code Templates, clique em `Apply` e `OK`. 

##Assistente de imports estáticos 

Uma das novidades trazidas pelo Java 5 foi a possibilidade de realizar imports estáticos. No Eclipse é possível configurar o assistente para lembrar os seus imports estáticos favoritos.

Vá para **Window > Preferences**,

Na caixa de busca procure pela palavra favorites. Selecione a opção **Java > Editor > Content Assist> Favorites**.

Adicione todas classes listadas na figura.

![preferences_imports](http://i1245.photobucket.com/albums/gg582/img_repo/assistentedeimportsestaticos.png)