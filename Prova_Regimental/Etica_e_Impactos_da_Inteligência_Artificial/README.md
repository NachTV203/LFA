# Análise ética do projeto: Sistema Especialista para Circuitos Elétricos Residenciais

**Disciplina:** Inteligência Artificial e LFA — Sistemas Especialistas  
**Projeto de referência:** *Aprendizado de Máquina Aplicado à Distribuição de Circuitos Elétricos Residenciais*  
**Integrantes informados no projeto:** 

Nome: Victor Alves Moreira --------------------- RGM: 30159067

Nome: Beatriz Nevis Miranda ------------------- RGM: 37227581

Nome: Paulo André Gemmal Fonseca -------- RGM: 38030144

Nome: Maurício Gabriel Gemmal Fonseca -- RGM: 38031183



**Natureza:** análise acadêmica de um protótipo didático, não de um projeto executivo de instalação elétrica.


## 1. Leitura

### 1.1 Artigo científico — integridade acadêmica

**Referência:** LACERDA JÚNIOR, Francisco Pires de. *Da proibição à governança: uso ético da inteligência artificial generativa na educação superior — uma revisão integrativa (2023–2026).* Revista Foco, v. 19, n. 8, 2026. [Acessar o artigo](https://doi.org/10.54751/revistafoco.v19n8-017).

**Questão de integridade a considerar:** o uso de IA generativa para elaborar ou revisar o trabalho precisa ser **declarado com clareza**. A equipe não deve apresentar conteúdo produzido com apoio de IA como se tivesse sido inteiramente redigido sem esse recurso, nem aceitar cálculos, referências ou interpretações sem conferência. A análise do artigo destaca a importância de autoria, transparência, supervisão humana e regras proporcionais à finalidade educacional.

**Como isso se aplica ao projeto:** informar que o ChatGPT auxiliou na organização e na redação desta análise e distinguir esse apoio da IA implementada no protótipo em Python. Também conferir as regras R1 a R8 com o texto do projeto e, antes de qualquer uso prático, submeter conclusões elétricas a profissional habilitado.

> **Comentário da dupla:** No nosso projeto, declarar o apoio do ChatGPT não reduz a importância do trabalho da equipe. O cuidado ético está em conferir as informações, assumir as decisões tomadas e não confundir a IA usada para redigir o relatório com a árvore de decisão e as regras implementadas no Colab.

### 1.2 Texto da UNESCO — ética da IA e responsabilidade social

**Referência:** UNESCO. Ética da Inteligência Artificial (IA) no Brasil. Atualizado em 28 de maio de 2025. Ler o texto da UNESCO.

Ideia principal: a inteligência artificial pode contribuir para o desenvolvimento sustentável e beneficiar a sociedade, mas isso depende de sua utilização responsável, alinhada a normas, princípios éticos e mecanismos de governança. O texto destaca a necessidade de políticas e cooperação internacional para que o avanço da tecnologia não produza danos. Informa também que a UNESCO aprovou, em novembro de 2021, a Recomendação sobre a Ética da Inteligência Artificial, publicada em português no Brasil em 2022.

Aplicação ao nosso projeto: embora o orientador de circuitos seja educativo, ele trata de informações que podem influenciar decisões ligadas à segurança elétrica. Por isso, sua utilização responsável exige transparência sobre os limites do treinamento, explicação das regras aplicadas e supervisão humana, especialmente em casos de maior risco, como circuitos de chuveiros. Essas medidas concretizam, no contexto do trabalho, a preocupação da UNESCO com tecnologias que beneficiem as pessoas sem colocá-las em risco.

## 2. Análise ética do projeto

### 2.1 Apresentação do sistema e papel da IA

O projeto desenvolve, em Python e com execução no Google Colab, um protótipo educativo para orientar a **classificação e a organização preliminar de circuitos elétricos residenciais**. Seu público são estudantes e moradores que desejam entender a diferença entre circuitos de iluminação, tomadas de uso geral e equipamentos de uso exclusivo. O usuário informa dados como potência (W), tensão (V), identificação de ponto de luz, uso exclusivo e condição de área molhada; a corrente é calculada no caso didático por **I = P/V**. Uma **árvore de decisão supervisionada** classifica o tipo de circuito, e o **motor de inferência**, por meio de regras **SE... ENTÃO... (R1 a R8)**, produz orientações justificadas de segurança. As saídas podem afetar o aprendizado dos usuários e, se forem interpretadas erroneamente como especificações prontas, a segurança de moradores e profissionais. Por isso, o sistema **não substitui o projeto elétrico nem a validação de profissional habilitado**.

**Distinção fundamental:** a classificação em iluminação, tomadas ou circuito exclusivo é uma **previsão do modelo treinado**; já as recomendações sobre área molhada, uso de circuito independente, DR e ligação de chuveiro decorrem de **regras explícitas estabelecidas pela equipe a partir das referências técnicas citadas no projeto**.

### 2.2 Cinco aspectos éticos exigidos na atividade

| Aspecto | Situação concreta e pessoas afetadas | Medida que a equipe adotará |
|---|---|---|
| **Privacidade e dados** | Um morador pode inserir a lista de equipamentos e os cômodos de sua residência. Embora o protótipo use dados técnicos, combinar essas informações com nome ou endereço revelaria detalhes desnecessários sobre a casa. **Afetados:** moradores e usuários. | Solicitar apenas dados técnicos indispensáveis, não pedir nome, CPF ou endereço e evitar armazenar históricos identificáveis. Qualquer coleta adicional deverá ser explicada e justificada. |
| **Viés e equidade** | O treinamento contém apenas **36 exemplos simulados** e adota **220 V** como referência. Uma casa com tensão ou configuração diferente pode receber orientações inadequadas se o modelo for tratado como universal. **Afetados:** estudantes e moradores de instalações distintas das simuladas. | Testar cenários com outras tensões, casos limítrofes e equipamentos variados; sinalizar consultas fora da faixa de treino; não extrapolar conclusões do conjunto sintético. |
| **Transparência** | A precisão de **100% em nove registros de teste simulados** pode levar alguém a acreditar, incorretamente, que o sistema foi validado para instalações reais. **Afetados:** usuários e avaliadores. | Exibir a classe prevista, a corrente calculada, a regra acionada e a justificativa; informar que a base é artificial e que os resultados não comprovam segurança ou conformidade normativa. |
| **Supervisão e responsabilidade** | Para um chuveiro de **5.500 W em 220 V**, o exemplo calcula **25 A** e recomenda circuito exclusivo; um usuário pode tentar escolher cabo e disjuntor só com essa informação. **Afetados:** moradores, instaladores e outras pessoas expostas ao risco elétrico. | Encaminhar dimensionamento e execução a eletricista ou projetista habilitado, mostrar alertas em cargas críticas e permitir corrigir dados e rever a resposta; não fornecer o dimensionamento final como decisão automática. |
| **Impacto social** | Uma orientação incompleta, divulgada como definitiva, pode contribuir para choque elétrico, incêndio ou gasto com instalação inadequada. Por outro lado, a ferramenta pode favorecer o aprendizado inicial. **Afetados:** usuários, famílias e comunidades. | Publicar o protótipo como recurso didático, com limites de uso visíveis, exemplos explicados e bloqueio ou advertência reforçada em situações de risco. Avaliar a compreensão desses avisos em testes com usuários. |

**Análise de aplicabilidade:** todos os cinco aspectos se aplicam. A privacidade demanda atenção mesmo sem nomes nos dados de treinamento, porque as consultas futuras podem revelar características de uma residência. O viés não é demográfico nos registros apresentados; o risco central decorre da **baixa representatividade técnica** dos exemplos artificiais.

### 2.2.1 Comentários sugeridos para discussão em grupo

- **Privacidade e dados:** Não precisamos saber o nome ou o endereço do morador para orientar o tipo de circuito. O grupo pode defender consultas sem cadastro e sem armazenamento de informações sobre a residência.
- **Viés e equidade:** Como o conjunto de treino é pequeno, artificial e baseado em 220 V, uma resposta correta nos exemplos não garante o mesmo resultado em outras instalações. Precisamos discutir testes com 127 V e casos fora da base antes de ampliar o uso.
- **Transparência:** Ao apresentar a acurácia de 100%, devemos destacar, na mesma explicação, que ela veio de apenas nove exemplos simulados. Mostrar a corrente calculada e a regra aplicada ajuda a pessoa a entender a recomendação e seus limites.
- **Supervisão e responsabilidade:** Nosso maior risco é alguém usar a recomendação para escolher um cabo ou disjuntor por conta própria. A interface deve orientar a procurar um profissional e não apresentar dimensionamentos finais como se estivessem aprovados.
- **Impacto social:** O benefício principal é tornar os conceitos elétricos mais compreensíveis. Esse benefício só é positivo se os usuários entenderem que o sistema apoia o aprendizado, mas não substitui análise e execução seguras.


### 2.3 Limitação que merece correção e verificação

O documento define na **regra R7** que um ponto destinado a equipamento individual com corrente nominal superior a **10 A** deve ter circuito independente. No entanto, o **trecho resumido de código mostrado no PDF** só acrescenta o alerta R7 quando a classe já foi prevista como `circuito_exclusivo` e a corrente ultrapassa 10 A. A equipe deve verificar a implementação completa no Colab e testar se um equipamento individual acima desse limite recebe o alerta mesmo quando a classificação inicial do modelo for inadequada. Essa checagem é uma medida concreta de segurança e transparência, não uma afirmação de que o código integral tenha sido reprovado.

> **Comentário da dupla:** Esse é um teste importante antes da apresentação: consultar um equipamento individual com corrente acima de 10 A e verificar se o alerta de circuito independente aparece mesmo quando a previsão da árvore estiver incorreta. Se o alerta não aparecer, a regra de segurança precisa ser revista no código completo.


## 3. Debate em sala e reflexão individual

### 3.1 Dilema ético para o debate

**Dilema:** é adequado disponibilizar livremente um orientador de circuitos que demonstra cálculos e recomenda circuitos exclusivos, sabendo que pessoas sem formação podem interpretar as respostas como instruções suficientes para realizar ligações elétricas?

**Alternativa A — permitir todas as consultas com um aviso genérico:** facilita o acesso ao aprendizado, mas o aviso pode passar despercebido e as respostas sobre cargas críticas, como chuveiros, podem ser utilizadas de maneira insegura.

**Alternativa B — manter o acesso educacional e aplicar controles proporcionais ao risco:** conserva as classificações e exemplos, mas exige alertas visíveis, identificação da regra aplicada, indicação das limitações e encaminhamento a profissional habilitado em situações críticas. Reduz a chance de uso indevido, embora torne a interface menos direta.

**Nossa possição:** optar pela **alternativa B**, pois a responsabilidade humana e os controles de uso são mais adequados a uma ferramenta que lida com riscos à segurança física. O artigo de Lacerda Júnior (2026) sustenta a importância de usos de IA justificáveis, verificáveis e acompanhados de governança, em vez de liberação sem critérios.

**Pergunta que pode ser feita quanto ao sistema:** se o sistema classificar de forma incorreta um equipamento de alta corrente, em que ponto a equipe deve impedir uma recomendação automática e exigir revisão humana?

> **Comentário da dupla:** Nossa proposta é manter o sistema acessível para estudo, mas com limites claros quando houver risco elétrico. Um aviso genérico pode não ser suficiente para cargas como o chuveiro. Preferimos que a resposta mostre a regra utilizada e encaminhe o dimensionamento e a execução a um profissional habilitado.


### 3.2 Reflexão individual — texto-base a finalizar depois do debate

> Minha posição inicial é manter o sistema disponível para estudo, mas não liberar suas recomendações como decisões técnicas finais. Considero importante que cada resposta mostre os dados recebidos, a regra aplicada e um aviso quando houver risco elétrico, sendo esse todo o possicionamento da dupla para que o sistema especialista seja uma ajuda para tomada de descisão.

## 4. Declaração de uso de sistemas de IA

### 4.1 IA incorporada ao projeto

O projeto utiliza um **classificador supervisionado do tipo árvore de decisão**, implementado em Python com **scikit-learn**, combinado a um **sistema especialista de regras condicionais (R1 a R8)** para orientar didaticamente a distribuição de circuitos elétricos residenciais. O sistema recebe potência, tensão, características de utilização do ponto, indicação de área molhada e equipamento; calcula a corrente, prevê uma classe e produz uma recomendação justificada. Conforme o PDF do projeto, foram usados **36 registros simulados**, sendo **27 para treinamento e 9 para teste**. A avaliação relatou **100% de acurácia nos nove exemplos testados**, um resultado limitado pela base pequena e artificial. As limitações incluem ausência de validação em instalações reais, simplificações no cálculo de corrente e incapacidade de dimensionar automaticamente cabos, disjuntores e demais proteções. 
### 4.2 IA utilizada na elaboração do trabalho

Foi utilizado o **ChatGPT (OpenAI, GPT-6)** como apoio à **organização e formatação** desta análise ética e do arquivo Markdown. As contribuições incorporadas incluem a estruturação dos cinco aspectos solicitados, exemplos de riscos ligados ao projeto e uma proposta de texto para debate e declaração de uso. O conteúdo foi elaborado a partir do **PDF do projeto**, do **enunciado fornecido** e da **descrição pública das leituras indicadas**.

## 5. Entrega e avaliação — conferência final

## Apêndice A — Base de conhecimento e regras técnicas do projeto

### A.1 Base de conhecimento e funcionamento

O conjunto didático reúne **36 registros fictícios**, com **12 exemplos por classe** (`iluminacao`, `tomadas_gerais` e `circuito_exclusivo`). O modelo recebe **corrente (`corrente_a`)**, indicação de **ponto de luz (`ponto_de_luz`)** e de **uso exclusivo (`uso_exclusivo`)**. A condição de **área molhada** é tratada nas regras, não nos atributos do treinamento. A fórmula **I = P/V** é usada nos exemplos simplificados do projeto; ela não resolve, sozinha, casos com fator de potência diferente de 1 ou outras condições de instalação.

### A.2 Regras do motor de inferência

| Regra | Condição (SE...) | Orientação (ENTÃO...) |
|---|---|---|
| **R1** | Iluminação em área não molhada | Indicar circuito de iluminação e avaliação da seção de cobre a partir do mínimo de referência de **1,5 mm²**. |
| **R2** | Iluminação em área molhada | Indicar circuito de iluminação com avaliação das medidas de proteção exigidas para o local. |
| **R3** | Tomadas gerais em área não molhada | Indicar circuito de tomadas, com seção mínima de referência de **2,5 mm²** em cobre. |
| **R4** | Tomadas gerais em área molhada | Indicar circuito apropriado ao setor e verificar proteção **DR de 30 mA**, quando exigida. |
| **R5** | Equipamento de uso exclusivo em área não molhada | Indicar circuito independente e dimensionamento específico do equipamento. |
| **R6** | Equipamento de uso exclusivo em área molhada | Indicar circuito independente e verificar DR de até **30 mA** e outras proteções aplicáveis. |
| **R7** | Ponto destinado a equipamento individual com corrente nominal **maior que 10 A** | Exigir circuito independente, conforme referência à NBR 5410, item **9.5.3.1**, citada no projeto. |
| **R8** | Chuveiro ou aquecedor elétrico de água | Indicar **ligação direta, sem tomada**, conforme referência à NBR 5410, item **9.5.2.3**, citada no projeto. |

**Observação:** as seções de 1,5 mm² e 2,5 mm² são **mínimos de referência**, e não bitolas finais aprovadas. As proteções e os condutores precisam ser dimensionados com base nas condições reais da instalação.

### A.3 Exemplos apresentados no trabalho original

| Consulta didática | Corrente calculada | Classificação | Regras apontadas |
|---|---:|---|---|
| Luz do quarto: 160 W / 220 V | 0,73 A | Iluminação | R1 |
| Tomadas da cozinha: 1.600 W / 220 V | 7,27 A | Tomadas gerais | R4 |
| Chuveiro do banheiro: 5.500 W / 220 V | 25,00 A | Circuito exclusivo | R6, R7 e R8 |

## Referências

1. LACERDA JÚNIOR, Francisco Pires de. **Da proibição à governança: uso ético da inteligência artificial generativa na educação superior — uma revisão integrativa (2023–2026)**. *Revista Foco*, v. 19, n. 8, 2026. DOI: https://doi.org/10.54751/revistafoco.v19n8-017.
2. UNESCO, **Ética da Inteligência Artificial (IA) no Brasil** - https://www.unesco.org/pt/fieldoffice/brasilia/expertise/artificial-intelligence-brazil
3. INSTITUTO DE ESTUDOS AVANÇADOS DA USP. **O Estado da Arte em Ética na Inteligência Artificial**. Gravação de 9 jun. 2026. https://www.iea.usp.br/midiateca/video/videos-2026/o-estado-da-arte-em-etica-na-inteligencia-artificial/.
4. ABNT. **NBR 5410 — Instalações elétricas de baixa tensão**. Norma mencionada no projeto de referência; conferir a edição aplicável para uso técnico. https://universidadeniltonlins.com.br/wp-content/uploads/2019/04/NBR-5410.pdf
5. SCIKIT-LEARN. **DecisionTreeClassifier**. Documentação: https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeClassifier.html.
