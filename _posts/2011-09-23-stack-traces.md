---
layout: post-alpha
title: "Stack Traces"
author: "Marcos Piazzolla"
published: true
tags:
- stack traces
- erros eclipse 
- aprendizes
---

# Stack Traces #

Muitas vezes quando desenvolvemos um aplicativo existem situa��es onde o inusitado acontece, a aplica��o para e uma
mensagem assustadora de erro acaba surgindo no terminal, a mensagem � t�o grande que logo entramos em desespero n�o 
sabendo por onde come�ar a leitura do "erro", estas mensagens que s�o "assustadoras" s�o conhecidas como Stack Traces e
pra falar a verdade elas n�o s�o t�o assustadoras assim, seu objetivo � apenas dar ao desenvolvedor um feedback do que 
aconteceu na aplica��o mas muitas vezes o tamanho da Stack Trace acaba assustando. As Stack Traces s�o nossas amigas e
aparecem para nos ajudar, vamos deixar de lado o medo e entender de vez o que uma Stack Trace nos mostra.
Mas antes mesmo de come�ar a tratar de Stack Traces e for�ar erros para que as mesmas ocorram, vamos falar de um 
conceito que ser� de grande ajuda para o entendimento do que foi dito acima, vamos falar sobre a pilha de execu��es.
	
# Pilha de Execu��es #

Vamos utilizar um exemplo para esclarecer este conceito de pilha de execu��o, atente a amostra de c�digo abaixo:

    package com.objectos.stacktraces;  
	
    class Stack {
       public static void main(String[] args) {
       metodoA();
       }

       static void metodoA() {
       System.out.println("M�todo A");
       metodoB();
       }

       static void metodoB() {
       System.out.println("M�todo B");
       }
    }

Todo programa java possui a tal "pilha de execu��es", mas afinal de contas o que � "esta pilha de execu��es" ? A Grosso
modo � onde todas as chamadas de m�todos em um programa java est�o, vamos analisar o trecho acima. 
Quando o programa acima for compilado e executado o mesmo ir� realizar uma s�rie de chamadas aos seus respectivos
m�todos, logo o java organiza as chamadas aos m�todos em uma estrutura muito conhecida na �rea de desenvolvimento de
software, a pilha. Assim quando o programa acima for executado todas as chamadas de m�todos ser�o movidas para a pilha e
executadas do topo da pilha at� a base, no caso o m�todo principal de nosso programa acima.

A pilha de execu��o do programa acima ficaria da seguinte forma:
Inicio do programa, no m�todo principal � efetuada a chamada ao m�todoA() logo o mesmo segue ao topo da pilha, seguindo
o fluxo do programa o metodoA() � executado e acaba fazendo uma chamada ao metodoB() que por sua vez assume o topo, o
metodoB() � executado e acaba deixando a pilha, dando passagem ao metodoA() que novamente assume o topo, ap�s a execu��o
do m�todo o fluxo volta ao m�todo principal que tamb�m estava na pilha, lembrando que a pilha armazena todas as chamadas
de m�todos (main() tamb�m � um m�todo). Assim a pilha de execu��es acaba junto com o programa que por sua vez acaba
imprimindo:

    M�todo A
    M�todo B

Agora que sabemos o que � a pilha de execu��es e como as coisas funcionam em um programa Java, podemos dar continuidade
ao que est�vamos discutindo anteriormente. As Stack Traces.

# Como as Stack Traces ocorrem ?

As Stack Traces surgem toda vez que o fluxo de um programa na pilha de execu��es � interrompido por uma exce��o, assim a
mensagem de erro � lan�ada apontando todo o fluxo da pilha de execu��es e os poss�veis pontos onde a exce��o ocorreu. 

Mas como algo assim pode ocorrer?

Isso � bem simples, lembrando que exce��es podem ocorrer por conta de simples erros que cometemos como por exemplo:
tentar dividir um valor por zero, acessar um �ndice inexistente de um vetor ou at� mesmo tentar acessar uma vari�vel de
refer�ncia que n�o aponte para um objeto.

Em situa��es como essas exce��es s�o lan�adas e Stack Traces acabam aparecendo.
Vamos for�ar uma exce��o e nos aprofundar um pouco mais sobre o assunto. Para isso vamos reaproveitar o exemplo acima e
adicionar o bloco respons�vel pela exce��o.

    package com.objectos.stacktraces;

    class Stack {
       public static void main(String[] args) {
       metodoA();
       }

       static void metodoA() {
          System.out.println("M�todo A");
	  metodoB();
       } 

       static void metodoB() {
          int x = 2, y = 0;
	  int z = x / y;
	  System.out.println(z);//Exce��o!!!!!!!!
	  System.out.println("M�todo B");
       }
    }

