# Aprendizado de Máquina Aplicado à Distribuição de Circuitos Elétricos Residenciais

**Sistema especialista com aprendizado supervisionado — atividade adaptada ao setor de energia**

**Área:** Inteligência Artificial e LFA | Sistemas Especialistas  
**Autores:** 

Nome: Victor Alves Moreira RGM: 30159067

Nome: Beatriz Nevis Miranda RGM: 37227581

Nome: Paulo André Gemmal Fonseca RGM: 38030144

Nome: Maurício Gabriel Gemmal Fonseca RGM: 38031183


> [!IMPORTANT]
> Este é um **protótipo didático** de apoio ao aprendizado e à análise preliminar de instalações elétricas. **Não substitui** o projeto, o dimensionamento ou a execução por profissional habilitado. Trabalhar com eletricidade oferece riscos.

## Visão geral

O projeto propõe um sistema especialista em Python para ajudar estudantes e moradores a compreender a **organização de circuitos elétricos residenciais**. A ferramenta recebe características de um ponto de consumo, estima a corrente elétrica, classifica o circuito por aprendizado supervisionado e aplica **regras técnicas explícitas** para justificar sua orientação.

O sistema classifica os pontos em três categorias:

- **Iluminação**;
- **Tomadas de uso geral**;
- **Circuitos exclusivos** para determinados equipamentos.

A proposta integra uma **árvore de decisão** com um **motor de regras SE... ENTÃO...**, inspirado em requisitos da ABNT NBR 5410.

## 1. Fundamentação

### O que são sistemas especialistas?

Sistemas especialistas são aplicações de inteligência artificial voltadas a apoiar a resolução de problemas e a tomada de decisões por meio de conhecimentos e regras semelhantes aos utilizados por um profissional experiente. Podem fornecer orientações em áreas como saúde, engenharia, educação e finanças, respeitando seus limites de aplicação.

### Conceitos de aprendizado de máquina

- **Aprendizado de máquina:** um algoritmo identifica padrões a partir de exemplos e os utiliza para analisar novos casos.
- **Aprendizado supervisionado:** o treinamento utiliza exemplos cujas respostas esperadas, chamadas **rótulos**, são conhecidas.
- **Atributos:** informações fornecidas ao modelo, como corrente elétrica, indicação de ponto de iluminação e uso exclusivo.
- **Rótulos:** `iluminacao`, `tomadas_gerais` e `circuito_exclusivo`.
- **Classificação:** prevê uma categoria de circuito. Diferentemente, a regressão estimaria uma variável numérica contínua.
- **Treino e teste:** a separação permite verificar o desempenho em exemplos não utilizados durante o ajuste do modelo.

### Como as duas abordagens trabalham juntas

1. O usuário informa as características do ponto de consumo.
2. O sistema calcula a corrente elétrica.
3. A árvore de decisão sugere a categoria do circuito.
4. O motor de inferência considera também se o local é uma área molhada e aplica as regras pertinentes.
5. A ferramenta apresenta a classificação e uma recomendação justificada.

A relação usada no exemplo didático é:

$$
I\,(A)=\frac{P\,(W)}{V\,(V)}
$$

**Exemplo:** para um chuveiro resistivo de **5.500 W**, em **220 V**, a corrente é **25,00 A** (`5500 / 220`). Essa expressão é usada nos exemplos para cargas resistivas com fator de potência igual a 1.

## 2. Exemplo de distribuição de circuitos por cômodo

O estudo considera uma residência **hipotética**, alimentada em **220 V fase-neutro**, como referência ao sistema 380/220 V do Distrito Federal. Os valores de potência abaixo são **estimativas pedagógicas**: não são medições de equipamentos reais nem cálculos normativos de previsão mínima em VA.

