## Anotações de conclusão

### Flex Container

1. começando, sempre abilitar o 'display: flex;' no inicio do CSS do pai dos elementos - o container. 

2. o padrão do flex é ROW, portanto, abilitando o ponto 1, fará com que os filhos do container se organizem horizontalmente.

3. justify-content

 os itens ficarão todos juntos, lado a lado, da esquerda para a direita. sobrando um espaço vazio no lado direto, é possivel usar o 'justify-content: space-between;'
 
 - o espaço vazio se distribui entre os elementos filhos, onde o primeiro item está colado no lado esquerdo e o ultimo colado no direito. 
 
 também é possível utilizar o 'justify-content: space-around;'
 
 - o espaço vaziu se distribui em volta dos elementos filhos, com uma quantidade idêntica de "vazio" a cada lado dos itens.
 
 ainda tem uma maior variedade dos valores que a propriedade 'justify-content' pode receber, como por exemplo, o 'center', que alinha os itens deixando seu comprimento total exatamente centralizado.

4. align-items

 com os itens distribuidos lado a lado, o padrão é o alinhamento pela linha de cima. para alinhá-los exatamente pelo eixo central, podemos usar 'alig-items: center;'. outros valores para essa propriedade são 'flex-end', pela linha de baixo, 'stretch' e 'baseline', que alinha o texto dentro dos itens

5. flex-direction

 usando o 'flex-direction: column', mudamos a orientação dos eixos horizontais para verticais. agora, os itens estarão um em cima do outro. 
 
 - o 'align-items: center' agora, não alinha pelo meio da altura do item mas pela largura, ou seja, usando o eixo do meio vertical.
 
 - para usar o 'justify-content: space-around', é necessário que aumentemos o 'height' do flex container, já que os espaços vazios estão aos lados dos itenw, e não é possível distribuir estes para cima e para baixo.


    lembrando que, quando flex-direction é uma COLUMN, 'justify-content' alinha verticalmente, enquanto 'align-items' alinha horizontalmente na tela. 

6. align-content

possui quase os mesmos valores que 'align-items', mas a diferença é que ele alinha os elementos como um grande pacote, considerando que eles tenham mais do que uma column(sendo rows) ou mais rows (sendo column). eles juntam o conteúdo, sem alterar o tamanho, no início da tela, no fim, no centro, também usam o 'space-between' e 'space-around'.

7. flex-flow

é um shorthand para o 'flex-direction' e o 'flex-wrap', respectivamente. o seu padrão é 'row nowrap'.

    .container {
        flex-flow: column wrap;
    }

### Flex items

1. flex-order

 'flex-order' é uma propriedade usada diretamente nos filhos do flex-container para alterar a posição do item em si na fileira ~ ou coluna do flex. 

2. flex-grow

 o 'flex-grow' sempre recebe valor numérico (1, 2, 3..), e distruibui os espaços "livres" de acordo com essa numeração. usando a classe em comum de todos os itens, e alterando para 'flex-grow: 1;', todos os itens crescem equivalente a mesma quantidade de "vazio" do restante do elemento container.
 
    .flexItem {
        flex-grow: 1;
        }
        
- o cálculo usado pelo navegador, é o seguinte: o espaço vazio é dividido pela quantidade de itens usando 'flex-grow'. como a classe usada se referia a 4 itens no HTML, o espaço será dividido em 4 pedaços e distribuidos um para cada item. assim, cada item cresce em tamanho respectivamente 1/4 do espaço vazio que existia na tela.

- se decidirmos usar uma classe diferente de um item específico, podemos dar uma quantidade maior de espaços vazios à ela:

    .primeiro {
        flex-grow: 2;
    }

o que aconteceu? o navegador dividiu o espaço vazio em 5 pedaços ~ pois o primeiro elemento possui 'flex-grow: 2;', e o segundo, terceiro e quarto item possui 'flex-grow: 1;'. portanto, o item 2 crescerá um total de 2/5 do espaço vazio, mais do que os outros itens, que crescerão apenas 1/5 cada. 

- o 'flex-grow: 0;' é o padrão. eles permanecerão do mesmo tamanho definido anteriormente.

3. flex-shrink

 considerando que cada um dos itens tenham 50px de largura, numa tela de 200px, cada um dos itens ficarão em seu tamanho original, um do lado do outro certinho. mas, caso a tela seja ainda menor, como podemos definir quais elementos diminuirão primeiro - ou mais do que os outros? 
 
 para ocupar uma tela de 100px, cada um deles diminuiu exatamente a metade, igualmente. todos eles ficaram com 25px de largura. 

    .flexItem {
        flex-shrink: 1;
    }
    
o padrão do 'flex-shrink' é 1. ou seja, todos eles diminuiem igualmente. para um elemento diminuir mais do que o outro, é necessário novamente usar a classe mais específica do elemento: 

    .primeiro {
        flex-shrink: 2;
    }

o primeiro elemento vai diminuir 2x mais do que os outros. na tela de 100px, o primeiro elemento ficará com 10px, enquanto os outros terão 30px.

- a tela foi dividida pela metade, ou seja, perdeu 100px. o navegador vai contar a quantidade de itens utilizando o 'flex-shrink'. o primeiro elemento possui 2, enquanto os outros três possuem 1, totalizando 5 'flex-grow's. dividindo 100 (a quantidade de pixels perdida) por 5 (quantidade de 'flex-grow'), calcula 5 pedaços de 20px cada. 

o primeiro item, que possui 'flex-shrink: 2;', diminui 2x os 20px. ele diminui 40px. os outros, diminuem apenas 20px, ou seja, possuem 30px após a diminuição da tela.

- o 'flex-shrink: 0;' não aceita diminuição. os elementos possuem a mesma quantidade de pixels, e o que acontece é que o navegador aplica uma espécie de 'zoom-out' dos elementos. para tirar o zoom, é só apertar 'control + 0', mas nesse caso, os elementos vazarão da tela e será necessário utilizar o scroll para continuar vizualizando. 
    não é muito recomendado usar.

4. flex-basis

o 'flex-basis' define a largura padrão do elemento antes dos espaços vazios serem distribuidos. pode ser % ou em px, ou 'auto'. é basicamente um 'width'.

 se definido como 0, o espaço vazio não é fatorado. caso definido como auto, o espaço extra é distruibuido com base no valor do 'flex-grow'

5. flex

onde o primeiro elemento após os ':' são, respectivamente, 'flex-grow', 'flex-shrink' e 'flex-basis'.

    .flexItem {
        flex: 1 1 25%;
    }
