# Laboratório de Prompt Injection e Defesa em LLMs

Este repositório serve como um laboratório prático e um material de apoio para o estudo de vulnerabilidades em Grandes Modelos de Linguagem (LLMs). Através de um Jupyter Notebook, demonstramos de forma clara e objetiva como ataques de **Prompt Injection** podem ocorrer e, mais importante, como implementar técnicas de defesa eficazes.

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

Criado com 🧠 por **Alex Bispo**.

