# 🧠 Study Content Automation (n8n + IA)

Um pipeline de automação construído com **n8n** que recebe PDFs e vídeos do YouTube via Telegram, extrai conceitos-chave usando IA (Google Gemini), e gera materiais de estudo (Resumos, Flashcards e Mapas Mentais) injetados diretamente no Anki via AnkiConnect.

## 📐 Arquitetura do Sistema

O fluxo principal do motor opera conforme o diagrama abaixo, unificando a entrada de dados (documentos ou vídeos) em um único pipeline de processamento de Inteligência Artificial:

```mermaid
flowchart TD
    A([Entrada: PDF ou Link YouTube]) --> B[Telegram Trigger]
    B --> C{Validação de chat_id autorizado}
    C --> D{É Arquivo ou Link?}
    D -- Arquivo --> E[Nó: Extração de Texto de PDF]
    D -- Link --> F[Nó: HTTP Request - API Transcrição]
    E --> G[Nó: LLM Gemini - Extração de Conceitos]
    F --> G
    G --> H[Notificação: Resumo no Telegram]
    G --> I[Arquivo: Mapa Mental Markdown]
    G --> J[Estrutura: Flashcards JSON]
    J --> K[(AnkiConnect: createDeck e addNote)]
