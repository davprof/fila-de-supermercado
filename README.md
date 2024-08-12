# Desenvolva um simulador de supermercado:

## Revisar conceitos

**Métodos utilitários:**

Random

**Estruturas de dados:**

Priority Queue

LinkedList

Queue

Stream

**Logs:** 
Todas as mudanças de estado (sempre que algo acontece):
1. Cliente chega
2. Cliente escolhe os itens da cesta
3. Cliente escolhe a fila
4. Cliente é atendido.
- Deve ter uma mensagem nos `logs`.

## Entidade Relacionamento

```
+----------------+
|   Produto      |
+----------------+
| - nome         |
| - peso         |
| - preco        |
+----------------+
       |
       |
       | 1..*  contém
       |
+----------------+
|   Cesta        |
+----------------+
| - produtos     |
+----------------+
       |
       |
       | 1        pertence a
       |
+----------------+
|   Cliente      |
+----------------+
| - tipo         |
+----------------+
       |
       | 1..*  entra em
       |
+----------------+
|   Caixa        |
+----------------+
| - id           |
| - fila         |
| - tempoProcesso|
+----------------+
```


## Simulação de Clientes:

Clientes devem ser gerados aleatoriamente e podem escolher vários produtos, os quais serão adicionados a uma cesta de compras.
Cada produto possui três atributos: nome, peso e preço.

## Tipos de Clientes:

Dois tipos de clientes devem ser gerados aleatoriamente:
**Tipo 1:** Prefere ir ao caixa com o menor número de pessoas na fila.
**Tipo 2:** Prefere ir ao caixa com o menor número total de produtos na fila.

## Simulação dos Caixas:

O supermercado deve possuir 3 caixas.
Cada caixa processa os produtos da cesta do cliente a uma taxa de 1 minuto por produto.
Após todos os produtos de um cliente serem processados, o próximo cliente na fila é atendido.

## Duas opções de implementação para a fila no simulador de supermercado:

### 1. Implementação Baseada em Tempo Real
Nesta abordagem, a simulação ocorre em "tempo real" com base em um relógio interno que avança em intervalos regulares. A cada incremento de tempo, o sistema verifica os caixas, processa os produtos, e decide para onde cada cliente deve ir.

#### Funcionamento:
**Relógio Interno:** A simulação avança segundo a segundo (ou minuto a minuto) com um relógio interno.
**Fila dos Caixas:** Cada caixa mantém uma fila de clientes em ordem de chegada.
**Processamento:** A cada minuto, o caixa processa um produto da cesta do cliente que está sendo atendido. Se todos os produtos de um cliente forem processados, o próximo cliente na fila começa a ser atendido.
**Decisão de Caixa:** Quando um novo cliente chega, ele é direcionado ao caixa com menos pessoas (para o Tipo 1) ou ao caixa com menos produtos (para o Tipo 2).

**Vantagens:**
Simula de forma realista o funcionamento de um supermercado.
Fácil de entender e implementar.

**Desvantagens:**
Pode ser menos eficiente em termos de processamento, especialmente se o número de clientes ou produtos for muito grande.


### 2. Implementação Baseada em Priority Queue
Nesta abordagem, as filas dos caixas são implementadas como PriorityQueue, onde a prioridade é definida pelo número de pessoas na fila ou pelo número de produtos que restam para ser processados.

#### Funcionamento:
**Priority Queue:** Existe uma única fila de prioridade global para todos os caixas, onde os clientes são adicionados em ordem de finalização de seus respectivos caixas.
**Ordenação pela Finalização:** A prioridade dentro da fila é baseada no tempo de finalização do atendimento dos clientes anteriores. O tempo de finalização é calculado com base no número de produtos do cliente atual e na ordem cronológica dos atendimentos.
**Processamento:** O próximo cliente a ser atendido é sempre aquele com o próximo tempo de atendimento previsto, respeitando a ordem cronológica. Se um cliente em um caixa tiver o próximo tempo de atendimento antes de outro caixa, ele será atendido primeiro, garantindo que a ordem cronológica seja mantida.


## Considerações:
**Tempo Real:** Foca em uma simulação mais direta, onde cada caixa opera independentemente.
**Priority Queue:** Garante que o próximo cliente a ser atendido é aquele cuja finalização ocorrerá primeiro, otimizando o processamento em um cenário com múltiplos caixas.
