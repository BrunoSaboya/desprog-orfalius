Shell Sort
======

ideias -> retomar o insertion sort, realizar algumas atividades que levem o leitor
a chegar a conclusão de que ele nao é bom para quando os menores elementos do vetor
estao muito a direita dele e dessa forma o algoritmo é lento. Entao apos isso será
apresentado e introduzido a ideia do Shell Sort e com ela algumas atividadese exercicios
q demonstrem a sua eficiencia e como chegar na conclusao e na ideia principal do algoritmo
e que o seu principal funcionamento sao em vetores cujos elemento menores estao muito
distantes do seu local ou seja, muito a direita.


Retomando o Insertion Sort
---

Como já vimos antes o funcionamento do Insertion Sort neste handout iremos apenas rever os
conceitos mais importantes e algumas atividades relacionadas ao algoritmo.

Ele consiste em um algoritmo cuja complexidade é ***O(n²)*** que a acada ieteração, o maior
elemento do vetor está na sua posição correta, dessa forma levando os menores elementos mais
perto de sua posição. Assim como uma analogia a "parte ordenada" e "resto" (parte desordenada)

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

:shell

Para facilitar mais o entendimento de como funciona o Shell Sort, vamos implementar o 
nosso algoritmo no python.

``` py
def shellSort(array, size)
  for interval i <- size/2n down to 1
    for each interval "i" in array
        sort all the elements at interval "i"
    end shellSort
```

O Shellsort é uma otimização do insertion sort que permite a troca de 
itens que estão muito distantes. A ideia é organizar a lista de elementos de forma que,
a partir de qualquer lugar e pegando qualquer enésimo número, produza uma lista ordenada.
Utilizamos de um numero que serve como índice para alternarmos os itens da lista, esse
índice normalmente é o tamanho da lista passada dividada em 2 (N/2), então por 4 (N/4), por 8 (N/8), até que o valor da divisão 
seja igual a 1 e ocorra um insertion sort normal.

Repare na animação abaixo como são criado os `md pares` de elementos conforme o `md temp` dice que depende do tamanho da lista
e como eles são trocados caso o elemento da esquerda seja maior que o elemento da direita do parzinho.

Aplicações
---

Uma possível maneira de se usar o Shell Sort são para os vetores que possuam elementos de valor pequeno
muito a `md direita` dele, bem distance da sua posição que deve se encontrar ao final das iterações.

Exemplo de vetor cujos elementos menores estão mais a direita:

```
{98, 85, 35, 100, 27, 10, 5, 1}
```

Se fosse utilizado o Insertion Sort nesse vetor, haveriam inúmeras iterações para apenas arrumar um número
e fazendo isso para todo o vetor, seria um processo muito demorado com muitas iterações.

Agora usando o Shell Sort, as iterações seriam as seguintes

```
i = 4
{27, 10, 5, 1, 98, 85, 35, 100}

i = 2
{5, 1, 27, 10, 35, 85, 98, 100}

i = 1
{1, 5, 10, 27, 35, 85, 98, 100}

```

Como podemos ver nas iterações acima, foram necessárias apenas 3 iterações para que o vetor fique arrumado por completo.

Exercícios
---

??? Exercício 1
Dado o vetor a seguir, qual seria a saída do terminal desse vetor corrigido?

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
Dado o vetor a seguir, qual seria a saída do terminal desse vetor corrigido?

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

Conclusão
---

Como podemos ver nos exercícios feitos, o Shell Sort é um algorítmo excelente para quando os números pequenos estão muito
distantes de seu local final assim como poucas iterações tiveram que ser feitas para que o vetor ficasse arrumado.