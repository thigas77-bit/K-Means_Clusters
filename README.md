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

**2. Atribuição:** Cada ponto do dataset tem sua distância euclidiana calculada até todos os centróides, sendo atribuído ao cluster do centróide mais próximo, usando a fórmula `d = √((x₁ - y₁)² + (x₂ - y₂)²)`.

**3. Atualização:** A posição de cada centróide é recalculada como a **média aritmética** de todos os pontos pertencentes ao seu cluster.

**4. Repetição:** Os passos 2 e 3 se repetem até que um critério de parada seja atingido.

**5. Parada:** O algoritmo encerra quando os centróides não se movem mais (`centroides_sem_mudanca`), quando o deslocamento total fica abaixo de uma tolerância definida (`tolerancia_atingida`), ou quando o número máximo de iterações é atingido (`max_iter`).

### Como foi utilizado neste projeto

O K-Means foi implementado do zero e testado em **4 cenários distintos de dados bidimensionais**, cada um representando um desafio diferente para o algoritmo. O objetivo foi observar como o algoritmo se comporta em condições favoráveis e desfavoráveis, analisando convergência, variabilidade, impacto da inicialização e limitações inerentes ao método.

---

## 🗂️ Estrutura do Projeto

O notebook está organizado em 12 seções sequenciais: Importações, Geração dos Datasets (4 Cenários), Normalização dos Dados com MinMaxScaler, Implementação do K-Means do Zero, Execução do K-Means nos 4 Cenários, Gráfico dos Clusters Finais com Centróides e Variabilidade, Gráficos de Variabilidade, Dissimilaridade e Deslocamento por Iteração, Gráfico de Evolução da Convergência, Análise de Inicialização com 10 sementes diferentes, Comparação entre Dados Normalizados e Não Normalizados, Método do Cotovelo de k=2 a 20, e Comparação com scikit-learn.

---

## 📊 Datasets Utilizados

O projeto utiliza dados **sintéticos bidimensionais** gerados com `make_blobs` e `numpy.random`, cobrindo 4 cenários cuidadosamente planejados:

| Cenário | Descrição | Dificuldade |
|--------|-----------|-------------|
| **Cenário 1** | Clusters Isolados — 4 grupos bem separados, baixa dispersão (`std=1.0`) | Fácil |
| **Cenário 2** | Clusters Próximos com Sobreposição — alta dispersão (`std=2.8`), centros próximos | Difícil |
| **Cenário 3** | Clusters Alongados — transformação linear aplicada para "esticar" os grupos | Desafiador |
| **Cenário 4** | Sem Clusters Definidos — distribuição uniforme aleatória, sem estrutura real | Extremo |

Cada cenário contém **1.200 amostras** e **2 features**, totalizando 4.800 pontos de dados.

> O Cenário 3 é particularmente relevante para entender uma **limitação conhecida do K-Means**: o algoritmo assume clusters com formato esférico, portanto tem dificuldades com grupos alongados ou com formas não convexas.

---

## ⚖️ Normalização dos Dados

Antes de executar o algoritmo, os dados são normalizados com **MinMaxScaler**, transformando todas as variáveis para o intervalo `[0, 1]`. Essa etapa é fundamental porque o K-Means baseia seus cálculos na **distância euclidiana**. Sem normalização, variáveis em escalas maiores dominam o cálculo de distância, distorcendo os agrupamentos. O projeto demonstra esse efeito com uma comparação direta entre os resultados com e sem normalização para todos os cenários.

---

## ⚙️ Implementação do Zero

O coração do projeto. Todas as funções foram escritas manualmente, sem depender das implementações prontas das bibliotecas:

**`dist_calc1(ponto, centroide)`** — Calcula a distância euclidiana entre dois pontos.

**`inicializar_centroides(X, k, random_state)`** — Seleciona K pontos aleatórios do dataset como centróides iniciais.

**`atribuir_clusters(X, centroides)`** — Atribui cada ponto ao cluster do centróide mais próximo.

**`atualizar_centroides(X, rotulos, k, centroides_atuais)`** — Recalcula a posição de cada centróide como a média do seu cluster. Inclui tratamento para **clusters vazios** via estratégia *Max-distance restart*: o centróide vazio é reinicializado no ponto mais distante de qualquer centróide ativo.

**`calcular_variabilidade(X, rotulos, centroides)`** — Calcula a soma das distâncias quadráticas dos pontos ao seu centróide (variabilidade intra-cluster).

**`calcular_dissimilaridade(centroides)`** — Calcula a média das distâncias euclidianas entre todos os pares de centróides (separação entre clusters).

**`kmeans(X, k, max_iter, tol, random_state)`** — Função principal que orquestra todo o algoritmo e retorna um dicionário rico com centróides finais, rótulos, histórico completo de iterações, número de iterações, critério de parada, variabilidades, dissimilaridade e indicador de cluster vazio.

---

