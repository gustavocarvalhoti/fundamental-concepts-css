# Conceitos Fundamentais sobre CSS
<img src="natal.png" alt="book" width="300px"/>

## Conceitos fundamentais
### Cascata
Sempre é lido de cima para baixo e direita para a esquerda o CSS (É sério).
````
div { border: 1px solid red  !important; }
div { border: 1px solid blue; } 
!important causa uma vitória automática para a primeira regra da cascata.
````

### Herança
````
Explicando bem diretamente, a herança, em CSS, quer dizer
que alguns valores de propriedade definidos em elementos são herdados por seus descendentes.

p { color : blue;}

<p>
    Lorem ipsum dolor, <em>sit amet consectetur</em> 
    adipisicing elit. Accusantium,
    <strong>atque</strong>!
</p>

Perceba que o parágrafo tem filhos (descendentes diretos),
<em> e <strong>, e que eles, automaticamente,  herdaram a cor azul de seu pai .

#### Propriedades não-herdadas
<p style="border: 1px solid black">
    Parágrafo com <em>texto enfatizado</em>.
</p>

Como border é uma propriedade não-herdada e não há propriedade de borda 
especificada para 'em', então ele obtém o valor inicial de borda none.

#### Controle de herança: 
inherit = "Herdado" - Vem do ancestral   
initial = "Inicial" - Definido pelo navegador, o <em> não será vermelho
<p>
    <span>Texto em vermelho.</span>
    <em>Texto na cor inicial (preto).</em>
    <span>Texto em vermelho de novo.</span>
</p>
unset = Ele serve para restaurar a propriedade com seu “valor natural”:
se a propriedade é herdada naturalmente, ele age como inherit; caso contrário, como initial.

revert = não afetará regras aplicadas a filhos de um elemento que foram resetadas, mas removerá os efeitos de uma regra-pai em um filho.
p {margin:  50px;}
<p style="margin: revert;">Texto do primeiro parágrafo.</p>
<p style="margin: unset;">Texto do segundo parágrafo.</p>

Revert -> Cancelará a margem de 50px e colocará de volta a margem default aplicada pelo navegador.
Unset  -> Simplesmente definirá a margem para o valor inicial (que é 0).

A propriedade all - abaixo mostra como não herdar nada, traz o valor inicial
blockquote {
    background-color : red;
    border :  5px solid green;
    color :  #fff ;
}
.u-total-fix {
    all : unset; 
}
````

### Especificidade - Qualidade daquilo que é específico.
```
p.red { background-color : red;}
Esse é um pedido mais... E specífico! Pesquisa a classe red e os <p> dentro dela.

Classificar Especificidade (Decrescente) ->
a. Estilo inline;
b. ID;
c. Classe, pseudo-classe e atributo;
d. Elemento e pseudo-elemento.
```

## Seletores
### Eficiência: Em ordem decrescente 
1. ID
2. Classe
3. Tipo
4. Irmão Adjacente: Compartilham o mesmo pai e precede imediatamente <br/>
````
h2 +  p  {...}
li :first-of-type +  li {...}
input :checked + .c-custom-check {...}
```` 
5. Descendente Direto <br/>
````
div > a  {...}
#l-hero >  .c-button {...}
.c-card > p {...}
````
6. Descendente <br/>
````
h1 em {...}
.c-widget  a  {...}
#l-comments .c-button {...}
````
7. Universal <br/>
````
* {...}
.u-float + * {...}
*.is-hidden {...}
````
8. Atributo <br/>
````
a [lang] {...}
span [lang="pt"] {...}
a [href$=".io"] {...}
````
9. Pseudo-classe/Pseudo-elemento <br/>
````
a :hover {...}
.c-input--textarea :focus {...}
p ::first-line {...}
````
Os navegadores leem os seletores da direita para a esquerda, isso mesmo <br/>
````
body .wrapper  #content ul li  a  {...} <- Nesse caso ele passou percorreu um monte de lugar até achar o estilo 
.c-list__link {...} <- Esse seria o melhor caminho para melhorar a performance da página, ele vai direto no 'a' e aplica o estilo
````