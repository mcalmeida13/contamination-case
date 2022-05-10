# Predição de probabilidade de contaminação viral utilizando Machine Learning 


## 1) Definição do problema: 

### Que problema estamos tentando resolver?  

Este case tem como objetivo avaliar os níveis de contaminação de um vírus no país X, gerando insights através de dados fornecidos pelo Gorverno.

![alt text](https://github.com/mcalmeida13/neoway-case/blob/main/img/2022-05-04_14-56.png?raw=true)




Sabe-se que a transmissão acontece de pessoa por pessoa, por isso elas devem estar conectadas de alguma maneira (familia, amizade ou trabalho). Foi fornecido um dataset com o nível de proximidade das pessoas e a frequência com que se encontram e a probabilidade da transmissão entre os indivíduos.

Já foi repassado também que a porbabilidade transmissão de um indivíduo A para B não é igual a de B para A, o que sugere que os atributos de cada indivíduo contribuem para a probabilidade de adoecer


![alt text](https://github.com/mcalmeida13/neoway-case/blob/main/img/2022-05-04_15-08.png?raw=true)

Foi fornecido outro dataset onde cada linha representa um indivíduo e um conjunto de atributos associados.

Este projeto tem o objetivo de prever utilizando Machine Learning a probabilidade de contaminação de um indivíduo **V1** para o indivíduo **V2** utilizando informações sobre cada indivíduo e suas relações.

Iremos atacar o problema utilizando **modelos de regressão**.

Os dados foram fornecidos pelo Governo do país, interessado em tomar decisões mais inteligentes.

## Metodologia

Para resolver o problema, utilizaremos as bibliotecas `pandas`, `Matplotlib` e `NumPy` para Análise exploratória e `Scikit-Learn` para modelagem.


Esse notebook é o passo a passo para criar o modelo final, que será salvo no formato `pickle`, que predizerá a probabilidade de contaminação ao receber as características dos indivíduos como input, além de uma lista de conexões com a probabilidade de contaminação preenchida. 

## 2) Dados:
Datasets para o problema: 

#### `individuos_espec.csv`

características de cada indivíduo 
-`name`: Id dos indivíduos 
-`idade`: idade dos indivíduos 
-`estado_civil`: Estado civil dos indivíduos
-`qt_filhos`: quantidade de filhos dos indivíduos 
-`estuda`: caso estudem 
-`trabalha`: caso trabalhem 
-`pratica_esportes`: caso pratiquem esportes 
-`transporte_mais_utilizado`: qual o transporte mais utilizado 
-`IMC`: valor do índice de massa corporal dos indivíduos 

#### `conexoes_espec.csv` 

lista das conexões e algumas características das mesmas 
- `V1`: id do individuo (relação entre os indivíduos) 
- `V2`: id do individuo (relação entre os indivíduos) 
-`grau`: familia, amigos, trabalho 
-`proximidade`: 
    - mora_junto, 
    - visita_frequente, 
    - visita_casual, 
    - visita_rara
- `prob_V1_V2`: taxa de contaminação de V1 (doente) para V2 (saudável) (essa é a **variável alvo**)

#### Como esses dados se comunicam?

Para gerar o dataset, precisamos fazer a ligação de duas cópias do dataset das características individuais das pessoas com seu nível de proximidade

![alt text](https://github.com/mcalmeida13/neoway-case/blob/main/img/2022-05-04_17-22.png?raw=true)

O dataset para treinar o modelo (`df_known`) será aquele que a variável `prob_V1_V2` será não nula e o dataset para entregar ao cliente será o que utulizaremos o modelo para prever a probabilidade (`df_unknown`) 


## 3) Projeto:

Projeto está estruturado da seguinte forma:
- Exploração
    - Indivíduos (`individuos_EDA.ipynb`)
    - Conexões (`conexoes_EDA.ipynb`)

- Preparação + Modelagem
    - Treinamento (`model_training.ipynb`): 
        - Merge dos datasets
        - Train/Test Split
        - Inputação de valores faltantes
        - Modelos
        - Cross Validation
        - Tunagem de hiperparâmetros

- Predição final (`model_predicting.ipynb`)


## 4) Resultados:
Métrica escolhida foi o Erro absoluto médio (Mean squared error - MAE) por serem números menores que, a métrica de erro médio quadrado mascararia a acurácia do modelo.
Modelo final performou com `MAE = 0.037` o que gera uma medição `predicto(%) = real(%) ± 3.7%`

![alt text](https://github.com/mcalmeida13/neoway-case/blob/main/img/model_result.png?raw=true)

O modelo treinado está salvo nesse repositório como `rf_final.pkl`

A predição da probabillidade de contaminação dos outros indivíduos estão no notebook `model_predicting.ipynb`