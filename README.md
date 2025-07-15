# Laboratório de Prompt Injection e Defesa em LLMs

Este repositório serve como um laboratório prático e um material de apoio para o estudo de vulnerabilidades em Grandes Modelos de Linguagem (LLMs). Através de um Jupyter Notebook, é demonstrado de forma clara e objetiva como ataques de **Prompt Injection** podem ocorrer e, mais importante, como implementar técnicas de defesa eficazes.

O código utiliza a plataforma [Ollama](https://ollama.com/) para rodar um modelo open-source localmente, permitindo que qualquer pessoa possa replicar os experimentos de forma segura e gratuita.

## 🎯 Conceitos Demonstrados

O notebook explora os seguintes cenários:

1.  **Assistente Vulnerável:** Uma implementação base de um chatbot que, apesar de ter um prompt de sistema bem definido, é vulnerável a ataques.
2.  **Ataque de Hijacking com Tokens Especiais:** Demonstração de como um atacante, conhecendo os tokens de formatação do modelo (`<|end_of_text|>`, etc.), pode injetá-los para sequestrar o objetivo do LLM.
3.  **Ataque Semântico (Falho):** Uma demonstração de que, para este modelo e configuração, um ataque semântico simples (sem tokens especiais) não é eficaz, ressaltando a importância dos tokens na manipulação.
4.  **Defesa 1: Sanitização de Entrada:** Implementação de uma função que remove os tokens especiais da entrada do usuário, neutralizando o ataque de hijacking.
5.  **Defesa 2: Spotlighting (Delimitação):** Implementação de uma abordagem de prompt mais robusta, que cria uma "caixa de segurança" ao redor da entrada do usuário e instrui o modelo a não tratar seu conteúdo como comandos.

## ⚙️ Pré-requisitos

Antes de executar o notebook, garanta que você tenha o seguinte ambiente configurado:

1.  **Python 3.10+**
2.  **Ollama instalado:** Siga as instruções de instalação em [ollama.com](https://ollama.com/).
3.  **Modelo Granite-3B baixado:** Após instalar o Ollama, execute o seguinte comando no seu terminal para baixar o modelo que usamos nos exemplos:
    ```sh
    ollama pull granite-code:3b
    ```
    *(Nota: Embora o código original use `granite3.3:2b`, o `granite-code:3b` é uma alternativa comum e compatível. Ajuste o nome do modelo no notebook se necessário.)*

## 📚 Referências e Leitura Adicional

As técnicas e vulnerabilidades demonstradas neste repositório são baseadas em pesquisas e padrões de segurança estabelecidos pela comunidade de IA.

1.  **[OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/)**: A principal referência da indústria para segurança em IA. O **Prompt Injection (LLM01)** é listado como a vulnerabilidade número um, validando a importância dos experimentos neste notebook.

2.  **[Defending Against Indirect Prompt Injection Attacks With Spotlighting](https://ceur-ws.org/Vol-3920/paper03.pdf)**: Artigo de pesquisa que descreve formalmente a técnica de **Spotlighting** (usando delimitadores e marcações) como uma defesa robusta, explicando o princípio de separar dados de instruções. Esta é a base teórica para a função `chat_assistant_with_spotlighting`.

3.  **[Anthropic's Guide to Prompt Engineering](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/claude-4-best-practices)**: A documentação da Anthropic, embora focada no modelo Claude, oferece excelentes práticas que são universalmente aplicáveis. A recomendação de usar tags XML para separar o prompt é um exemplo prático de Spotlighting.

4.  **[The Sandboxed Mind: Principled Isolation Patterns for Prompt-Injection-Resilient LLM Agents](https://arxiv.org/html/2505.13076v1)**: Um paper que discute padrões de arquitetura de sistema para isolar entradas não confiáveis, tratando a **sanitização de entrada** e o encapsulamento como uma das camadas de defesa fundamentais.

Criado com 🧠 por **Alex Bispo**.