| Cômodo | Ponto / equipamento | Potência (W) | Tensão (V) | Corrente (A) | Circuito |
|---|---|---:|---:|---:|:---:|
| Sala | Iluminação | 120 | 220 | 0,55 | C1 |
| Sala | Tomadas gerais | 900 | 220 | 4,09 | C2 |
| Quarto 1 | Iluminação | 80 | 220 | 0,36 | C1 |
| Quarto 1 | Tomadas gerais | 700 | 220 | 3,18 | C2 |
| Quarto 2 | Iluminação | 80 | 220 | 0,36 | C1 |
| Quarto 2 | Tomadas gerais | 600 | 220 | 2,73 | C2 |
| Cozinha | Iluminação | 100 | 220 | 0,45 | C1 |
| Cozinha | Tomadas gerais | 1.800 | 220 | 8,18 | C3 |
| Banheiro | Iluminação | 60 | 220 | 0,27 | C1 |
| Banheiro | Tomada de uso geral | 600 | 220 | 2,73 | C4 |
| Banheiro | Chuveiro exclusivo | 5.500 | 220 | 25,00 | C6 |
| Área de serviço | Iluminação | 60 | 220 | 0,27 | C1 |
| Área de serviço | Tomadas gerais | 1.600 | 220 | 7,27 | C5 |
| Quarto 2 | Ar-condicionado exclusivo | 1.200 | 220 | 5,45 | C7 |

**Outros exemplos de cálculo:** tomadas da sala: `900 / 220 = 4,09 A`; tomadas da cozinha: `1800 / 220 = 8,18 A`.

### Quadro de organização didática dos circuitos

| Circuito | Destinação | Potência (W) | Corrente (A) | Condutor — indicação didática |
|:---:|---|---:|---:|---|
| C1 | Iluminação de todos os cômodos | 500 | 2,27 | Cobre 1,5 mm²: mínimo de referência |
| C2 | Tomadas da sala e dos quartos | 2.200 | 10,00 | Cobre 2,5 mm²: mínimo de referência |
| C3 | Tomadas da cozinha | 1.800 | 8,18 | Cobre 2,5 mm²: mínimo de referência |
| C4 | Tomada do banheiro | 600 | 2,73 | Cobre 2,5 mm²: mínimo de referência |
| C5 | Tomadas da área de serviço | 1.600 | 7,27 | Cobre 2,5 mm²: mínimo de referência |
| C6 | Chuveiro (uso exclusivo) | 5.500 | 25,00 | Seção a dimensionar; não determinar apenas pela corrente |
| C7 | Ar-condicionado (uso exclusivo) | 1.200 | 5,45 | Seção a dimensionar conforme instalação e manual |

**Atenção:** a soma ilustrativa de **13.400 W** corresponde a **60,91 A** ao somar as correntes dos circuitos terminais de 220 V. **Isso não determina a corrente do alimentador nem a do disjuntor geral.** Um projeto real deve considerar demanda, simultaneidade, distribuição entre fases e características do fornecimento.

Os circuitos exigem condutores ativos adequados, neutro quando necessário e condutor de proteção (**PE**). As seções **1,5 mm²** (iluminação) e **2,5 mm²** (tomadas) são mínimos usuais de referência da NBR 5410, **não bitolas finais aprovadas**. O dimensionamento precisa avaliar capacidade de corrente, método de instalação, temperatura, agrupamento, queda de tensão, proteções e curto-circuito.

O material também apresenta uma tabela ilustrativa de corrente admissível para cabos de cobre com isolamento PVC 70 °C, método B1 e dois condutores, reproduzida abaixo **apenas como exemplo da condição indicada**, sem uso como dimensionamento automático:

| Seção (mm²) | Corrente indicada (A) |
|---:|---:|
| 1,5 | 17,5 |
| 2,5 | 24 |
| 4 | 32 |
| 6 | 41 |
| 10 | 57 |
| 16 | 76 |

