#praticar 
## Zero-shot Prompting

Os LLMs hoje treinados em grandes quantidades de dados e sintonizados para seguir instruções são capazes de executar tarefas de tiro zero. Tentamos alguns exemplos de tiro zero na seção anterior. Aqui está um dos exemplos que usamos:

```
Extraia palavras-chave do texto abaixo.   
  
Texto: {texto}   
  
Palavras-chave:
```

Observe que no prompt acima não fornecemos nenhum exemplo ao modelo -- esses são os recursos de Zero-Shot[^1] em ação.

Se você revisar os exemplos da aula anterior, notará que cada prompt é um exemplo de zero-shot learning[^1]. Os prompts foram formulados de maneira que o modelo gerasse a saída desejada sem exemplos anteriores específicos.

Quando o Zero-Shot[^1] não funciona, é recomendável fornecer demonstrações ou exemplos no prompt que levam ao Few-Shot prompt[^2].


Enquanto o Zero-Shot[^1] Learning permite uma ampla generalização, em alguns casos, pode não ser suficientemente preciso para tarefas especializadas ou contextos específicos. Isso ocorre porque o modelo pode não ter exemplos internos diretamente relacionados à tarefa em questão. Em tais cenários, técnicas como Few-Shot Learning[^3] ou Fine-Tuning[^4] podem ser mais apropriadas, pois fornecem ao modelo uma orientação mais clara sobre a tarefa desejada através de exemplos ou dados adicionais.

Exploraremos as limitações e quando aplicar cada técnica nas próximas seções, garantindo que você esteja bem equipado para escolher a melhor abordagem para suas necessidades.

Então, pergunto-lhe: pode pensar em situações onde o Zero-Shot Learning[^1] pode não ser a melhor escolha? Como a precisão e o contexto específico influenciam essa decisão?

---

## Few-Shot Prompting

Embora os LLM's demonstrem recursos notáveis de zero-shot, eles ainda ficam aquém em tarefas mais complexas. O prompt de Few-Shot pode ser usado como uma técnica para permitir o aprendizado no contexto, onde fornecemos demonstrações no prompt para direcionar o modelo para um melhor desempenho. As demonstrações servem de condicionamento para exemplos subsequentes onde gostaríamos que o modelo gerasse uma resposta.

Vamos demonstrar a solicitação de poucos disparos por meio de um exemplo.

  
**Exemplo de Entrada (com exemplos de few-shot):**

```
Eu vou te dar alguns exemplos de como transformar frases no presente simples para o futuro simples. Depois, quero que você faça o mesmo com a frase que eu te der.
  
1. Exemplo: Entrada: Eu corro no parque todos os dias. Saída: Eu correrei no parque todos os dias.

Agora é a sua vez: Entrada: Nós jogamos futebol na escola."
```

**Exemplo de Saída (respondendo ao few-shot):**

```
Saída: Nós jogaremos futebol na escola.
```

Podemos observar que o modelo aprendeu de alguma forma como executar a tarefa fornecendo apenas um exemplo (ou seja, 1-shot). Para tarefas mais difíceis, podemos experimentar aumentar as demonstrações (por exemplo, 3 tiros, 5 tiros, 10 tiros, etc.).

Aqui estão mais algumas dicas sobre demonstrações/exemplares ao fazer poucos disparos:

1. **Variedade nos Exemplos Importa:** Quando você dá exemplos ao GPT-4, não é só se os exemplos estão corretos que conta, mas também se eles mostram diferentes tipos de situações que o modelo pode encontrar. Isso é como mostrar a alguém várias fotos de cachorros de diferentes raças para ensinar o que é um cachorro, ao invés de mostrar só um tipo.
    
2. **O Jeito que Você Apresenta os Exemplos é Importante:** Se você usar uma maneira organizada de mostrar as informações ao modelo, como sempre usar a mesma estrutura ou padrão, isso ajuda o modelo a entender o que você quer. Por exemplo, se você sempre coloca a palavra "Email:" antes de escrever um e-mail, o modelo aprende que após essa palavra vem um e-mail.
    