## 📈 Análise de Convergência

Uma das partes mais ricas do projeto é o acompanhamento detalhado de **como o algoritmo evolui** a cada iteração. Para cada cenário são gerados:

- **Gráfico 2:** Visualização dos clusters finais com os centróides destacados e a variabilidade de cada grupo na legenda.
- **Gráfico 3:** Evolução da **variabilidade total** por iteração — mostra a queda progressiva à medida que os clusters se consolidam.
- **Gráfico 4:** Evolução da **dissimilaridade** (distância média entre centróides) por iteração.
- **Gráfico 5:** Evolução do **deslocamento dos centróides** por iteração — quando chega a zero, o algoritmo convergiu.
- **Gráfico 6:** *Snapshots* visuais da posição dos clusters em iterações intermediárias, mostrando o processo de convergência em tempo real.

---

## 🎲 Análise de Inicialização

Um dos problemas clássicos do K-Means é sua **sensibilidade à inicialização aleatória** — dependendo dos centróides iniciais, o algoritmo pode convergir para soluções subótimas.

O projeto testa **10 sementes diferentes** (seeds 0 a 9) para cada cenário e registra variabilidade total, dissimilaridade, número de iterações e critério de parada. Os resultados revelam comportamentos distintos:

- No **Cenário 1** (clusters bem separados), a maioria das sementes converge para a solução ótima (variabilidade ≈ 2.02), mas sementes ruins resultam em valores até 15× maiores.
- No **Cenário 2** (clusters sobrepostos), todas as sementes convergem para valores similares, indicando que o espaço de soluções é mais uniforme.
- No **Cenário 3** (clusters alongados), há variação relevante, evidenciando a limitação do K-Means com formatos não esféricos.

---

## 📐 Método do Cotovelo

Para determinar o **número ideal de clusters K**, o projeto implementa e aplica o **Método do Cotovelo** (*Elbow Method*), testando valores de k de 2 a 20 para todos os cenários.

A lógica é observar onde a curva de variabilidade total "dobra" — o ponto em que aumentar K deixa de gerar ganho expressivo na qualidade dos clusters. Os gráficos revelam:

- **Cenário 1:** Cotovelo nítido em k=4, confirmando a estrutura real dos dados.
- **Cenário 2:** Cotovelo menos pronunciado, refletindo a maior dificuldade de separação.
- **Cenário 3:** Comportamento intermediário devido ao formato elongado dos clusters.
- **Cenário 4:** Curva suave e sem cotovelo evidente — esperado, pois não há estrutura real de grupos nos dados.

---

## 🔬 Comparação com scikit-learn

O projeto vai além e valida a implementação comparando-a diretamente com o `KMeans` do **scikit-learn** nos 4 cenários. A comparação mede variabilidade total, número de iterações e tempo de execução:

| Cenário | Métrica | Nossa Impl. | scikit-learn |
|--------|---------|-------------|--------------|
| Cenário 1 | Variabilidade Total | 2.0231 | 31.4678 |
| Cenário 1 | Iterações | 3 | 4 |
| Cenário 2 | Variabilidade Total | 21.2079 | 21.1491 |
| Cenário 2 | Iterações | 32 | 7 |
| Cenário 3 | Variabilidade Total | 8.1840 | 6.5430 |
| Cenário 4 | Variabilidade Total | 50.2211 | 50.2276 |

A comparação mostra que nossa implementação é funcionalmente correta e encontra soluções de qualidade comparável. A diferença de velocidade é esperada, pois o scikit-learn usa operações vetorizadas otimizadas em C/Fortran, enquanto a nossa usa loops Python puros — o que torna a implementação didaticamente mais clara e transparente.

---

## 🛠️ Tecnologias Utilizadas

- **Python 3**
- **NumPy** — operações matriciais e cálculos numéricos
- **Matplotlib** — todas as visualizações e gráficos
- **scikit-learn** — geração de datasets (`make_blobs`), normalização (`MinMaxScaler`) e comparação (`KMeans`)
- **Google Colab** — ambiente de execução e desenvolvimento colaborativo

---

## ▶️ Como Executar

1. Acesse o notebook pelo Google Colab.
2. Execute as células em ordem sequencial (de cima para baixo).
3. Todas as dependências já estão disponíveis no ambiente Colab — não é necessária nenhuma instalação adicional.

Para rodar localmente, instale as dependências com `pip install numpy matplotlib scikit-learn` e abra o notebook com `jupyter notebook notebook.ipynb`.

---

## 📌 Observações Finais

Este projeto foi desenvolvido com foco didático e analítico. Cada função possui docstrings detalhadas explicando sua lógica, parâmetros e decisões de implementação. O notebook é autocontido e pode ser usado como material de estudo sobre o funcionamento interno do K-Means, suas limitações e boas práticas de aplicação.

---

*Projeto acadêmico — todos os direitos reservados ao grupo.*