Fonte da ilustração: [Eletroproj — Bitola de fio: tabela de fios e amperagem](https://eletroproj.com.br/bitola-de-fio-tabela-amperagem-e-aplicacoes/).

**Regra importante:** o circuito C2 soma 10,00 A por agrupar várias tomadas. Isso **não** significa que cada tomada precise de circuito próprio. O requisito de circuito independente mencionado na NBR 5410, item 9.5.3.1, refere-se ao ponto destinado a equipamento individual cuja corrente nominal seja superior a 10 A.

## 3. Base normativa

A referência para o padrão de entrada de unidades consumidoras individuais em baixa tensão é a **Neoenergia Brasília DIS-NOR-030, revisão 07, de 17/04/2026**. Os itens 6.15.1 e 6.15.2 atribuem ao consumidor a segurança da instalação interna e exigem conformidade com a ABNT NBR 5410. A norma da distribuidora **não é** uma tabela para escolher bitolas por cômodo.

| Fonte | Aplicação no projeto |
|---|---|
| Neoenergia Brasília — DIS-NOR-030, rev. 07 | Condições de fornecimento, medição, aterramento e padrão de entrada; exigência de atendimento à NBR 5410 na instalação interna. |
| ABNT NBR 5410 | Divisão de circuitos, seções mínimas, tomadas em áreas específicas, dimensionamento e proteção. |
| ANEEL — Resolução Normativa nº 1.000/2021 e PRODIST | Regras regulatórias de distribuição/conexão; não substituem a NBR 5410 para dimensionamento interno. |
| Materiais técnicos do MME e da Rede e-Tec/MEC | Orientações sobre condutores, capacidade de corrente, queda de tensão e dispositivo DR. |

## 4. Base de dados e separação para treino

O arquivo **`dataset_circuitos_residenciais.csv`** reúne **36 registros inteiramente simulados**:

- 12 de `iluminacao`;
- 12 de `tomadas_gerais`;
- 12 de `circuito_exclusivo`.

Cada registro armazena cômodo, potência, tensão, corrente, finalidade do ponto e classe. A tensão de referência é **220 V** e a corrente é derivada de `P / V`. A informação **área molhada** é fornecida no momento da consulta e considerada pelo motor de regras, **não pela árvore de decisão**.

| Amostra | Potência (W) | Tensão (V) | Corrente (A) | Ponto de luz | Uso exclusivo | Rótulo |
|---|---:|---:|---:|:---:|:---:|---|
| Quarto | 160 | 220 | 0,73 | Sim | Não | `iluminacao` |
| Sala | 1.000 | 220 | 4,55 | Não | Não | `tomadas_gerais` |
| Banheiro | 5.500 | 220 | 25,00 | Não | Sim | `circuito_exclusivo` |

### Exemplo de preparação dos dados em Python

Trecho apresentado no trabalho, que pressupõe a presença do arquivo CSV correspondente:

```python
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeClassifier
from sklearn.metrics import accuracy_score, confusion_matrix

dados = pd.read_csv('dataset_circuitos_residenciais.csv')
dados['corrente_calculada'] = dados.potencia_w / dados.tensao_v

X = dados[['corrente_a', 'ponto_de_luz', 'uso_exclusivo']]
y = dados['classe']

X_treino, X_teste, y_treino, y_teste = train_test_split(
    X, y, test_size=0.25, random_state=42, stratify=y
)
print(len(X_treino), len(X_teste))  # 27 treino, 9 teste
```

O rótulo `y` não entra no conjunto de atributos `X`, pois isso revelaria ao modelo a resposta correta. A divisão estratificada preserva as três classes no treino e no teste.

## 5. Treinamento e avaliação

A classificação é realizada por uma árvore de decisão do **scikit-learn** com profundidade máxima de três níveis:

```python
modelo = DecisionTreeClassifier(max_depth=3, random_state=42)
modelo.fit(X_treino, y_treino)

previsoes = modelo.predict(X_teste)
classes = ['iluminacao', 'tomadas_gerais', 'circuito_exclusivo']
matriz = confusion_matrix(y_teste, previsoes, labels=classes)

print('Acurácia:', f'{accuracy_score(y_teste, previsoes):.1%}')
print(pd.DataFrame(matriz, index=classes, columns=classes))
```

Na execução documentada (`random_state=42`), foram obtidos **100% de acurácia em nove exemplos de teste**, com três acertos em cada classe e nenhum erro:

| Classe real / prevista | Iluminação | Tomadas gerais | Exclusivo |
|---|---:|---:|---:|
| Iluminação | 3 | 0 | 0 |
| Tomadas gerais | 0 | 3 | 0 |
| Exclusivo | 0 | 0 | 3 |

O resultado é esperado em uma base **pequena, sintética e com atributos diretamente relacionados às categorias**. Portanto, **não comprova** generalização para instalações reais nem capacidade de prevenir acidentes. O notebook complementar inclui visualizações da matriz de confusão e da árvore de decisão.

## 6. Base de regras e motor de inferência

A recomendação final é produzida por oito regras didáticas inspiradas nas exigências da NBR 5410. As regras consideram a classe prevista, a indicação de área molhada, a corrente do equipamento e sua identificação.

| Regra | Condição | Orientação |
|:---:|---|---|
| **R1** | Iluminação em área **não molhada** | Indicar circuito de iluminação e avaliar seção de cobre a partir de 1,5 mm². |
| **R2** | Iluminação em área **molhada** | Indicar circuito de iluminação, com avaliação das medidas de proteção do local. |
| **R3** | Tomadas gerais em área **não molhada** | Indicar circuito de tomadas, a partir de 2,5 mm² de cobre como referência mínima. |
| **R4** | Tomadas gerais em área **molhada** | Indicar circuito apropriado ao setor e verificar DR de alta sensibilidade (IΔn ≤ 0,03 A / 30 mA), quando exigido. |
| **R5** | Uso exclusivo em área **não molhada** | Indicar circuito independente e dimensionamento específico. |
| **R6** | Uso exclusivo em área **molhada** | Indicar circuito independente, verificar DR de até 30 mA e demais proteções adequadas. |
| **R7** | Ponto individual destinado a equipamento com corrente nominal **superior a 10 A** | Exigir circuito independente (NBR 5410, item 9.5.3.1). |
| **R8** | Chuveiro ou aquecedor elétrico de água | Indicar conexão direta, sem tomada (NBR 5410, item 9.5.2.3). |

### Implementação resumida das regras

O relatório apresenta o seguinte trecho simplificado; o notebook complementar contém uma versão mais completa, com validação, mensagens e avisos:

```python
def aplicar_regras(classe, area_molhada, corrente_a, equipamento):
    if classe == 'iluminacao':
        regra = 'R2' if area_molhada else 'R1'
    elif classe == 'tomadas_gerais':
        regra = 'R4' if area_molhada else 'R3'
    else:
        regra = 'R6' if area_molhada else 'R5'

    extras = []
    if classe == 'circuito_exclusivo' and corrente_a > 10:
        extras.append('R7: ponto individual acima de 10 A')
    if equipamento.lower() == 'chuveiro':
        extras.append('R8: ligação direta, sem tomada')

    return regra, extras
```

## 7. Consultas de exemplo

Em cada consulta, o usuário informa **potência**, **tensão**, **se é ponto de iluminação**, **se o equipamento é de uso exclusivo** e **se a área é molhada**. O sistema calcula a corrente, prevê a classe e aplica as regras.

```python
def corrente(potencia_w, tensao_v):
    if potencia_w <= 0 or tensao_v <= 0:
        raise ValueError('Potência e tensão devem ser positivas.')
    return potencia_w / tensao_v

# Exemplo: 5500 W / 220 V = 25,00 A
# A previsão é obtida por modelo.predict(novo_caso).
# A orientação final é obtida por aplicar_regras(...).
```

| Novo caso | Cálculo | Classe prevista | Regras | Recomendação |
|---|---|---|---|---|
| Luz do quarto | `160 / 220 = 0,73 A` | `iluminacao` | R1 | Orientar circuito de iluminação; 1,5 mm² de cobre é seção mínima, não escolha final. |
| Tomadas da cozinha | `1600 / 220 = 7,27 A` | `tomadas_gerais` | R4 | Orientar circuito de tomadas destinado à cozinha/serviço; avaliar DR ≤ 30 mA. |
| Chuveiro do banheiro | `5500 / 220 = 25,00 A` | `circuito_exclusivo` | R6, R7, R8 | Circuito exclusivo, ligação direta e proteções aplicáveis; dimensionamento por profissional. |

Se somente a condição **área molhada** for alterada no exemplo das tomadas, a classificação do modelo permanece a mesma, pois essa variável não está nos atributos `X`. No entanto, a **orientação muda de R3 para R4**, mostrando a integração entre aprendizado supervisionado e regras explícitas.

## 8. Entrega e materiais do projeto

O material documenta:

- O problema, o público, os atributos, os rótulos e as regras técnicas;
- Uma base CSV com **36 exemplos fictícios**;
- Treinamento e teste de uma árvore de decisão, com acurácia e matriz de confusão;
- Aplicação das regras R1–R6 e de verificações complementares R7–R8;
- Três casos de consulta, com corrente, classe, regras e justificativa.

**Notebook no Google Colab:** [Abrir notebook do projeto](https://colab.research.google.com/drive/1Kc7NWuZ0ELbgLbLmnz_ktn6iBo-GScb0#scrollTo=abykzCkt2rPJ)

**Base de dados:** `dataset_circuitos_residenciais.csv` (mencionado no relatório; é um arquivo complementar que deverá ser adicionado ao repositório para executar os exemplos de treinamento).

> [!NOTE]
> Este `README.md` documenta o conteúdo do relatório original. Os trechos de Python são exemplos extraídos do material; eles **não constituem, sozinhos, uma aplicação completa e executável**. O CSV e o notebook são materiais complementares.

## 9. Análise crítica e limitações

- Os **100% de acurácia** correspondem a apenas nove exemplos de teste de uma base artificial; são necessários dados reais, casos limítrofes e validação independente.
- A conta `P / V` reproduz as condições dos exemplos. Equipamentos com fator de potência diferente de 1, partida de motores, sistemas trifásicos ou previsão de demanda exigem outras análises.
- A ferramenta **não define automaticamente** a seção final dos cabos, quantidade de condutores, disjuntor, aterramento, DR/DPS, capacidade de interrupção, queda de tensão ou padrão de entrada.
- A divisão de circuitos por cômodo depende de quantidades mínimas de tomadas, previsão de potência em VA, percursos, condições de instalação e requisitos da NBR 5410.
- Uma aplicação voltada a usuários deve alertar quando a consulta estiver fora da faixa de treinamento e encaminhar decisões construtivas a **eletricista qualificado ou projetista habilitado**.

## Referências

1. [Neoenergia Brasília — Normas técnicas e padrões de entrada](https://www.neoenergia.com/web/brasilia/sua-casa/normas-tecnicas). Acesso indicado no documento: 16 nov. 2026.
2. [Neoenergia — DIS-NOR-030, revisão 07](https://www.neoenergia.com/documents/d/brasilia/dis-nor-030-rev07?download=true). *Fornecimento de energia elétrica em tensão secundária de distribuição a edificações individuais*. Aprovada em 17 abr. 2026.
3. **ABNT NBR 5410 — Instalações elétricas de baixa tensão.** Consultar edição e atualizações aplicáveis, em especial os itens 9.5.2.3 e 9.5.3.
4. [Ministério de Minas e Energia — Guia de eficiência energética em edifícios públicos](https://www.gov.br/mme/pt-br/centrais-de-conteudo/publicacoes/eficiencia-energetica/guia-de-eficiencia-energetica-em-edificios-publicos.pdf/@@download/file).
5. [MEC / Rede e-Tec Brasil — Instalações elétricas](https://redeetec.mec.gov.br/images/stories/pdf/eixo_infra/tec_edific/inst_eletr/161012_inst_eletr.pdf).
6. [ANEEL — Procedimentos de Distribuição (PRODIST)](https://www.gov.br/aneel/pt-br/centrais-de-conteudos/procedimentos-regulatorios/prodist), em complemento à Resolução Normativa nº 1.000/2021.
7. [Scikit-learn — Documentação](https://scikit-learn.org/stable/): `DecisionTreeClassifier`, `train_test_split` e `confusion_matrix`.
8. [Eletroproj — Bitola de fio: tabela de fios e amperagem](https://eletroproj.com.br/bitola-de-fio-tabela-amperagem-e-aplicacoes/).
9. [ChatGPT — Ajuda com o arquivo Markdown e criação do codigo via Google Colab] (https://chatgpt.com/)

---
