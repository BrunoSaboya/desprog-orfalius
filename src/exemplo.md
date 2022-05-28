Shell Sort
======

Retomando o Insertion Sort
---

Como já vimos antes o funcionamento do Insertion Sort neste handout iremos apenas rever os
conceitos mais importantes e algumas atividades relacionadas ao algoritmo.

Ele consiste em um algoritmo cuja complexidade é ***O(n²)*** e, a acada iteração o maior
elemento do vetor está na sua posição correta, dessa forma levando os menores elementos mais
perto de sua posição. Assim como uma analogia a "parte ordenada" e "resto" (parte desordenada).

??? Checkpoint

Considere o vetor abaixo e ordene o vetor utilizando o algoritmo Insertion Sort.
Anote o como ficou o vetor após cada iteração.

`md int v[] = {2, 6, 4, 5, 3}`
::: Gabarito

```
{2, 6, 4, 5, 3}
{2, 4, 6, 5, 3}
{2, 4, 5, 6, 3}
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
{5, 6, 10, 15, 7, 3, 1}
{5, 6, 7, 10, 15, 3, 1}
{3, 5, 6, 7, 10, 15, 1}
{1, 3, 5, 6, 7, 10, 15}
```

???

Como pudemos ver, para cada iteração houveram inumeras trocas para que os menores números para suas
posições corretas, desse modo demorando mais tempo para que se completeasse a organização do vetor.

??? Checkpoint
Agora é com você, pense com os seus colegas qual seria uma boa ideia que resolvesse esse nosso problema
de que os elementos precisam ser movidos uma posição por vez.

Dica: pense em saltos.

::: Gabarito
Para que tal problema seja solucionado, vamos utilizar de um "gap" que serve como guia para os indices
pularem um numero maior de casas em apenas uma iteração do loop interno.
???


Com essa solução de "pular"/"gap", podemos apresentar o Shell Sort que justamente se apropria dessa ideia
e executa com maestria. O algoritmo pega to tamanho do vetor passado, e apartir dele esse *temp* é criado
que será utilizado para trocar os elementos que estejam distantes.

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

???

Então agora é com você, vamos ver ser você realmente entendeu como funciona essa separação
e organização que o Shell Sort proporciona.

??? Checkpoint

Com o mesmo vetor inicial, escolha um outro valor de gap, e escreva como que ficariam os vetores
delimitados.

::: Gabarito

Para apenas fins explicativos e facilitar, esses seriam os vetores caso o gap fosse igual
a 4.

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

Agora vamos explicar como calcular e encontrar a complexidade do Shell Sort. Inicialmente temos a expressão geral para qualquer caso.

$$(n - gap) * \frac{n}{gap} $$

No pior dos casos, a última iteração será um Insertion Sort que por sua vez, fica assim na fórmula acima:

$$(n - 1) * \frac{n}{1} $$

Que possui uma complexidade de **O(n²)**.

Agora vamos generalizar para todos os piores casos.

??? Checkpoint

Inicialmente, na primeira iteração a fórmula fica da seguinte maneira:

$$ (n - \frac{n}{2}) * \frac{n}{\frac{n}{2}} $$

Realize a somatória com seguintes fórmulas enquanto nao atingimos
a iteração de Insertion Sort.

::: Gabarito

Somatório:

$$ (n - \frac{n}{4}) * \frac{n}{\frac{n}{4}} $$

$$ + $$

$$ (n - \frac{n}{8}) * \frac{n}{\frac{n}{8}} $$

$$ ... $$

Desse modo, o somatório de todas elas gera uma complexidade $>= O(n²)$.

???

Tendo isso em mente, o Shell Sort se prova mesmo que em seu pior caso, ele é melhor que o Insertion Sort.


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

Conclusão
---

Como podemos ver nos exercícios feitos, o Shell Sort é um algorítmo excelente para quando os números pequenos estão muito distantes de seu local final e com poucas iterações
o vetor ficou arrumado e em ordem.