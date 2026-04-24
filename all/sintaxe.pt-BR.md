# SINTAXE E DICAS DA ALL
1. [Soma `+`](#soma)
2. [Subtração `-`](#subtração)
3. [Multiplicação `*`](#multiplicação)
4. [Divisão `/`](#divisão)
5. [Comparação `?`](#comparação)
6. [Entrada/Constantes](#entradaconstantes)
7. [Funções simples](#funções-simples)
8. [Funções inline](#funções-inline)
9. [Funções compostas ou complexas](#funções-compostas-ou-complexas)
10. [Saídas](#saídas)
11. [Comentários `//`](#comentários)
12. [Funções com número variavel de argumentos](#funções-com-número-variavel-de-argumentos)
13. [Boas práticas e objetivo](#boas-práticas-e-objetivo)

# Operações
Há cinco operações, representas pelos símbolos `+ - * / ?`.
**Atenção:** A ordem seguida é a de escrita !
### Soma
Representada normalmente pelo símbolo `+`.
Exemplo de uso:
`a = 1 + 1;` a = 2

### Subtração
Representada normalmente pelo símbolo `-`, tmabém pode representar números negativos.
Exemplos equivalentes de uso:
`a = 3 - 1;` a = 2;
`a = 3 + -1;` a = 2.

### Multiplicação
Representada normalmente pelo símbolo `*`.
Exemplo de uso:
`a = 1 * 1;` a = 1.

### Divisão
Representada normalmente por um unico símbolo `/`.
Exemplo de uso:
`a = 4 / 2;` a = 2.

### Comparação
Representada pelo uso de `?`, seguido 2 a 3 argumentos, tudo separado por `,`.
Os argumentos devem começar com `<` ou `>`, tendo `!` sempre como argumento obrigatório.
Exemplos de uso para `a = B ? C, > 5, < 6, ! 7;` onde:
`B = 2, C = 1` a = 5, pois B é maior que C `>`;
`B = 1, C = 2` a = 6, pois B é menor que C `<`;
`B = 1, C = 1` a = 7, pois as condições anteriores não foram satisfeitas `!`.


# Variaveis
**Atenção:** todas devem terminar com `;`, assim como em outras linguas.
### Entrada/Constantes
Devem ser definidas com `:`.
Ao serem definidas com números, viram constantes.
Ao serem definidas com o próprio nome, viram entradas dentro de seu escopo (ou seja para o programa ou função).
Exemplos equivalentes de uso:
`A:1; B:B; a = A + B;` Colocando a entrada "B" como "1", o resultado de "a" será "2";
`A:1; a = A + :B;` Pode-se definir entradas em modo curto, ou seja, sem usando somente o nome apos os dois pontos.
*Recomenda-se escrever sempre em caixa-alta.*

### Funções simples
Devem ser definidas com `=`.
Podem ser lidas posteriormente, mas nunca re-escritas.
Exemplo:
`a = 1 + 2; b = a * 3;` b = 9.
Também pode-se usar o próprio nome como "memória" dentro da função:
`mem = A ? B, > C, ! mem;`
Neste exemplo se "A" for maior que "B" o valor será substituido por "C", caso contrário continuará o mesmo da iteração anterior.
Na primeira iteração o valor padrão lido da memória será nulo, ou seja, zero.
*Recomenda-se escrever sempre em caixa-baixa.*

### Funções inline
Devem ser escritas dentro de `()` em outras linhas.
Exemplos:
`a = 2 * (9 - 1);` a = 16
`a = 2 * 9 - 1;` a = 17, pois a ordem escrita foi seguida

### Funções compostas ou complexas
Devem ser definidas com `{}`, e chamadas com `[]` junto com os argumentos passados usando `=`.
O argumento final deve ser o proprio nome como função simples, com o valor que deve ser retornado.
Exemplo:
```
func{
	a = :B + :C;
	func = a + 1;
};
resultado = func[B=1, C=2];
```
Onde o resultado seria 4.
Assim como em funções simples, a regra de usar o próprio nome como argumento de memória também funciona.
Componentes separados da função podem ser lidos se mencionados com `.`, ou até mesmo pegar dois valores ao mesmo tempo ao usar `,` na definição:
`resultado, a = func[B=1, C=2].a;` resultado = 4, a = 3.
*Recomenda-se escrever sempre em caixa-baixa.*

### Saídas
São declaradas com `|` antes do nome, depois do valor alvo.
Devem ser pensadas como "sondas".
O nome não pode se repetir no mesmo escopo.
Exemplo:
`A:1; A|Saida; a = A + A;` Saida = 1.
*Recomenda-se escrever com o começo das palavras em caixa-alta e o resto em caixa-baixa.*


# Extras
### Comentários
Como em muitas linguagems, pode ser escrito com `//`, porém o fim deverá ter `;` como variaveis;
`a = 1 + 1; //Texto a ser ignorado pelo compilador/interpretador; b = 2 + 2;` a = 2, e b = 4.

### Funções com número variavel de argumentos
Quando funções compostas são tão genéricas, que poderiam ser utilizadas com varios argumentos, pode-se usar entradas de tamanho variavel.
Para declarar tais entradas é necessario o símbolo `#` seguido do de argumentos (similar a operação de comparação) como número de subargumentos ou se o número é divisivel por tal número, seguido de uma função inline de como deve ser tratado cada subargumento sequencialmente.
Quando o número de argumentos é repetitivo, pode-se usar `.` ao invez de escrever todos.
Para chamar, especifica-se os argumentos dentro de `[]` para uma tal entrada.
Um exemplo de função de soma:
```
sum{
	sum = A#/1(A+.);
};
a = sum[ A=[1,1] ]; //Saída de 2;
b = sum[ A=[1,1,1] ]; //Saída de 3;
```
Um exemplo com uma função com argumentos opcionais, mas com limite de argumentos:
```
func{
	func = A#0(1),1(A),2(A + A);
}
a = func[A=[]];			//Saída de 1;
b = func[A=[5]];		//Saída de 5;
c = func[A=[7, 3]];		//Saída de 10;
d = func[A=[1, 2, 3]];	//Expressão inválida;
```
*No caso da expressão parecer dúbia, não a use !*

### Boas práticas e objetivo
- Sendo uma lingua para projetar/expressar a função de componentes de um computador análogico, ela deve parecer natural para quase qualquer leitor, e ser centrada em conexões físicas que os componentes teriam - colocando a ordem de onde os dados vão passar de cima para baixo, definições em outras páginas, no final, ou começo.
- O nome de entradas e saídas do escopo principal deve ser o nome de componentes de interação do computador, ex: `TERMOMETRO` e `PonteiroDoRelogio`, ou ainda, partes devem ter cada sub-parte nomeada.
- Sendo os componentes algo que tratam sinais elétricos, faz sentido usar multiplicações e divisões pois são alteradoras de proporções, somar e subtrair por números constantes (e não outras variaveis) pode não fazer sentido, por isso nesses casos recomenda-se ter uma entrada no escopo global `:ONE;` usada como referencia para certos cálculos. Ou seja, é importante pensar em proporções, e não em valores.
- Na função comparativa, o argumento `!` deve ser pensando em ser ativado quando os valores não tem uma diferença significativa para ativar o(s) outro(s) argumento(s). Pois em componentes reais é necessario um certo nivel para disparar, ou funcionamentos especificos como em um [schmitt trigger](https://pt.wikipedia.org/wiki/Disparador_Schmitt).
- Assim como a memória pode ser usada repetindo o nome de si como argumento, retro-alimentação pode ser representada usando como argumento um função que será declarada posteriormente.
