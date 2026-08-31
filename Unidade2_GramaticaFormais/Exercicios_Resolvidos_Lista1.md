# Lista 1 — Linguagens Formais, Alfabeto, Linguagens e Gramáticas

## 1. Alfabeto - Considere: Σ = a, b, c

1. Quantos símbolos existem no alfabeto?
  **3 símbolos**

2. Quais são os símbolos?
   **a, b, c**

3. O símbolo `a` pertence ao alfabeto?
   **Sim, `a ∈ Σ`**

4. O símbolo `d` pertence ao alfabeto?
   **Não, `d ∉ Σ`**

5. Escreva uma palavra formada por símbolos desse alfabeto.
   **`acaba`**

## 2. Palavras sobre um alfabeto - Considere: Σ = 0, 1

Classifique cada sequência como válida ou não válida:

| Sequência | Válida? | Justificativa |
|---|---|---|
| `0101` | Sim | esses os símbolos pertencem a alfabeto |
| `00110` | Sim | esses símbolos pertencem ao alfabeto |
| `012` | Não | 2 não pertence ao alfabeto |
| `111` | Sim | todos os símbolos pertencem a alfabeto |
| `10a` | Não | a pertence ao alfabeto |

## 3. Pertinência de símbolos e palavras - Considere: Σ = 0, 1

Determine se as afirmações são verdadeiras ou falsas:

1. `0 ∈ Σ` = **Verdadeiro**
2. `1 ∈ Σ` = **Verdadeiro**
3. `01 ∈ Σ` = **Falso** (01 é uma palavra, não um símbolo individual)
4. `01 ∈ Σ*` = **Verdadeiro**
5. `2 ∈ Σ` = **Falso**
6. `101 ∈ Σ*` = **Verdadeiro** (todos os símbolos de 101 pertencem a Σ)

## 4. Linguagem - Considere: L = 0, 01, 011, 0111

Determine se cada palavra pertence à linguagem:

1. `0 ∈ L` = **Sim**
2. `01 ∈ L` = **Sim**
3. `0111 ∈ L` = **Sim**
4. `10 ∈ L` = **Não**
5. `111 ∈ L` = **Não**
6. `011 ∈ L` = **Sim**

## 5. Descrevendo uma linguagem por padrão - Considere: L = bⁿ | n ≥ 1

1. Escreva as cinco primeiras palavras: 
   **`b, bb, bbb, bbbb, bbbbb`**

2. Explique o significado de `bⁿ`:
   **Representa n ocorrências seguidas do símbolo `b`.**

3. A palavra `bbbbbb` pertence à linguagem?
   **Sim, pois `bbbbbb = b⁶` e 6 ≥ 1.**

4. A palavra vazia (ε) pertence à linguagem?
   **Não, pois tem a condição de `n ≥ 1`, e ε corresponde a n = 0.**

## 6. Linguagem vazia e palavra vazia

Explique, com suas próprias palavras, a diferença entre L = ∅ e L = {ε}.

∅ é um conjunto que não possui nenhum elemento, a linguagem não tem palavra alguma. {ε} é um conjunto que possui exatamente uma palavra, e essa palavra é a palavra vazia.

1. Qual delas possui uma palavra?
   L = {ε}

2. Qual delas não possui nenhuma palavra?
   L = ∅

3. Qual é o comprimento da palavra ε?
   |ε| = 0

## 7. Estrutura de uma gramática - Considere: G = (S,A,0,1,P,S) com P = S→0A, A→1

Identifique:

1. O conjunto de variáveis.
   **`V = S, A`**

2. O conjunto de terminais.
   **`T = 0, 1`**

3. O conjunto de produções.
   **`P = S→0A, A→1`**

4. O símbolo inicial.
   **`S`**

5. Qual palavra pode ser gerada por essa gramática?
   **`S ⇒ 0A ⇒ 01` → palavra `01`**

## 8. Como ler e aplicar uma produção - Considere: S → 0S

Começando com S:

1. Aplique a regra uma vez.
   **`S ⇒ 0S`**

2. Aplique a regra duas vezes.
   **`0S ⇒ 00S`**

3. Aplique a regra três vezes.
   **`00S ⇒ 000S`**

4. Escreva a sequência completa de derivação.
   **`S ⇒ 0S ⇒ 00S ⇒ 000S`**

## 9. Derivação completa de uma palavra

Utilizando G: { S → aSS → b, gere `aaab` escrevendo todos os passos da derivação.

**`S ⇒ aS ⇒ aaS ⇒ aaaS ⇒ aaab`**

## 10. Identificando palavras geradas por uma gramática - Considere G: { S → 0SS → 1

Determine se cada palavra pode ser gerada (apresentando a derivação quando possível):

1. `1` → **Sim**: `S ⇒ 1`
2. `01` → **Sim**: `S ⇒ 0S ⇒ 01`
3. `001` → **Sim**: `S ⇒ 0S ⇒ 00S ⇒ 001`
4. `0001` → **Sim**: `S ⇒ 0S ⇒ 00S ⇒ 000S ⇒ 0001`
5. `101` → **Não**, pois depois de aplicar `S→1` a derivação encerra e não é possível produzir mais símbolos.
6. `1001` → **Não**, pois a gramática só gera palavras no formato `0...01` (zero ou mais `0`'s seguidos de um único `1` final); `1001` começa com `1` seguido de outros símbolos, o que essa gramática não permite.

---
## Checklist de estudo

- [x] Identificar os símbolos de um alfabeto.
- [x] Diferenciar símbolo de palavra.
- [x] Explicar o que é uma linguagem.
- [x] Verificar se uma palavra pertence a uma linguagem.
- [x] Interpretar Σ*.
- [x] Diferenciar ∅ de ε.
- [x] Interpretar w ∈ L.
- [x] Identificar os componentes de uma gramática.
- [x] Ler uma regra como S→aS.
- [x] Realizar uma derivação passo a passo.
- [x] Identificar quando uma derivação termina.
- [x] Determinar se uma palavra pode ser gerada por uma gramática.

---

## Desafio final - Considere: G: { S → aSS → b

1. A palavra `b` pode ser gerada?
   **Sim: `S ⇒ b`**

2. A palavra `ab` pode ser gerada?
   **Sim: `S ⇒ aS ⇒ ab`**

3. A palavra `aab` pode ser gerada?
   **Sim: `S ⇒ aS ⇒ aaS ⇒ aab`**

4. A palavra `aaab` pode ser gerada?
   **Sim: `S ⇒ aS ⇒ aaS ⇒ aaaS ⇒ aaab`**

5. A palavra `aba` pode ser gerada?
   **Não. A regra `S→b` sempre encerra a derivação (não sobra mais nenhum `S`), então não há como colocar um `a` depois do `b`.**

6. Escreva a derivação completa de `aaaab`.
   **`S ⇒ aS ⇒ aaS ⇒ aaaS ⇒ aaaaS ⇒ aaaab`**

7. Descreva, com suas palavras, o padrão das palavras geradas por essa gramática.
   **A gramática gera a linguagem `L = {aⁿb | n ≥ 0}`: qualquer quantidade de `a`'s (inclusive zero) seguida de exatamente um `b` no final, que é sempre o símbolo que encerra a derivação.**
