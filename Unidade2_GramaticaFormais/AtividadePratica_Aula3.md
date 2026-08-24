# Exercícios Práticos — Gramáticas Formais

<img width="724" height="285" alt="image" src="https://github.com/user-attachments/assets/1d4e3b01-203f-445d-8715-3c720217dd8f" />

## Bloco 1 — G₁: `S → aS | b`

**A)** `S ⇒ aS ⇒ aaS ⇒ aaaS ⇒ aaab`

**B)** Termina quando só restam terminais. Ao aplicar `S → b`, não sobra mais nenhum `S`, então não há mais regra a aplicar.

---

## Bloco 2 — G₂: `S → aSb | ε`

**A)** `S ⇒ aSb ⇒ aaSbb ⇒ aaaSbbb ⇒ aaaεbbb ⇒ aaabbb`

**B)** Não. G₂ gera sempre com número igual de `a`' e `b`'. `aabbb` tem 2 `a`' e 3 `b`, então não pertence à linguagem.

---

## Bloco 3 — `S → aA | A → b`

**Regular (Tipo 3).** Cada produção tem no máximo uma variável, sempre à direita dos terminais — padrão linear à direita típico do Tipo 3.

---

