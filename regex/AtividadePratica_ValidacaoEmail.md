# Atividade Prática - Regex para Validação de E-mail

Construa um programa que:
1. solicite cinco endereços de e-mail;
2. valide cada endereço com uma Regex;
3. armazene separadamente os formatos válidos e inválidos;
4. apresente os dois grupos ao final;
5. explique por que cada entrada inválida foi rejeitada.

### Regex
```
^[A-Za-z0-9._+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$
```

### Código

```python
import re

def validar_email(email):
    """Valida o formato de um e-mail usando Regex"""
    padrao = r"^[A-Za-z0-9._+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$"
    return bool(re.fullmatch(padrao, email))

def explicar_erro(email):
    """Explica por que o e-mail foi considerado inválido"""
    if "@" not in email:
        return "Não possui o símbolo @, que é obrigatório pra separar o usuário do domínio."
    
    partes = email.split("@")
    
    if len(partes) != 2:
        return "Possui mais de um @ ou o @ tá no lugar errado."
    
    usuario, dominio = partes
    
    if usuario == "":
        return "Não tem nada antes do @. Precisa ter o nome do usuário."
    
    if dominio == "":
        return "Não tem nada depois do @. Precisa ter o domínio."
    
    if "." not in dominio:
        return "O domínio não tem extensão (tipo .com ou .br). Falta um ponto e a extensão."
    
    partes_dominio = dominio.rsplit(".", 1)
    extensao = partes_dominio[1]
    
    if len(extensao) < 2:
        return "A extensão tem menos de 2 letras. Precisa ter pelo menos 2 (tipo .com, .br)."
    
    if " " in email:
        return "O e-mail tem espaço, o que não é permitido."
    
    return "O formato não corresponde ao padrão esperado de um e-mail."


# Lista de e-mails pra testar
emails = [
    "maria@gmail.com",
    "joao.silva@udf.edu.br",
    "estudante_01@faculdade.com",
    "pedro.gmail.com",
    "ana@dominio"
]

validos = []
invalidos = []

# Valida cada e-mail
for email in emails:
    if validar_email(email):
        validos.append(email)
    else:
        motivo = explicar_erro(email)
        invalidos.append((email, motivo))

# Mostra os resultados
print("=== E-MAILS VÁLIDOS ===")
if validos:
    for email in validos:
        print(f"  ✅ {email}")
else:
    print("  Nenhum e-mail válido.")

print("\n=== E-MAILS INVÁLIDOS ===")
if invalidos:
    for email, motivo in invalidos:
        print(f"  ❌ {email}")
        print(f"     Motivo: {motivo}")
else:
    print("  Nenhum e-mail inválido.")
```

### Saída do programa

```
=== E-MAILS VÁLIDOS ===
  ✅ maria@gmail.com
  ✅ joao.silva@udf.edu.br
  ✅ estudante_01@faculdade.com

=== E-MAILS INVÁLIDOS ===
  ❌ pedro.gmail.com
     Motivo: Não possui o símbolo @, que é obrigatório pra separar o usuário do domínio.
  ❌ ana@dominio
     Motivo: O domínio não tem extensão (tipo .com ou .br). Falta um ponto e a extensão.
```

### Explicação dos resultados

| E-mail | Resultado | Por quê |
|---|:---:|---|
| maria@gmail.com | ✅ Válido | Tem usuário, @, domínio e extensão .com |
| joao.silva@udf.edu.br | ✅ Válido | Aceita pontos no usuário e domínio com várias partes |
| estudante_01@faculdade.com | ✅ Válido | Aceita sublinhado e números no usuário |
| pedro.gmail.com | ❌ Inválido | Não tem o @. Sem ele, não dá pra separar usuário de domínio |
| ana@dominio | ❌ Inválido | Não tem extensão. Falta o ponto e pelo menos 2 letras depois (tipo .com) |

---

## Desafio

Aprimore a Regex para impedir:
- ponto no início do usuário;
- ponto imediatamente antes de @;
- dois pontos consecutivos;
- hífen no início ou no final de uma parte do domínio.

Em aplicações reais, evite criar uma Regex excessivamente rígida: endereços válidos
podem ter formatos menos comuns

### Regex melhorada

```
^[A-Za-z0-9]([A-Za-z0-9._+-]*[A-Za-z0-9])?@([A-Za-z0-9]([A-Za-z0-9-]*[A-Za-z0-9])?\.)+[A-Za-z]{2,}$
```

### Explicação de cada parte