3. **Usar Rótulos Aleatórios com Inteligência:** Mesmo se você não tiver certeza dos rótulos certos para colocar nos seus exemplos, se você escolher esses rótulos de maneira que mostrem mais ou menos a frequência com que eles realmente acontecem, isso é melhor do que escolher sem nenhum critério. Por exemplo, se na vida real, você sabe que recebe mais e-mails sobre trabalho do que lazer, é melhor você rotular mais exemplos como trabalho mesmo que esteja chutando, do que rotular metade e metade.
    

Exemplo de Entrada (com few-shot):

```
Vou te mostrar alguns títulos de artigos de marketing e as palavras-chave que eles visam. Depois, quero que você crie um título baseado na palavra-chave que eu te fornecer.

1. Exemplo: Palavra-chave: "marketing de conteúdo". Título: "10 Estratégias Inovadoras de Marketing de Conteúdo para 2023".
2. Exemplo: Palavra-chave: "SEO". Título: "Como Dominar o SEO em um Mundo com IA: Dicas Práticas".

Agora é a sua vez: Palavra-chave: "publicidade paga".
```

Neste exemplo de few-shot, o modelo é condicionado a entender que, para cada palavra-chave, é esperado um título de artigo que seja criativo e relevante para o tópico, indo além do simples entendimento das palavras e entrando na criação de conteúdo atraente.

A ideia aqui é escolher exemplos que mostrem ao modelo não apenas a estrutura da tarefa (neste caso, criar títulos), mas também o estilo e tom que são desejados, que pode ser mais difícil de captar sem exemplos específicos.

Considerando as estratégias de marketing digital, o few-shot prompting pode ser particularmente útil para treinar modelos para criar conteúdo que siga um certo tom de voz ou diretrizes de marca, onde exemplos podem ajudar o modelo a captar nuances que não seriam óbvias a partir de uma única instrução. Como você vê a aplicação de few-shot prompts para otimizar a criação de conteúdo em seu trabalho?

No geral, parece que fornecer exemplos é útil para resolver algumas tarefas. Quando a solicitação de Zero-shot e a solicitação de Few-Shot não são suficientes, isso pode significar que tudo o que foi aprendido pelo modelo não é suficiente para se sair bem na tarefa. A partir daqui, é recomendável começar a pensar em ajustar seus modelos ou experimentar técnicas de solicitação mais avançadas. A seguir, falaremos sobre uma das técnicas populares de sugestão, chamada de sugestão em Chain-of-Thought (CoT)[^5] , que ganhou muita popularidade.

---

## **Cadeia de Pensamento (CoT)**

A solicitação de cadeia de pensamento (CoT)[^5] permite recursos de raciocínio complexos por meio de etapas intermediárias de raciocínio. Você pode combiná-lo com prompts de poucos tiros para obter melhores resultados em tarefas mais complexas que exigem raciocínio antes de responder.

Para ilustrar como a Cadeia de Pensamento (CoT) pode ser usada para resolver problemas complexos, vamos criar um exemplo hipotético no contexto do marketing digital. A tarefa será desenvolver uma estratégia para aumentar o engajamento do público em uma nova plataforma de mídia social para uma marca de moda.

### **Exemplo de Entrada com Cadeia de Pensamento (CoT):**

**Tarefa:** Desenvolver uma estratégia para aumentar o engajamento do público em uma nova plataforma de mídia social para uma marca de moda.

**Cadeia de Pensamento:**

1. **Identificar o público-alvo da marca de moda:**
    
    - Quem são os consumidores ideais?
        
    - Quais são seus interesses e comportamentos em mídias sociais?
        
2. **Analisar a nova plataforma de mídia social:**
    
    - Quais são as características únicas desta plataforma?
        
    - Como o público-alvo interage com conteúdo nesta plataforma?
        
3. **Estabelecer objetivos de engajamento:**
    
    - O que significa "engajamento" nesta plataforma? (curtidas, compartilhamentos, comentários)
        
    - Qual é o objetivo específico de engajamento? (aumentar o número de seguidores em 20%, dobrar o número de comentários nas postagens)
        
