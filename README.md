# 🤖 Implementação e Análise do Algoritmo K-Means do Zero

> **Projeto acadêmico de grande porte desenvolvido em grupo**, com implementação completa do algoritmo K-Means a partir do zero, análise de desempenho em múltiplos cenários, visualizações ricas e comparação direta com a biblioteca scikit-learn.

---

## 👥 Sobre o Projeto

Este é um projeto **extenso e complexo**, desenvolvido colaborativamente, que vai muito além de simplesmente "chamar uma função de biblioteca". O grupo optou por construir o algoritmo K-Means **inteiramente do zero em Python puro com NumPy**, cobrindo desde a inicialização dos centróides até critérios de parada, tratamento de casos extremos, análise de convergência e validação dos resultados.

O notebook contém mais de **12 seções estruturadas**, dezenas de funções documentadas, 6 tipos de gráficos distintos e uma análise comparativa rigorosa, tornando-o uma referência completa sobre o funcionamento interno do K-Means.

---

## 📋 Índice

1. [O que é o K-Means?](#o-que-é-o-k-means)
2. [Estrutura do Projeto](#estrutura-do-projeto)
3. [Datasets Utilizados](#datasets-utilizados)
4. [Normalização dos Dados](#normalização-dos-dados)
5. [Implementação do Zero](#implementação-do-zero)
6. [Análise de Convergência](#análise-de-convergência)
7. [Análise de Inicialização](#análise-de-inicialização)
8. [Método do Cotovelo](#método-do-cotovelo)
9. [Comparação com scikit-learn](#comparação-com-scikit-learn)
10. [Tecnologias Utilizadas](#tecnologias-utilizadas)
11. [Como Executar](#como-executar)

---

## 🧠 O que é o K-Means?

O **K-Means** é um algoritmo de aprendizado de máquina não supervisionado que agrupa dados em **K clusters** (grupos), buscando minimizar a variabilidade intra-cluster — ou seja, garantir que os pontos dentro de um mesmo grupo sejam os mais parecidos entre si possível.

### Como funciona (passo a passo)

O algoritmo segue um ciclo iterativo simples e elegante:

**1. Inicialização:** São escolhidos aleatoriamente K pontos do dataset para serem os centróides iniciais de cada cluster.

**2. Atribuição:** Cada ponto do dataset é calculado com a distância euclidiana até todos os centróides, sendo atribuído ao cluster do centróide mais próximo. A fórmula utilizada é:
