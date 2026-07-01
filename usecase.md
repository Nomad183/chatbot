```mermaid
flowchart LR
    %% Aktor
    User((Masyarakat))
    Bot((Sistem Chatbot))

    %% Batasan Sistem
    subgraph Sistem_Chatbot [Sistem Chatbot Layanan Informasi BKPSDM]
        direction TB
        UC1([UC-01: Greeting & Menerima Pesan])
        UC2([UC-02: Anti-Spam / Rate Limiter])
        UC3([UC-03: Normalisasi Pertanyaan])
        UC4([UC-04: Quick Response / Data Statis])
        UC5([UC-05: Advanced Query / RAG Gemini])
        UC6([UC-06: Memberikan Respons API])
        UC7([UC-07: Logging & Auto-Learning])
    end

    %% Interaksi Aktor Utama
    User -->|Kirim WhatsApp| UC1
    UC6 -->|Balasan WhatsApp| User

    %% Interaksi Aktor Sistem
    Bot --> UC3
    Bot --> UC4
    Bot --> UC5
    Bot --> UC7

    %% Alur dan Relasi Antar Use Case
    UC1 -. "<< include >>" .-> UC2
    UC1 --> UC3
    UC3 --> UC4
    UC4 -. "<< extend >>\n(Jika kemiripan < 75%)" .-> UC5
    UC4 -->|Jika kemiripan > 75%| UC6
    UC5 --> UC6
    UC6 -. "<< include >>" .-> UC7
