# LESS

O LESS uma linguagem dinâminca de esitlo que é baseada em CSS (mesma ideia, sintaxe familiar) que gera CSS no final. **LESS** é um pré-processador, porque, no fim, o browser só entende CSS mesmo. Você escreve um arquivo .less mas usa no final um .css compilado com o comando **lessc**.


## Variáveis

Variáveis servem para definir valores padrões para seus projetos e facilitar a manutenção e alteração dos mesmos elas permitem que você especifique valores amplamente utilizados em apenas um local, possibilitando assim reutilizá-las por toda sua folha de estilos, realizando mudanças globais de maneira tão fácil como alterar apenas uma linha de código.

**less**

```less
@black: #000;
@red: #F00;

.n1v {
   color: @black;
}
.nv2 {
   color: @red;
}
```

**css**

```css
.n1v {
   color: #000;
}
.nv2 {
   color: #F00;
}
```

## Mixins

Com o LESS nos podemos criar funções, que é chamada de **mixins**. Mixins ou Funções podem ou não receberem argumentos **(parâmetros)**. Mixins são bem úteis quando você tem que repetir a mesma coisa várias vezes, como nas propriedades CSS3 que precisam de **prefixos**.

+ Funções com parâmetros

**less**

```less
.radius(@raio: 5px) {
  -webkit-border-radius: @raio;
     -moz-border-radius: @raio;
          border-radius: @raio;
}
```

Parece uma classe CSS mas ele recebe uma variável como parâmetro (que pode ter um valor default também).

```less
.container {
   .radius;
}

.coluna {
   width: 345px;
   .radius(10px);
}
```

**css**

```css
.container {
   -webkit-border-radius:5px;
      -moz-border-radius:5px;
           border-radius:5px;
}

.coluna {
   width: 345px;
   -webkit-border-radius:10px;
      -moz-border-radius:10px;
           border-radius:10px;
}
```

+ Funções sem parâmetros

**less**

```less
.float-l() {
   float: left;
}

.float-r() {
   float: right;
}

.container {
   .float-l;
}

.coluna {
   .float-r;
}
```

**css**

```css
.container {
   float: left;
}

.coluna {
   float: right;
}
```

## Contas matemáticas

Sabe quando você tem aquele elemento principal com **960px** mas que precisa de um padding de **35px** e duas colunas lá dentro de tamanhos iguais mas deixando **20px** entre elas? Qual o tamanho de cada coluna mesmo? **435px**. Aí você coloca no CSS:

**css**

```css
.container {
   padding: 35px;
   width: 960px;
}
.coluna {
   width: 435px;
}
```

E quando alguém mudar o tamanho do padding, você torce pra lembrarem de refazer a conta da coluna – que, aliás, seria (960px – 35px * 2 – 20px) / 2 = 435px. No LESS, você pode fazer a conta direito na propriedade e o resultado final é calculado:

**less**

```less
.coluna {
   width: (960px - 35px * 2 - 20px) / 2;
}
```

Melhor ainda, junte com as variáveis que vimos antes e você nem copia e cola valores!

**less**

```less
@total: 960px;
@respiro: 35px;
@espaco: 20px;
 
.container {
   padding: @respiro;
   width: @total;
}
.coluna {
   width: (@total - @respiro * 2 - @espaco) / 2;
}
```