**Parte do usuário:** `[A-Za-z0-9]([A-Za-z0-9._+-]*[A-Za-z0-9])?`
- `[A-Za-z0-9]` — o primeiro caractere tem que ser letra ou número (impede ponto no início)
- `([A-Za-z0-9._+-]*[A-Za-z0-9])?` — no meio pode ter pontos, sublinhados, etc., mas o último caractere antes do @ tem que ser letra ou número (impede ponto antes do @)
- Como os pontos só podem aparecer no meio e o `*` aceita qualquer sequência, eu precisei de uma verificação extra pra dois pontos seguidos

**Parte do domínio:** `([A-Za-z0-9]([A-Za-z0-9-]*[A-Za-z0-9])?\.)+`
- `[A-Za-z0-9]` — cada parte do domínio começa com letra ou número (impede hífen no início)
- `([A-Za-z0-9-]*[A-Za-z0-9])?` — no meio pode ter hífens, mas termina com letra ou número (impede hífen no final)
- `\.` — ponto separando as partes do domínio
- `+` — pelo menos uma parte de domínio antes da extensão

**Extensão:** `[A-Za-z]{2,}`
- Pelo menos 2 letras no final

**Sobre os dois pontos seguidos:** a Regex acima sozinha não impede `..` no usuário. Pra resolver isso completamente, adicionei uma verificação extra no código com Python, porque fazer isso só com Regex fica muito complicado e difícil de ler.

### Código do desafio

```python
import re

def validar_email_avancado(email):
    """Validação avançada de e-mail"""
    # Regex melhorada
    padrao = r"^[A-Za-z0-9]([A-Za-z0-9._+-]*[A-Za-z0-9])?@([A-Za-z0-9]([A-Za-z0-9-]*[A-Za-z0-9])?\.)+[A-Za-z]{2,}$"
    
    # Verifica dois pontos seguidos no usuário (mais fácil fazer com Python)
    usuario = email.split("@")[0] if "@" in email else ""
    if ".." in usuario:
        return False
    
    return bool(re.fullmatch(padrao, email))


# Casos de teste do desafio
emails_teste = [
    # Devem ser válidos
    ("maria@gmail.com", True),
    ("joao.silva@udf.edu.br", True),
    ("estudante_01@faculdade.com", True),
    ("contato+curso@exemplo.com.br", True),
    
    # Devem ser inválidos - casos básicos
    ("pedro.gmail.com", False),
    ("ana@dominio", False),
    ("@gmail.com", False),
    ("aluno@", False),
    
    # Devem ser inválidos - casos do desafio
    (".maria@gmail.com", False),         # ponto no início
    ("maria.@gmail.com", False),         # ponto antes do @
    ("ma..ria@gmail.com", False),        # dois pontos seguidos
    ("maria@-gmail.com", False),         # hífen no início do domínio
    ("maria@gmail-.com", False),         # hífen no final do domínio
]

print("=== TESTE DA REGEX MELHORADA ===\n")

acertos = 0
for email, esperado in emails_teste:
    resultado = validar_email_avancado(email)
    status = "✅" if resultado == esperado else "❌ FALHOU"
    label = "válido" if resultado else "inválido"
    print(f"  {status} {email} → {label}")
    if resultado == esperado:
        acertos += 1

print(f"\nResultado: {acertos}/{len(emails_teste)} testes passaram.")
```

### Saída do código

```
=== TESTE DA REGEX MELHORADA ===

  ✅ maria@gmail.com → válido
  ✅ joao.silva@udf.edu.br → válido
  ✅ estudante_01@faculdade.com → válido
  ✅ contato+curso@exemplo.com.br → válido
  ✅ pedro.gmail.com → inválido
  ✅ ana@dominio → inválido
  ✅ @gmail.com → inválido
  ✅ aluno@ → inválido
  ✅ .maria@gmail.com → inválido
  ✅ maria.@gmail.com → inválido
  ✅ ma..ria@gmail.com → inválido
  ✅ maria@-gmail.com → inválido
  ✅ maria@gmail-.com → inválido

Resultado: 13/13 testes passaram.
```

### O que aprendi com o desafio

Tentar impedir tudo só com Regex é possível, mas a expressão fica gigante e quase impossível de ler. Por isso fiz a verificação dos dois pontos seguidos com Python mesmo (`".." in usuario`). Também percebi que a Regex cobre a maioria dos casos, mas pra um sistema de verdade tem vários casos estranhos que passam despercebidos se não testar.

