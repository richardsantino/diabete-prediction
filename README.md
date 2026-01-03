## Diabetes.
Este projeto tem como objetivo entender como variaveis de pacientes se relacionam com diabetes e criar um modelo preditivo que, baseado em variaveis de entrada, prevê se um paciente tem ou não diabetes.

## Conteúdo
0. [Desafio](#desafio)
1. [Dados](#dados)
3. [Modelo](#modelo)
4. [Insights](#insights)

## Desafio
É parte do desafio executar as seguintes atividades:

**1.** Limpar e tratar os dados. <br>
**2.** Conhecer as variaveis e suas distribuições.  <br>
**3.** Entender como e quais variaveis se relacionam com diabetes. <br>
**4.** Criar um modelo preditivo capaz de classificar se um paciente tem ou não diabetes. <br>
**5.** Comparar o modelo criado com um "preditor" padrão *(disponibilizado no dataset)*.

## Dados
Os dados foram coletados por Mohan Krishna Thalla, trata-se de dados sintéticos que respeitam distribuições coletadas por pesquisa médica de pacientes reais. Por se tratar de dados sintéticos, o projeto de como objetivo pessoal apenas tecnico e qualquer inferência de dados ao mundo real seria erronea.

variaveis dos pacientes:
- **age**: Idade. <br>
- **gender**: Gênero. <br>
- **ethnicity**: Ethnia. <br>
- **education_level**: Level educacional. <br>
- **income_level**: Level de renda. <br>
- **employment_status**: Status de emprego. <br>
- **smoking_status**: Status de fumante. <br>
- **alcohol_consumption_per_week**:	Consumo alcoólico por semana (drinks). <br>
- **physical_activity_minutes_per_week**: Atividade fisica por semana (minutos). <br>
- **diet_score**:	Score de dieta. <br>
- **sleep_hours_per_day**: Tempo de sono por dia (horas). <br>
- **screen_time_hours_per_day**: Tempo de tela por dia (horas). <br>
- **family_history_diabetes**:	Histórico de diabetes na familia. <br>
- **hypertension_history**: Histórico de hipertensão. <br>
- **cardiovascular_history**: Histórico cardiovascular. <br>
- **bmi**: IMC. <br>
- **waist_to_hip_ratio**: Razão entre cintura e quadril. <br>
- **systolic_bp**: Pressão de sangue em fase Sistólica (mmHg). <br>
- **diastolic_bp**:	Pressão de sangue em fase Diastólica (mmHg). <br>
- **heart_rate**: Batimentos cardiacos sob descanso (bpm). <br>
- **cholesterol_total**: Total de colesterol (mg/dL). <br>
- **hdl_cholesterol**: Colesterol lipoproteína de alta densidade ~ "colesterol bom" (mg/dL). <br>
- **ldl_cholesterol**: Colesterol lipoproteína de baixa densidade ~ "colesterol ruim" (mg/dL). <br>
- **triglycerides**: Triglicerídeos (mg/dL). <br>
- **glucose_fasting**: Glicemia de jejum (mg/dL). <br>
- **glucose_postprandial**: Glicemia pós-alimentação (mg/dL). <br>
- **insulin_level**: Insulina no sangue (µU/mL). <br>
- **hba1c**: Hemoglobina Glicada ~ níveis de açúcar no sangue (%). <br>
- **diabetes_risk_score**: "Preditor" padrão ~ Score de diabetes baseado em hábitos e indicadores clínicos. <br>
- **diagnosed_diabetes**: Classifcação de diabetes (Sim/Não). <br>

🔗 [dataset link ~ Kaggle](https://www.kaggle.com/datasets/mohankrishnathalla/diabetes-health-indicators-dataset) <br>

## Modelo
Foram testados três modelos diferentes: **Regressão Logistica**, **Arvore de Decisão** e **Floresta Aleatória**. Entre os três modelos o que obteve melhor performance foi ***Floresta Aleatória***, seu score foi:

ROC-AUC: **1.** (treino), **0.9428** (validação) e **0.9413** (teste).  <br>

O Threshold de **0.25** foi escolhido priorizando o recall (probabilidade de acertar que um paciente tem diabetes dado que ele realmente tem diabetes), pois seria extremamente prejudicial para o paciente se ele não fosse direcionado para tratamento dado que ele possui diabetes, porem a precisão também é levado em conta pois em contra partida não podemos cometer muitos falsos positivos pois cada tratamento possui um custo operacional. Dito isso obtemos os seguintes scores:

precision: **0.8739** = probabilidade de um paciente estar com diabetes dado que o modelo classificou-o como diabetes. <br>
recall: **0.9011** = probabilidade do modelo de classificar o paciente como diabetes dado que o paciente tem diabetes. <br>
accuracy: **0.8634** = probabilidade de acertos. <br>

(obs.: mais informações estão inseridas no arquivo **diabetes_prediction.ipynb**)

## Insights

**1.**
A limpeza foi facilitada pela saude que os dados originalmente possui, porem foi feito poucos tratamentos para se obter uma analise visual mais facilitada, como a inserção dos niveis para colunas ordinais (education_level e income_level) e a troca de 0,1 por No,Yes para colunas binarias (family_history_diabetes, hypertension_history, cardiovascular_history, diagnosed_diabetes]).

**2.**
Distribuições balanceadas no geral. Variaveis categorias e binarias possuem boa frequencia de valores inclusive a variavel target (diagnosed_diabetes), as variaveis numericas seguem uma distribuição normal ou uma similar.

**3.** 
Beaseado no EDA, mais especificamente na *Analise Bivariada* usando Modelo linear generalizado (GLM) com função sigmoidal para inferir insights sobre os coeficientes (variaveis). O GLM obteve um **R²** de 0.4778, logo os coeficientes certamente explicam como as variaveis dos pacientes se relacionam com diabetes.

Sob os coeficientes estatisticamente significantes:
- quanto maior o valor, maior a probabilidade de diabetes: age, family_history_diabetes, bmi, triglycerides, hba1c, gender_Other_.
- quanto maior o valor, menor a probabilidade de diabetes: diet_score, hdl_cholesterol, education_level_Postgraduate_.

variaveis peculiares: gender_Other_, education_level_Postgraduate_. qual será as variaveis ocultas sobre elas? <br>

**4.** 
[Modelo](#modelo)

**5.**
Modelo de arvore aleatória tem performance superior a risk score, onde arvore aleatória possui ROC-AUC: **0.94** e risk score ROC-AUC: **0.66**.
