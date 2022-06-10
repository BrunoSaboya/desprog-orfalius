Shell Sort
======

Introdução
---

Na aula de hoje irmos ver o Algoritmo de ordenação chamado Shell Sort que se baseia no algoritmo já visto em
aula previamente e iremos retomar o Insertion Sort para garantir um melhor entendimento do algoritmo de hoje.

Retomando o Insertion Sort
---

Como já vimos antes o funcionamento do Insertion Sort neste handout iremos apenas rever os
conceitos mais importantes e algumas atividades relacionadas ao algoritmo. Para isso a seguir
segue uma ilustração de como funciona o Insertion Sort


:insertion


Ele consiste em um algoritmo cuja complexidade é ***O(n²)*** e, a acada iteração o maior
elemento do vetor está na sua posição correta, dessa forma levando os menores elementos mais
perto de sua posição. Assim como uma analogia a "parte ordenada" e "resto" (parte desordenada).

??? Checkpoint

Considere o vetor abaixo e ordene o vetor utilizando o algoritmo Insertion Sort.
Anote o como ficou o vetor após cada iteração do looping interno.

`md int v[] = {2, 6, 4, 5, 3}`
::: Gabarito

```
{2, 6, 4, 5, 3}
{2, 4, 6, 5, 3}
{2, 4, 5, 6, 3}
{2, 4, 5, 3, 6}
{2, 4, 3, 5, 6}
{2, 3, 4, 5, 6}
```

???

Bem fácil não é mesmo? Vamos agora aumentar um pouco a dificuldade do vetor e sua resolução.

??? Checkpoit

Considere o vetor abaixo.

`md int v[] = {10, 6, 15, 5, 7, 3, 1}`

::: Gabarito

```
{6, 10, 15, 5, 7, 3, 1}
{6, 10, 15, 5, 7, 3, 1}
{6, 10, 5, 15, 7, 3, 1}
{6, 5, 10, 15, 7, 3, 1}
{5, 6, 10, 15, 7, 3, 1}
{5, 6, 10, 7, 15, 3, 1}
{5, 6, 7, 10, 15, 3, 1}
{5, 6, 7, 10, 3, 15, 1}
{5, 6, 7, 3, 10, 15, 1}
{5, 6, 3, 7, 10, 15, 1}
{5, 3, 6, 7, 10, 15, 1}
{3, 5, 6, 7, 10, 15, 1}
{3, 5, 6, 7, 10, 1, 15}
{3, 5, 6, 7, 1, 10, 15}
{3, 5, 6, 1, 7, 10, 15}
{3, 5, 1, 6, 7, 10, 15}
{3, 1, 5, 6, 7, 10, 15}
{1, 3, 5, 6, 7, 10, 15}
```

???

Como pudemos ver, para cada iteração houveram inumeras trocas dentro do looping interno para que os menores números chegem suas
posições corretas, desse modo demorando mais tempo para que se completeasse a organização do vetor.

??? Checkpoint
Agora é com você, pense com os seus colegas qual seria melhor que andar apenas um por um, pois essa é a ideia do Insertion Sort

Dica: pense em saltos.

::: Gabarito
Para que tal problema seja solucionado, vamos utilizar de um "gap" que serve como guia para os indices
pularem um numero maior de casas em apenas uma iteração do loop interno. Ou seja, andar em passos maiores que apenas um por um
???


Com essa solução de "pular"/"gap", podemos apresentar o Shell Sort que justamente se apropria dessa ideia
e executa com maestria. O algoritmo pega to tamanho do vetor passado, e apartir dele esse *temp* é criado
que será utilizado para trocar os elementos que estejam distantes. Isso se traduz em criar sub-vetores menores e trabalhar neles

??? Checkpoint

Vamos entender como que o Shell Sort funciona de maneira simplificada. Antes, uma breve 
explicação sobre o gap, ele é um parametro que é deduzido apartir do tamanho do vetor
inicial, existem diversas maneiras de escolher. Para o nosso caso será apenas $N/2$ e $N/4$ e por fim $N/8$.

:shell_2

Anote como que seriam os vetores nesse momento da iteração do algoritmo com esse gap.

::: Gabarito

O vetor ficaria da seguinte maneira:

:shell_3

1°
`md {5, 3, 9, 4}`

2°
`md {6, 1, 8, 7}`

3°
`md {3, 9, 4}`

4° 
`md {1, 8, 7}`

5°
`md {9, 4}`

6°
`md {8, 7}`

???

Então agora é com você, vamos ver ser você realmente entendeu como funciona essa separação
e organização que o Shell Sort proporciona.

??? Checkpoint

Com o mesmo vetor inicial, escreva como que ficariam os vetores delimitados com um Gap de tamanho 4.

::: Gabarito

:shell_4

1°
`md {9, 5}`

2°
`md {8, 6}`

3°
`md {3, 4}`

4°
`md {7, 1}`

Qualquer outro valor de gap que não seja igual a 1, proporcionaria mais de um vetor e dessa forma o Shell Sort entra em ação.

???

??? Checkpoint

Quando chegarmos a um $Gap = 1$, o que aconteceria com o vetor ou com o algoritmo?


:::Gabarito

Isso mesmo, seria apenas uma aplicação de um Insertion Sort básico em um vetor que já está
praticamente inteiro ordenado e arrumado dessa forma facilitando e exigindo poucas
etapas dele para que o vetor esteja completamente ordenado.

???

Repare na animação abaixo como são criado os `md pares` de elementos conforme o `md temp` que depende do tamanho da lista
e como eles são trocados caso o elemento da esquerda seja maior que o elemento da direita do parzinho.

