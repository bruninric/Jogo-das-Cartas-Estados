# Jogo das Cartas

Este repositório contém o seguinte arquivo:

- Jogo das Cartas - Estados

## Descrição

Atividade relacionada ao desafio **Super Trunfo**.

**O trabalho contido neste repositório integra o desenvolvimento do TCC.**

Este é um programa em C que simula um jogo de cartas simples chamado "Jogo dos Estados". Nele, duas cartas, cada uma representando um "estado" (ou uma entidade geográfica com características específicas), são comparadas com base em diversos atributos. O programa solicita ao usuário os dados de cada carta, realiza cálculos para derivar novos atributos e, por fim, compara as duas cartas para determinar qual delas vence em cada categoria.

## Desenvolvimento e Funções (Jogo das Cartas - Estados)

O código foi desenvolvido utilizando a linguagem C e se baseia em uma estrutura principal (`struct Carta`) para armazenar os dados de cada carta.

### Estrutura `Carta`

A `struct Carta` armazena os seguintes dados:
- `estado`: Um caractere identificador (ex: 'A'-'H').
- `codigo[4]`: Um código de 3 caracteres para a carta (ex: "A01").
- `cidade[50]`: Nome da cidade/localidade associada à carta.
- `populacao`: Número de habitantes (unsigned long int).
- `area`: Área em km² (double).
- `pib_bilhoes`: Produto Interno Bruto em bilhões (double).
- `pib_real`: Produto Interno Bruto em valor absoluto (double, calculado).
- `num_pontos_turisticos`: Quantidade de pontos turísticos (int).
- `densidade_populacional`: Habitantes por km² (double, calculado).
- `pib_per_capita`: PIB dividido pela população (double, calculado).
- `super_poder`: Um valor numérico consolidado representando a "força" da carta (float, calculado).

### Principais Funções

1.  **`calcularValoresIniciais(Carta *c)`**:
    * Calcula o `pib_real` convertendo o `pib_bilhoes` para sua representação absoluta.
    * Calcula a `densidade_populacional` (população / área), tratando casos de área zero.
    * Calcula o `pib_per_capita` (PIB real / população), tratando casos de população zero.

2.  **`calcularSuperPoder(Carta *c)`**:
    * Calcula o `super_poder` da carta. Este valor é uma soma ponderada de diversos atributos da carta, incluindo população, área, PIB real, número de pontos turísticos, PIB per capita e o inverso da densidade populacional (tratando divisão por zero).

3.  **`lerDadosCarta(Carta *c, int numeroCarta)`**:
    * Interage com o usuário para coletar os dados básicos de uma carta especificada (população, área, PIB em bilhões, etc.).
    * Realiza a leitura de forma segura, tratando a entrada de strings e caracteres para evitar problemas com buffers ou newlines pendentes.

4.  **`main()`**:
    * **Inicialização**: Declara duas instâncias da `struct Carta`.
    * **Título**: Exibe o título "JOGO DOS ESTADOS".
    * **Entrada de Dados**: Chama `lerDadosCarta` para preencher os dados das duas cartas.
    * **Cálculos**: Chama `calcularValoresIniciais` e `calcularSuperPoder` para cada carta.
    * **Exibição de Dados**: Mostra ao usuário todos os dados (originais e calculados) de ambas as cartas para conferência.
    * **Comparação**: Compara as duas cartas atributo por atributo:
        * **Maior vence**: População, Área, PIB (valor real), Número de Pontos Turísticos, PIB per Capita, Super Poder.
        * **Menor vence**: Densidade Populacional (com lógica especial para valores nulos ou muito próximos de zero, onde zero é considerado o "menor" ideal).
    * **Resultado da Comparação**: Imprime qual carta venceu em cada um dos critérios comparados (indicado por `1` se a Carta 1 venceu, `0` caso contrário ou empate no critério específico).

## Como Compilar e Executar

1.  **Salvar**: Salve o código como um arquivo `.c` (por exemplo, `jogo_estados.c`).
2.  **Compilar**: Use um compilador C (como GCC) para compilar o código.
    ```bash
    gcc jogo_estados.c -o jogo_estados -lm
    ```
    (A flag `-lm` é necessária para linkar a biblioteca matemática devido ao uso de `fabs` e `1e9`).
3.  **Executar**: Rode o executável gerado.
    ```bash
    ./jogo_estados
    ```
    O programa então solicitará a entrada dos dados para as duas cartas e exibirá os resultados.

