# Laboratório de Prompt Injection e Defesa em LLMs

Este repositório serve como um laboratório prático para o estudo de vulnerabilidades em Grandes Modelos de Linguagem (LLMs). Através de um Jupyter Notebook, é demonstrado de forma clara como ataques de **Prompt Injection** podem ocorrer e, mais importante, é comprado a eficácia de diferentes técnicas de engenharia de prompt para defesa.

O código utiliza a plataforma [Ollama](https://ollama.com/) para rodar um modelo open-source localmente, permitindo que qualquer pessoa possa replicar os experimentos de forma segura e gratuita.

## 🎯 Cenário do Experimento

O objetivo é testar a robustez de um assistente de IA para uma clínica veterinária, que tem a instrução de responder **apenas** sobre cachorros e gatos. O ataque consiste em uma série de 10 prompts maliciosos que tentam forçar o assistente a quebrar sua regra principal e responder qual é a capital do Brasil.

Comparamos a taxa de falha (sucesso do ataque) em quatro implementações de assistentes, cada uma com um nível de defesa diferente.

## 🔬 Assistentes e Técnicas de Defesa

O notebook implementa e compara quatro assistentes:

1.  **`Dummy` (Linha de Base):** Um assistente com um prompt de sistema simples e direto. Representa uma implementação comum e ingênua, sem defesas explícitas.

2.  **`Sophisticated` (IA Constitucional & Spotlighting):** Esta defesa implementa duas práticas recomendadas:
    * **IA Constitucional:** Define um conjunto de regras explícitas e invioláveis (`<regras>`).
    * **Spotlighting:** Envolve a entrada do usuário em delimitadores (`<entrada_usuario>`) e instrui o modelo a tratar o conteúdo como dados brutos, e não como comandos.

3.  **`Dummy with Reminder` (Reforço no Final):** Uma técnica que explora uma característica da arquitetura dos LLMs. Ao repetir a instrução de sistema original *após* a pergunta do usuário, aproveitamos o **efeito de recência**, garantindo que a diretriz principal seja a última coisa que o modelo "lê" antes de responder.

4.  **`Sophisticated with Reminder` (Defesa em Camadas):** A implementação mais robusta, que combina as duas técnicas anteriores. Ela usa a estrutura da "constituição" e, adicionalmente, reforça essa mesma constituição ao final do prompt do usuário.


## ⚙️ Pré-requisitos

Antes de executar o notebook, garanta que você tenha o seguinte ambiente configurado:

1.  **Python 3.10+**
2.  **Ollama instalado:** Siga as instruções de instalação em [ollama.com](https://ollama.com/).
3.  **Modelo Granite-3B baixado:** Após instalar o Ollama, execute o seguinte comando no seu terminal para baixar o modelo que usamos nos exemplos:
    ```sh
    ollama pull granite3.3:2b
    ```
    *(Nota: Embora o código original use `granite3.3:2b`. Ajuste o nome do modelo no notebook se necessário.)*

## 📊 Resultados Esperados

Ao executar o notebook, você observará uma clara progressão na eficácia das defesas. A taxa de sucesso dos ataques (falhas do assistente) deve diminuir significativamente a cada nível de defesa implementado, seguindo a ordem:

`Dummy` > `Sophisticated` > `Dummy with Reminder` > `Sophisticated with Reminder`

Isso demonstra que, embora não exista uma solução 100% infalível, a aplicação de múltiplas camadas de defesa na engenharia do prompt aumenta drasticamente a resiliência do LLM contra manipulações.

## 📚 Referências e Leitura Adicional

As técnicas e vulnerabilidades demonstradas neste repositório são baseadas em pesquisas e padrões de segurança estabelecidos pela comunidade de IA.

1.  **[OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/)**: A principal referência da indústria para segurança em IA. O **Prompt Injection (LLM01)** é listado como a vulnerabilidade número um.
2.  **[Constitutional AI (Anthropic)](https://www.anthropic.com/news/claudes-constitution)**: A abordagem da Anthropic de criar um conjunto de regras explícitas para guiar o comportamento do modelo, que inspirou o assistente `Sophisticated`.
3.  **[AI Engineering - Building Applications with Foundation Models (Chip Huyen)](https://www.oreilly.com/library/view/ai-engineering/9781098163423/)**: Livro que menciona a técnica de reforçar instruções ao final do prompt para combater o efeito "Lost in the Middle".

Criado com 🧠 por **Alex Bispo**.
