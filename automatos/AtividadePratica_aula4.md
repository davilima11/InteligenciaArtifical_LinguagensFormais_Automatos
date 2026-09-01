# Atividade Prática — Construção de Autômato

Construir um Autômato Finito Determinístico (AFD) que reconheça todas as palavras sobre o alfabeto Σ = {0, 1} que terminam com **00**.
---

O autômato é definido pela 5-tupla A = (Q, Σ, δ, q₀, F), onde:

- **Q** = {q0, q1, q2} — conjunto de estados
- **Σ** = {0, 1} — alfabeto
- **q₀** = q0 — estado inicial
- **F** = {q2} — conjunto de estados finais
- **δ** — função de transição definida na Seção 4


## 3. Diagrama

O autômato foi construído no simulador JFLAP:

<img width="957" height="361" alt="image" src="https://github.com/user-attachments/assets/4dd66aa0-faf9-497d-ab57-dface8211d8d" />


## 4. Tabela de Transição

| Estado | Entrada 0 | Entrada 1 |
|--------|-----------|-----------|
| → q0   | q1        | q0        |
| q1     | q2        | q0        |
| * q2   | q2        | q0        |



## 5. Explicação da Lógica

Cada estado representa uma memória sobre o sufixo da palavra lida até o momento:

- **q0** — ainda não há um 0 relevante no final da palavra
- **q1** — a palavra lida termina em exatamente um 0
- **q2** — a palavra termina em 00 (por isso é o estado de aceitação)

As transições seguem essa memória. Em q0, ler 1 mantém a máquina em q0 e ler 0 avança para q1. Em q1, ler outro 0 completa o padrão e move para q2, enquanto ler 1 quebra o padrão e retorna a q0. Em q2, ler outro 0 mantém a máquina em q2 (o sufixo continua sendo ...00) e ler 1 retorna a q0. Como cada estado possui exatamente uma transição para cada símbolo de Σ, o determinismo está garantido.



## 6. Testes 

Os testes abaixo foram no simulador JFLAP (função Multiple Run).

**Teste 1 — palavra "100"** (esperado: aceitar)

q0 —1→ q0 —0→ q1 —0→ q2

Estado final q2 ∈ F → **ACEITA** ✓

**Teste 2 — palavra "101"** (esperado: rejeitar)

q0 —1→ q0 —0→ q1 —1→ q0

Estado final q0 ∉ F → **REJEITA** ✓

**Teste 3 — palavra "1000"** (esperado: aceitar)

q0 —1→ q0 —0→ q1 —0→ q2 —0→ q2

Estado final q2 ∈ F → **ACEITA** ✓

Os testes cobrem um exemplo positivo, um negativo e um que valida a auto-transição de q2 no símbolo 0, evitando o viés de confirmação. A verificação no JFLAP confirmou os resultados: **Accept** para 100 e 1000; **Reject** para 101 e 1001.
