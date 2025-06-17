#  Trabalho de Complexidade de Algoritmos - Lotofácil

##  Descrição Geral

Este projeto resolve o problema de **cobertura de subconjuntos para a Lotofácil**, proposto na disciplina de Complexidade de Algoritmos. O objetivo é gerar todas as combinações possíveis de apostas e, a partir delas, encontrar subconjuntos mínimos de apostas de 15 números que **cobrem todas as combinações menores** (de 11 a 14 números), além de analisar a **complexidade de tempo** e o **custo financeiro** dessas soluções.

---

##  Estrutura dos Arquivos

- **main.py**: Menu interativo principal. Permite executar cada etapa do projeto.
- **combinacoes.py**: Gera todas as combinações possíveis de 11 a 15 números. (PROGRAMA 1)
- **cobertura.py**: Aplica heurística gulosa para encontrar subconjuntos de 15 números que cobrem todas as combinações de 11 a 14 números. (PROGRAMAS 2 a 5)
- **analise.py**: Contém a análise de complexidade de tempo dos algoritmos de cobertura. (ITEM 6)
- **custo.py**: Calcula o custo financeiro total para jogar os subconjuntos de apostas encontrados. (ITEM 7)
- **randomico.py**: Implementa uma abordagem randômica alternativa para fins comparativos.
- **relatorio_justificativa.md**: Justificativa técnica e comparativa entre abordagens heurísticas e exatas.

---

##  Funcionamento do Projeto

### 1. Geração das Combinações (PROGRAMA 1)

Gera e salva os seguintes conjuntos:
- **S15** → 3.268.760 combinações de 15 números
- **S14** → 4.457.400 combinações de 14 números
- **S13** → 5.200.300 combinações de 13 números
- **S12** → 5.200.300 combinações de 12 números
- **S11** → 4.457.400 combinações de 11 números

### 2. Cobertura dos Subconjuntos (PROGRAMAS 2–5)

Geração dos subconjuntos SB15_k (k = 11 a 14), usando uma heurística gulosa:
- **SB15_14** cobre todas as sequências de S14
- **SB15_13** cobre todas as sequências de S13
- **SB15_12** cobre todas as sequências de S12
- **SB15_11** cobre todas as sequências de S11

### 3. Análise de Complexidade (ITEM 6)

Veja seção específica mais abaixo.

### 4. Cálculo do Custo Financeiro (ITEM 7)

Multiplica a quantidade de apostas em cada subconjunto SB15_k por R$ 3,00 (preço oficial da Lotofácil).

### 5. Abordagem Randômica

Arquivo `randomico.py` simula seleção aleatória de apostas, servindo como comparação com a heurística gulosa.

---

##  Análise de Complexidade de Tempo

A heurística gulosa possui complexidade aproximada de **O(n · m)**, onde:

- **n** é o número de apostas de 15 números (≈ 3.268.760)
- **m** é o número de subconjuntos a cobrir (S11 a S14)

### PROGRAMA 2 — SB15_14

- Cobertura de 4.457.400 combinações de 14 números
- Tempo elevado pela grande sobreposição entre subconjuntos
- Complexidade: `O(3.2M · 4.4M)` (teórico, mas otimizado com intersecções)

### PROGRAMA 3 — SB15_13

- Cobertura de 5.200.300 combinações de 13 números
- Mais combinações que S14, maior custo computacional

### PROGRAMA 4 — SB15_12

- Cobertura de 5.200.300 combinações de 12 números
- Mesmo volume que S13, mas com sobreposição menor

### PROGRAMA 5 — SB15_11

- Cobertura de 4.457.400 combinações de 11 números
- Tende a ser mais intensivo, pois subconjuntos são menores e menos compartilháveis

>  Todas essas etapas podem levar de **horas a dias** para serem computadas.

---

##  Custo Financeiro Total

Cada cartão de 15 números custa **R$ 3,00**. O programa `custo.py` calcula:

- **Custo total SB15_14** = quantidade de apostas × R$ 3,00
- **Custo total SB15_13** = idem
- **Custo total SB15_12** = idem
- **Custo total SB15_11** = idem

*Os valores exatos dependem da execução da heurística.*

---
##  Por que utilizamos uma heurística?

O problema enfrentado neste projeto é uma variação do **Set Cover Problem** — um problema clássico da ciência da computação que pertence à classe dos problemas **NP-difíceis**. Isso significa que, até hoje, **não existe um algoritmo eficiente conhecido** para resolvê-lo de forma exata em tempo viável, especialmente em larga escala.

###  Por que não usar força bruta?

Uma solução exata exigiria:

- Testar todas as **3.268.760** apostas possíveis de 15 números (combinatória de 25 elementos tomados de 15 em 15).
- Verificar **todos os subconjuntos possíveis** dessas apostas para encontrar o menor grupo que cobre todas as combinações de 11 a 14 números.

Agora, imagine que quiséssemos verificar **todas as combinações de até 50 apostas** dentro de um conjunto de 100 mil apostas geradas.  
O número total de combinações seria:

> **Mais de 10⁹⁰ subconjuntos diferentes**

Esse valor é tão gigantesco que mesmo com supercomputadores modernos, o tempo estimado de execução seria de **milhões de anos**.

---

###  Por que usamos a heurística gulosa?

A heurística gulosa oferece uma solução **aproximada**, porém com ótimo desempenho na prática. Ela encontra apostas de 15 números que cobrem o maior número possível de subconjuntos ainda não cobertos, repetindo esse processo até completar a cobertura.

Resultado:  
-  Tempo de execução razoável (horas ou dias em vez de séculos)
-  Cobertura 100% garantida
-  Complexidade muito mais gerenciável: cerca de O(n × m), onde n ≈ 3 milhões e m ≈ 5 milhões.

Por isso, a heurística não é apenas uma escolha: **é uma necessidade computacional** para este problema.

---

##  Abordagem Alternativa Randômica

O script `randomico.py` executa tentativas de cobertura aleatória.  
Essa abordagem **falha em alcançar cobertura total** de forma eficiente, reforçando a escolha da heurística gulosa.

---

##  Como Executar

1. Execute `main.py` no terminal:
   ```bash
   python main.py
