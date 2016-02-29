# {less}

O LESS uma linguagem dinâminca de esitlo que é baseada em CSS (mesma ideia, sintaxe familiar) que gera CSS no final. **LESS** é um pré-processador, porque, no fim, o browser só entende CSS mesmo. Você escreve um arquivo .less mas usa no final um .css compilado com o comando **lessc**.lessc


## Variáveis

Variáveis servem para definir valores padrões para seus projetos e facilitar a manutenção e alteração dos mesmos elas permitem que você especifique valores amplamente utilizados em apenas um local, possibilitando assim reutilizá-las por toda sua folha de estilos, realizando mudanças globais de maneira tão fácil como alterar apenas uma linha de código.

**less**

```less
@orange: #E85A05;
@green: #008000;

label {
   color: @orange;
}

span {
   color: @green;
}
```

**css**

```css
label {
   color: #E85A05;
}

span {
   color: #008000;
}
```
## Hierarquia em prol da flexibilidade

**less**

```less
.ul-first {
   margin: 0 auto;
   li {
      list-style: none; display: inline-block; background: #000;
      .drop-down {
         display: none;
      }
      &:hover {
         background: #FFF;
         .drop-down {
            display: block;
         }
      }
   }
}
```

**css**

```css
.ul-first {
  margin: 0 auto;
}
.ul-first li {
  list-style: none;
  display: inline-block;
  background: #000;
}
.ul-first li .drop-down {
  display: none;
}
.ul-first li:hover {
  background: #FFF;
}
.ul-first li:hover .drop-down {
  display: block;
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

## Mixins

Com o LESS nos podemos criar funções, que é chamada de **mixins**. Mixins ou Funções podem ou não receberem argumentos **(parâmetros)**. Mixins são bem úteis quando você tem que repetir a mesma coisa várias vezes, como nas propriedades CSS3 que precisam de **prefixos**.

Parece uma classe CSS mas ele recebe uma variável como parâmetro (que pode ter um valor default também).

+ Mixins com parâmetros

**less**

```less
.radius(@raio: 5px) {
  -webkit-border-radius: @raio;
     -moz-border-radius: @raio;
          border-radius: @raio;
}
```

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

+ Mixins sem parâmetros

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

## Using Less

**Necessário Node.js pré instalado**

 + Windowns
  + https://nodejs.org

+ Linux

```
 + curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
   sudo apt-get install -y nodejs

 + curl -sL https://deb.nodesource.com/setup_5.x | sudo -E bash -
   sudo apt-get install -y nodejs
```
