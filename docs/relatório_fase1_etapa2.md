1.	Informe quantos número de árvores foram utilizados no motor NLU.
80

2.	Informa qual o valor de threshold foi utilizado no processo de limiar de confiança
0,60

3.	Coloque o resultado da primeira execução
Entrada: 'Tenho 30 kg de banana para doar'
Intenção: cadastrar_doacao | Confiança: 0.93
Retorno: Intenção 'cadastrar_doacao' identificada com 92.5% de confiança.

4.	Descreva como você poderia fazer para os resultados de testes serem melhores, aumento o grau de confiança dos resultados
Para evoluir o motor de NLU e mitigar problemas com frases ambíguas ou dados escassos, as seguintes estratégias podem ser adotadas:
• Aumento e Diversificação do Dataset: O modelo atual possui pouquíssimas frases por intenção. Adicionar variações linguísticas, sinônimos de alimentos (legumes, proteínas, grãos) e diferentes estruturas sintáticas enriquecerá o aprendizado.
• Pré-processamento de Texto (NLP Avançado): Aplicar técnicas como Stemming ou Lemmatização (reduzir palavras ao seu radical/raiz), remoção de Stop Words irrelevantes (artigos, preposições) e conversão de todo o texto para letras minúsculas para que variações ortográficas não confundam o vetorizador.
• Uso de N-grams Maiores: O parâmetro ngram_range=(1, 2) captura palavras isoladas e pares de palavras. Expandir ou testar combinações específicas ajuda a fixar o contexto de expressões cruciais como "precisa de doação".
• Transição para Embeddings de Palavras (Word2Vec / BERT): Substituir o TF-IDF por representações vetoriais densas baseadas em Transformers (como um modelo BERT em português). Isso permite que o motor compreenda o significado semântico das palavras (ex: entender que "mantimentos" e "comida" possuem forte correlação, mesmo que "mantimentos" não esteja explicitamente na base de treino).


5.	Descreva por que o Random Forest foi o melhor método de Machine Learning para essa fase.
O Random Forest se destaca como o melhor método para a fase atual do projeto pelos seguintes fatores técnicos:
• Resistência ao Overfitting: Como o dataset de treino inicial é muito pequeno, modelos lineares simples ou redes neurais profundas poderiam facilmente memorizar o texto (overfitting). O Random Forest combina múltiplas árvores criadas de forma aleatória, o que gera uma forte generalização e reduz a variância do erro.
• Manipulação de Matrizes Esparsas de Alta Dimensão: O processo de vetorização TF-IDF gera matrizes com muitas colunas (características) e a maioria delas preenchida com zeros. O Random Forest seleciona subconjuntos de variáveis aleatoriamente, lidando muito bem com dados esparsos sem perder desempenho.
• Geração Nativa de Probabilidades: Diferente de algoritmos como o SVM clássico, o Random Forest entrega probabilidades bem distribuídas através do método predict_proba(). Isso torna a métrica de confiança confiável para operar a trava de segurança por threshold configurada no projeto.