Compilamos o programa e ent�o veja s� o que acontece:

    M�todo A
    Exception in thread "main" java.lang.ArithmeticException: / by zero
        at com.objectos.stacktraces.Stack.metodoB(Stack.java:24)
        at com.objectos.stacktraces.Stack.metodoA(Stack.java:19)
        at com.objectos.stacktraces.Stack.main(Stack.java:14)
    Java Result: 1
	
Temos o nosso Stack Trace mostrando a pilha de execu��o, vamos analisar com calma o que aconteceu e pensar em uma forma
de tratar este problema.
No topo da pilha temos o ponto onde a exce��o ocorreu, que foi exatamente no metodoB(), como n�o tratamos a exce��o
(falaremos disso mais adiante) ela acabou passando para o pr�ximo elemento da pilha, o metodoA() que fez a chamada ao
metodoB() o causador de nossos problemas, mas o metodoA() assim como seu antecessor na pilha n�o trata a exce��o
deixando isso a crit�rio do m�todo principal, como o m�todo principal n�o possui nenhuma tratativa para a exce��o
teremos um belo Stack Trace na tela quando o programa for executado.

Falamos muito sobre o nosso Stack Trace acima, mas ainda fica a duvida. Como ele poder� nos ajudar?
O Stack Trace pode, n�o, ele vai nos ajudar na trativa de exce��es e erros que ocorrem ao decorrer da aplica��o, como
por exemplo acima, se lermos o Stack Trace podemos perceber que a mensagem de "erro" apareceu na tela por algu�m tentar
realizar uma opera��o matem�tica ilegal, lendo a primeira linha percebemos isso quando encontramos "ArithmeticException:
/by zero" e de quebra percebemos que fora uma divis�o por zero, algo que n�o existe!

Agora ficou f�cil pois encontramos o causador de nossos problemas, o pr�ximo passo � tratar a exce��o para que este erro
jamais aconte�a novamente.
	
# Corrigindo o problema #

Conseguimos for�ar nossa exce��o para que uma Stack Trace ocorresse, mas como evitar que algo assim acabe acontecendo?

Isso � bem simples basta utilizar uma tratativa de exce��es, um bloco try/catch, que � respons�vel em capturar uma ou
mais exce��es e fazer algo sempre que a exce��o ocorrer, em nosso caso vamos mostrar que n�o existe divis�o por ZERO. 
Vamos adicionar um bloco try/catch ao programa acima e analisar o resultado.

    package com.objectos.stacktraces;

    class Stack {
       public static void main(String[] args) {
          metodoA();
       }

       static void metodoA() {
          System.out.println("M�todo A");
             metodoB();
       }

       static void metodoB() {
          try {		
             int x = 2, y = 0;
             int z = x / y;
             System.out.println(z);
	     catch(ArithmeticException ae ) {
	        System.out.println("N�o existe divis�o por Zero!!!!");
             }
                   System.out.println("M�todo B");
              }
       }

Atente para a sa�da:

    M�todo A
    N�o existe divis�o por zero!!!
    M�todo B
	
Agora as coisas parecem bem melhores, temos nossa exce��o tratada, o programa funciona normalmente e uma tratativa de
exce��es com uma mensagem bem elegante sempre que algo de errado acontecer. Tudo isso gra�as aquela mensagem de erro
"medonha" que muitos se apavoram s� de ver, percebemos aqui que o Stack Trace � realmente o nosso amigo e com ele
podemos corrigir falhas em nossas aplica��es pois o mesmo nos indica todo o fluxo do programa atrav�s da pilha de
execu��es e os respectivos pontos onde ocorreram as exce��es, com isso ele deixou de ser apenas uma mensagem de erro e 
se tornou em um grande aliado nosso.

## *Refer�ncias*

SIERRA, Kathy. BATES, Berty. Use a Cabe�a, Segunda edi��o

http://macoli.wordpress.com/2010/02/20/noobs-e-stacktraces/

http://javafree.uol.com.br/topic-882405-FAQ-Stack-Trace.html

*Artigo escrito por Marcos Piazzolla.*		
