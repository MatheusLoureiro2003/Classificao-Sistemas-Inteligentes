# Classificao-Sistemas-Inteligentes
Classificaça o Resgate de Vítimas de Catástrofes Naturais, Desastres ou Grandes Acidentes

Tarefa 1: Classificaça o
Resgate de Vítimas de Catástrofes Naturais, Desastres ou Grandes Acidentes
Objetivo da tarefa
Construir um modelo de classificação com CART e outro com Redes Neurais MLP (RN): dadas
as características de 1 a 10 (ver descrição dos atributos), o modelo aprendido deve aprender a
classificar o estado de uma vítima que corresponde à característica 13 (tri). Esta característica
vem do protocolo START (Simple Triage and Rapid Treatment) utilizado para classificar uma
vítima de acordo com as cores:
• verde (0): ferimentos leves que não representam risco à vida
• amarela (1): ferimentos graves; podem aguardar um pouco
• vermelha (2): ferimentos críticos; requerem tratamento imediato para sobreviver
• preta (3): salvamento inviável; morto
Requisitos
1. O formato do dataset para treinamento está aqui.
2. Não é permitido utilizar as seguintes características como entradas de treinamento:
11 gcs, 12 avpu, 13 tri e 14 sobr.
3. Saída:
13 tri:
Você pode se inspirar nos códigos disponíveis no Google Colab: Classificador CART
Procedimento e relatório
TREINAMENTO/VALIDAÇÃO
1) Gere um dataset de treinamento/validação com o programa gerar_dados_vitimas.py
O número de vítimas deve ser entre 2.000 e 10.000 vítimas (utilize uma semente fixa
para fins de reprodutibilidade).
a. Descreva os parâmetros de criação do dataset: número de vítimas, idade,
desvio padrão, ruído e tipo de acidente.
b. Defina o número de folds para realizar a validação cruzada
2) Treine o CART com o dataset de treinamento/validação com o método da validação
cruzada.
a. utilize diversas hiperparametrizações variando ao menos max_depth,
min_samples_leaf e criterion,
b. escolha a melhor delas com base no maior f-score médio da validação cruzada,
c. descreva a melhor hiperparametrização.
3) Treine a RN com o dataset de treinamento/validação com validação cruzada.
a. utilize diversas hiperparametrizações: número de camadas ocultas, número de
neurônios/camada, função de ativação e taxa de aprendizado
b. Escolha a melhor delas com base no maior f-score médio da validação cruzada
UTFPR/Curitiba - SISTEMAS INTELIGENTES 1 – 2026/1 – Prof. Tacla
c. descreva a melhor hiperparametrização.
4) Compare os resultados do melhor modelo CART x melhor modelo de RN.
a. Viés: compare o f-score médio de treino com o f-score médio de validação
(aproximação empírica do viés estatístico pelas médias calculadas sobre os kfolds). Utilize a tabela abaixo como modelo sendo 𝑓𝑠𝑡
, o f-score de treino, 𝑓𝑠𝑣
,
de validação.
𝑓𝑠̅̅̅ =
1
𝑘
∑ 𝑓𝑠𝑡
𝑘
𝑖=1
sendo 𝑓𝑠𝑡𝑖 = 2(𝑃. 𝑅)/(𝑃 + 𝑅)
𝑃 = 𝑝𝑟𝑒𝑐𝑖𝑠ã𝑜 𝑒 𝑅 = 𝑟𝑒𝑐𝑎𝑙𝑙, k=número do fold
MÉDIA f-score CART RN
treino 𝑓𝑠̅̅̅
𝑡 𝑓𝑠̅̅̅
𝑡
Validação 𝑓𝑠̅̅̅
𝑣 𝑓𝑠̅̅̅
𝑣
Diferença abs. | 𝑓𝑠̅̅̅
𝑡 − 𝑓𝑠̅̅̅
𝑣 | | 𝑓𝑠̅̅̅
𝑡 − 𝑓𝑠̅̅̅
𝑣 |
b. Variância (estabilidade do modelo): comparar as variâncias de f-score
calculadas sobre os k-folds (como uma aproximação empírica da variância
estatística):
𝑉𝑎𝑟 =
1
𝑘
∑(𝑓𝑠𝑖 − 𝑓𝑠̅)
2
𝑘
𝑖=1
MÉDIA var. CART RN
treino 𝑉𝑎𝑟𝑡 𝑉𝑎𝑟𝑡
Validação 𝑉𝑎𝑟𝑣 𝑉𝑎𝑟𝑣
Diferença abs. 𝑉𝑎𝑟𝑡 − 𝑉𝑎𝑟𝑣 𝑉𝑎𝑟𝑡 − 𝑉𝑎𝑟𝑣
TESTES CEGOS
5) Retreino: com todo o dataset de treino/validação e com as melhores
hiperparametrizações de CART e da RN obtidas nas etapas 2 e 3:
a. treine um novo modelo com CART e
b. treine um novo modelo com RNs.
6) Teste cego: com o dataset de teste cego (1000v), compare os valores de precisão,
recall e f-score do modelo CART (5a) x modelo RNs (5b). Use o dataset de teste cego
somente neste item, se for usado em qualquer outra etapa de treino/validação,
configura-se vazamento de dados (data leakage).
7) Analise:
a. observando os resultados de teste cego, comente sobre a capacidade de
generalização dos modelos CART (5a) x modelo RNs (5b) levando em conta os
conceitos de overfitting e underfitting;
b. com base na matriz de confusão do teste cego somente, as classes que
apresentam mais problemas e aquelas que apresentam menos problemas para
o classificador. Justifique.
UTFPR/Curitiba - SISTEMAS INTELIGENTES 1 – 2026/1 – Prof. Tacla
c. por fim, se o modelo que apresentou os melhores resultados na etapa de
treino/validação (1-4) teve melhor desempenho nos testes cegos. Caso não,
justifique.