4. **Propor estratégias de conteúdo:**
    
    - Que tipo de conteúdo ressoa com o público-alvo? (imagens de alta qualidade, vídeos dos bastidores, tutoriais de moda)
        
    - Como a marca pode criar conteúdo que incentive o engajamento?
        
5. **Plano de implementação:**
    
    - Como a marca vai criar e programar este conteúdo?
        
    - Que métricas serão usadas para medir o sucesso?
        
6. **Revisão e ajustes:**
    
    - Como a marca vai revisar o desempenho do conteúdo?
        
    - Que ajustes podem ser feitos para melhorar o engajamento com base nos dados coletados?
        

**Entrada Combinada com CoT:**

Para transformar a descrição da Cadeia de Pensamento (CoT) em um prompt de poucos tiros (few-shot) que pode ser utilizado em um modelo de linguagem, é preciso formatar a entrada para que ela seja interpretada como uma série de passos lógicos que o modelo seguirá para chegar a uma conclusão ou solução. Abaixo está um exemplo de como você pode estruturar essa entrada:

### **Exemplo de Prompt de Poucos Tiros com CoT para Aumentar o Engajamento em Mídia Social:**

**Prompt:**

```
Aqui está uma tarefa para você: Desenvolver uma estratégia para aumentar o engajamento do público em uma nova plataforma de mídia social para uma marca de moda. Para completar esta tarefa, siga a Cadeia de Pensamento abaixo:

1. Identificar o Público-Alvo:"Primeiro, identifique quem é o público-alvo da marca de moda. Quais são seus interesses? Como eles geralmente se comportam em mídias sociais?"
    
2. Analisar a Plataforma: "Agora, analise as características da nova plataforma de mídia social. O que a torna especial? Como o público-alvo poderia interagir com o conteúdo aqui?

1. Estabelecer Objetivos de Engajamento: "Defina o que significa engajamento para esta campanha. Isso inclui curtidas, compartilhamentos, comentários? Quais são os objetivos numéricos?"
    
5. Criar Estratégias de Conteúdo: "Com base na identidade da marca e no comportamento do público-alvo, que tipo de conteúdo você acha que aumentará o engajamento? Pense em formatos e temas."
    
6. Plano de Implementação: "Como você planeja implementar e programar o conteúdo? Quais serão as métricas chave para avaliar o sucesso?"
    
7. Revisão e Ajuste: "Por último, como você revisará o desempenho do conteúdo e que ajustes poderão ser necessários para melhorar os resultados?"
    

Ação do Modelo: "Agora, utilizando a Cadeia de Pensamento fornecida, desenvolva uma estratégia detalhada que aborde cada ponto acima. Por favor, forneça uma resposta estruturada, passo a passo."


```

Esse prompt foi estruturado para guiar o modelo através de um raciocínio sequencial, incentivando a geração de uma resposta detalhada e bem pensada, o que é essencial para tarefas que requerem um nível mais profundo de análise e estratégia, como o marketing digital.

[^1]: Zero-shot learning: é uma abordagem de aprendizado de máquina onde um modelo é treinado para realizar uma tarefa sem exemplos diretos dessa tarefa durante o treinamento, mas com base em conhecimento prévio de tarefas relacionadas.
[^2]: Few-Shot prompt: Few-Shot Prompt é uma técnica de aprendizado de máquina que envolve o uso de exemplos limitados (geralmente apenas alguns) para guiar o modelo na realização de uma tarefa específica. Esses exemplos, ou "prompt", são fornecidos ao modelo como entrada, e o modelo é treinado para extrapolar o padrão dos exemplos para realizar a tarefa desejada. Essa abordagem é útil em cenários onde os dados de treinamento são escassos ou difíceis de obter.
[^3]: Few-Shot Learning: é uma abordagem geral no campo de aprendizado de máquina, onde um modelo é treinado com um número limitado de exemplos por classe, visando a capacidade de generalização para classes não vistas durante o treinamento.
[^4]: ![[Glossário IA#^ef0c7d]]
[^5]: Chain-of-Thought (CoT) é uma técnica de geração de texto que se baseia em gerar continuamente ideias relacionadas a partir de um prompt inicial, resultando em um texto fluido e coerente.