:shell

Complexidade
---

Antes de explicar a complexidade do nosso algorítmo, iremos passar um código de exemplo de como funciona o Shell Sort

``` c 
// Shell sort
void shellSort(int array[], int n) {
  // Rearrange elements at each n/2, n/4, n/8, ... intervals
  for (int interval = n / 2; interval > 0; interval /= 2) {
    for (int i = interval; i < n; i += 1) {
      int temp = array[i];
      int j;
      for (j = i; j >= interval && array[j - interval] > temp; j -= interval) {
        array[j] = array[j - interval];
      }
      array[j] = temp;
    }
  }
}
```

??? Checkpoint

Tendo o código acima em mente e o loop tanto interno quanto externo, deduza qual seria o tamanho deles para `md n` iterações.

::: Gabarito

Loop externo
$$(n - gap)$$

Loop Interno
$$\frac{n}{gap}$$

???

Agora iremos aplicar essa definição para outros tamanhos de Gaps

??? Checkpoint

Quando o Gap é $\frac{n}{2}$, como que ficam os tamanhos do loop externo e intero??

::: Gabarito

Loop externo
$$ (n - \frac{n}{2}) $$

Loop Interno
$$ \frac{n}{\frac{n}{2}} $$


??? Checkpoint

E para um gap de $\frac{n}{4}$?

::: Gabarito

Loop externo
$$ (n - \frac{n}{4}) $$

Loop Interno
$$ \frac{n}{\frac{n}{4}} $$


??? Checkpoint

E para um gap de $\frac{n}{8}$?

:::Gabarito

Loop externo
$$ (n - \frac{n}{8}) $$

Loop Interno
$$ \frac{n}{\frac{n}{8}} $$

???

Bom, acho que deu para pegar a ideia de como que funcionam os loops externos e internos do Shell Sort e suas complexidades basta apenas multiplicar um pelo outro.

$$(n - gap)\frac{n}{gap}$$

??? Checkpoint

Agora é a sua vez de deduzir qual seria a complexidade desse algoritmo. Realize então o somatório de todos os casos
para ter o valor da complexidade do Shell Sort.

::: Gabarito

O somatório de todos os casos de tamanhos de gap, resulta em uma complexidade $$>= O(n²)$$

???

Tendo isso em mente, o Shell Sort se prova mesmo que em seu pior caso, ele é melhor que o Insertion Sort pois o seu melhor caso é uma complexidade 
***O(n²)*** como já visto anteriormente.

Exercícios
---

??? Exercício 1
Dado o vetor a seguir, qual seria a saída do terminal a cada iteração desse vetor corrigido?

vetor = `md {12, 45, 3, 35, 86, 22}`
::: Gabarito
```
{12, 22, 3, 25, 86, 45}
{3, 22, 12, 25, 86, 45}
{3, 12, 22, 35, 45, 86}
```
:::
???

??? Exercício 2
Dado o vetor a seguir, qual seria a saída do terminal a cada iteração desse vetor corrigido?

vetor = `md {46, 22, 1, 75, 35, 85, 64, 56, 12, 5, 97, 42}`
::: Gabarito
```
{46, 22, 1, 5, 35, 42, 64, 56, 12, 75, 97, 85}
{5, 22, 1, 46, 35, 12, 64, 56, 42, 75, 97, 85}
{1, 12, 5, 22, 35, 46, 42, 56, 64, 75, 97, 85}
{1, 5, 12, 22, 35, 42, 46, 56, 64, 75, 85, 97}
```
:::
???

??? Exercício 3
Resolva o vetor a seguir usando o Insertion Sort. Qual seria a saída ao final de cada iteração do loop externo?

vetor = `md {35, 32, 40, 8, 12, 18}`
::: Gabarito
```
{32, 35, 40, 8, 12, 18}
{32, 35, 40, 8, 12, 18}
{8, 32, 35, 40, 12, 18}
{8, 12, 32, 35, 40, 18}
{8, 12, 18, 32, 35, 40}
```
:::
???

??? Exercício 4
Baseado no mesmo vetor do exercício anterior, qual seria o valor da variável `md temp` em cada iteração do loop interno?

vetor = `md {35, 32, 40, 8, 12, 18}`
::: Gabarito
```
1ª iteração:
8
12
18

2ª iteração:
0
0

3ª iteração:
32
```
:::
???

Viu como o Shell Sort é muito mais eficiente que o Insertion Sort?

Curiosidade
---

O intervalo entre os elementos é reduzido com base na sequência utilizada. Algumas das sequências óptimas que podem ser utilizadas no algoritmo de ordenação de conchas são:

Shell's original sequence: N/2 , N/4 , …, 1

Knuth's increments: 1, 4, 13, …, ($3^{k}$ – 1) / 2

Sedgewick's increments: 1, 8, 23, 77, 281, 1073, 4193, 16577...(4j+1+ 3·2j+ 1)

Hibbard's increments: 1, 3, 7, 15, 31, 63, 127, 255, 511…

Papernov & Stasevich increment: 1, 3, 5, 9, 17, 33, 65,...

Pratt: 1, 2, 3, 4, 6, 9, 8, 12, 18, 27, 16, 24, 36, 54, 81....

O desempenho do Shell Sort depende do tipo de sequência utilizada para uma determinada matriz de entrada.

Conclusão
---

Como podemos ver nos exercícios feitos, o Shell Sort é um algorítmo excelente para quando os números pequenos estão muito distantes de seu local final e com poucas iterações
o vetor ficou arrumado e em ordem.