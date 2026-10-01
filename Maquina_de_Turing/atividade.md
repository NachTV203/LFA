# ATIVIDADE REMOTA — MÁQUINAS DE TURING

**Teoria da Computação**  
*Estudo, simulação e reflexão sobre os limites computacionais*

| Disciplina | Tema | Modalidade | Valor |
| :--- | :--- | :--- | :--- |
| Teoria da Computação | Máquinas de Turing | Remota | 1,0 ponto |

---

## 🎥 Material Obrigatório

**Assista ao vídeo antes de realizar a atividade:**  
[Akitando #86 — O Computador de Turing e Von Neumann: Por que calculadoras não são computadores?]([https://www.youtube.com/watch?v=YOUR_LINK_HERE](https://akitaonrails.com/2020/10/23/akitando-86-o-computador-de-turing-e-von-neumann-por-que-calculadoras-nao-sao-computadores/)) 

> **Orientação:** Assista ao material com atenção e utilize os conceitos apresentados para responder às questões e desenvolver a atividade de simulação.

---

## 1. Objetivos da atividade
Ao final da atividade, o estudante deverá ser capaz de:
* Compreender o conceito de Máquina de Turing.
* Identificar os principais componentes de uma Máquina de Turing.
* Compreender a importância das Máquinas de Turing para a computação.
* Construir e simular uma Máquina de Turing simples.
* Reconhecer que existem problemas que não podem ser resolvidos por algoritmos, compreendendo os limites da computação.

## 2. Conteúdo
* Conceito de Máquina de Turing.
* Fita, cabeça de leitura/escrita e estados.
* Alfabeto e regras de transição.
* Funcionamento de uma Máquina de Turing.
* Simulação computacional.
* Computabilidade e limites computacionais.

---

## 3. Desenvolvimento da atividade

### Etapa 1 — Introdução
*Após assistir ao vídeo e estudar o material disponibilizado, responda às questões abaixo.*

**1. O que é uma Máquina de Turing?**
> Como explicado no vídeo, não é um computador físico, mas sim um modelo matemático abstrato criado por Alan Turing em 1936 para definir o que é computação. Turing por conta da maquina de escrever de sua mãe imaginou uma espécie de "super máquina de escrever" que processa símbolos (como 0 e 1) em uma fita infinita, sendo capaz de ler, apagar e escrever dados com base em configurações predeterminadas. 

**2. Quais são os principais componentes de uma Máquina de Turing?**
> Ela é composta por uma **fita infinita** (que serve ao mesmo tempo como armazenamento de dados e de simbolos), uma **cabeça de leitura/escrita** (que se move para a esquerda ou direita) e um **conjunto finito de estados e regras de transição** (que dizem para a máquina o que fazer dependendo do estado atual e do símbolo que está sendo lido na fita).

**3. Qual é a importância das Máquinas de Turing para a computação?**
> Ela definiu o limite matemático do que um computador pode fazer. Turing venho provar que uma única máquina poderia simular qualquer outra se programa e dados convivessem no mesmo espaço. Essa é a base de todos os computadores modernos da arquitetura de Von Neumann, separando o que é um computador de verdade de uma simples "máquina de calcular gigante".

**4. Qual é a relação entre Máquina de Turing e algoritmo?**
> A Máquina de Turing é, na prática, a definição formal e matemática do que é um algoritmo. Um algoritmo é uma sequência finita de instruções para resolver um problema. Na Máquina de Turing, essa sequência é representada pela tabela de estados e transições. Se um problema possui um algoritmo capaz de resolvê-lo, ele pode ser executado e simulado por uma Máquina de Turing o que pode ser chamado de "Turing Complete".


### Etapa 2 — Simulação
Utilize um software ou simulador de Máquina de Turing indicado pelo professor.

Crie uma máquina capaz de reconhecer palavras da forma: **`0^n1^n`**

**Exemplos aceitos:**
* 01
* 0011
* 000111
* 00001111

**Exemplos rejeitados:**
* 0
* 1
* 001
* 011
* 00111

> **Desafio:** A máquina deverá verificar se existe a mesma quantidade de símbolos **0** e **1**, seguindo a lógica de funcionamento de uma Máquina de Turing.

```yaml

input: '001'
blank: ' '
start state: inicio

table:

  inicio:
    X: R
    0: {write: X, R: procura1}
    Y: R
    ' ': {R: aceita}

  procura1:
    0: R
    X: R
    Y: R
    1: {write: Y, L: volta}
    ' ': {R: rejeita}

  volta:
    [0,1,X,Y]: L
    ' ': {R: inicio}

  aceita:

  rejeita:

```

### Etapa 3 — Registro da simulação
Após executar a máquina, registre as evidências abaixo:

**Registro dos testes:**

| Teste | Entrada | Resultado esperado | Resultado obtido | Estados percorridos |
| :---: | :--- | :--- | :--- | :--- |
| **1** | `0011` | ACEITA | ACEITA (XXYY) | inicio -> procura1 -> volta -> inicio -> procura1 -> volta -> inicio -> ACEITA |
| **2** | `000111` | ACEITA | ACEITA (XXXYYY) | inicio -> procura1 -> volta (repetido 3x) -> inicio -> ACEITA |
| **3** | `00111` | REJEITA | REJEITA (XXYY1) | volta (repetido 2x) -> inicio -> lê 1 e para por falta de regra -> REJEITA |

**Descrição da Máquina de Turing criada:**
> A máquina funciona com a lógica de ida e volta marcando pares. No estado "inicio", ela procura um 0, substitui por "X" e muda para o estado `procura1`, indo para a direita. Ela ignora os outros 0s até achar o primeiro 1, que ela substitui por "Y". Em seguida, entra no estado volta, indo para a esquerda até achar um espaço em branco, reiniciando o ciclo. Se ao final do processo, no estado "inicio", ela ler apenas "X", "Y" e, por fim, um espaço em branco, ela `aceita` pois seria quantidades iguais. Se faltar par para um 0 ou sobrar um 1, ela cai no estado "rejeita" e trava.

**Captura de tela da simulação:**

<img width="1463" height="786" alt="image" src="https://github.com/user-attachments/assets/436772f8-9e0e-4cf8-a92c-0c1d25c076b5" />
<img width="1467" height="783" alt="image" src="https://github.com/user-attachments/assets/5648480b-3961-4ec7-aba4-c1ab83026ac2" />
<img width="1468" height="790" alt="image" src="https://github.com/user-attachments/assets/1fc4c7b4-39af-4a64-bd2b-6663640f3650" />
<img width="1467" height="788" alt="image" src="https://github.com/user-attachments/assets/6668b57a-98d3-47e3-bbd9-1fcaf1ed0f75" />
<img width="1468" height="792" alt="image" src="https://github.com/user-attachments/assets/49ac4c54-0f25-4f80-abea-88bb93e448dd" />
<img width="1468" height="789" alt="image" src="https://github.com/user-attachments/assets/a3682658-7492-49c3-b714-61761d7eb242" />


### Etapa 4 — Reflexão sobre os limites computacionais

**Uma Máquina de Turing consegue resolver qualquer problema? Explique com suas palavras por que existem problemas que não podem ser resolvidos por algoritmos.** 
> Não. Uma Máquina de Turing não consegue resolver todos os problemas. Existem alguns problemas que simplesmente não podem ser resolvidos por algoritmos, porque não existe uma sequência de passos que consiga chegar a uma resposta para todos os casos possíveis.

---

## 4. Entrega
O estudante deverá enviar **um único arquivo** contendo:
- [x] Respostas da Etapa 1;
- [x] Descrição da Máquina de Turing criada;
- [x] Capturas de tela da simulação;
- [x] Resultados dos 3 testes;
- [x] Resposta da reflexão sobre os limites computacionais.

---

## 5. Critérios de avaliação — 1,0 ponto

| Critério | Valor |
| :--- | :--- |
| Compreensão do conceito e importância das Máquinas de Turing | 0,20 |
| Construção/configuração da Máquina de Turing | 0,30 |
| Realização e registro da simulação | 0,20 |
| Interpretação dos resultados | 0,10 |
| Compreensão dos limites computacionais | 0,20 |
| **Total** | **1,00** |

---

## 6. Questão final

**Problema para reflexão:**
Imagine que você recebeu um problema computacional muito complexo. Como saber se ele é apenas difícil de resolver ou se, na verdade, não existe nenhum algoritmo capaz de resolvê-lo para todos os casos?

*Explique utilizando os conceitos estudados sobre **Máquinas de Turing, computabilidade e limites computacionais.***

> Um problema é apenas difícil quando existe uma forma de resolvê-lo, mesmo que demore bastante. Já um problema não computável é aquele que não pode ser resolvido por nenhum algoritmo em todos os casos. Isso mostra que os computadores também têm limites e não conseguem resolver tudo.


---

## 📌 Orientações finais
1. Assista ao vídeo indicado.
2. Estude os conceitos apresentados.
3. Responda às questões propostas.
4. Realize a simulação da Máquina de Turing.
5. Faça os três testes solicitados.
6. Registre os resultados e as evidências da simulação.
7. Responda à reflexão sobre os limites computacionais.
8. Organize o material em um único arquivo.
9. Envie o arquivo conforme as orientações do professor.
