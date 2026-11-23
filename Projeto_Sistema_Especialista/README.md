# Sistema especialista para classificação de spam

Trabalho da disciplina de Inteligência Artificial e LFA, com a Profa. Kadidja Valéria.

Grupo: Davi Vieira Lima, Fernanda Barbosa Ramos, Samuel Azevedo Da Silva e Arthur Borges 40900509.

Google Colab: https://colab.research.google.com/drive/1xH-jnab7s3wwlnoLsnepeWYVOfpTYVJ8?usp=sharing

## Descrição

O sistema serve para ajudar a pessoa a decidir o que fazer com uma mensagem que acabou de chegar.

Ele recebe dois fatos: o texto da mensagem e se o remetente é conhecido. Com isso, responde se é spam ou não, qual regra usou e o que fazer.

## Base de conhecimento e regras

A base tem quatro regras. Cada uma cruza a previsão do modelo com o fato informado pelo usuário, e as duas primeiras cobrem o que o sistema faz quando acha spam.


- R1: SE spam e remetente desconhecido, ENTÃO apagar e denunciar.
- R2: SE spam e remetente conhecido, ENTÃO confirmar por outro canal, porque a conta dele pode estar invadida.
- R3: SE não spam e remetente desconhecido, ENTÃO ler com atenção e não clicar em links.
- R4: SE não spam e remetente conhecido, ENTÃO tratar como mensagem normal.


## Motor de inferência

O motor é a função `aplicar_regras()`. Ela recebe os fatos, percorre a base de conhecimento na ordem e para na primeira regra cujas condições fecham.

## Aprendizado de máquina

A previsão vem de uma árvore de decisão (`DecisionTreeClassifier`, `max_depth=2`) treinada em 50 mensagens escritas pela equipe, 37 para treino e 13 para teste. O `CountVectorizer` transforma as palavras em números para o modelo conseguir ler.

## Como rodar

1. Abra o notebook https://colab.research.google.com/drive/1xH-jnab7s3wwlnoLsnepeWYVOfpTYVJ8?usp=sharing no Google Colab.
2. Execute as células na ordem, em *Ambiente de execução > Executar tudo*.

Bibliotecas usadas: Python, Pandas, scikit-learn e Matplotlib.

