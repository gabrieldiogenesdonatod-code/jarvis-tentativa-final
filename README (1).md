# J.A.R.V.I.S — Deploy no Streamlit Community Cloud

## O que mudou em relação à sua versão V8 (Tkinter)

Tkinter é uma interface de **computador local** — ela nunca funcionaria
num servidor como o `share.streamlit.io`, então o app foi reescrito do
zero em Streamlit, mantendo o máximo possível do comportamento original:

| Recurso            | Versão V8 (Tkinter)         | Versão Streamlit (nuvem)                  |
|---------------------|------------------------------|--------------------------------------------|
| Cérebro (IA)        | OmniRoute (`localhost`)      | Pollinations AI (gratuita, sem chave)      |
| Voz (falar)         | pyttsx3 (alto-falante do PC) | gTTS (áudio tocado no navegador)           |
| Microfone           | SoundCard (placa de som do PC)| `st.audio_input` (mic do navegador)       |
| Abrir site/pesquisa | Abria o navegador do PC      | Mostra um link clicável no chat            |
| Comandos de PC (calculadora, bloco de notas etc.) | Funcionavam | **Removidos** — não fazem sentido num servidor |
| Memória             | `memoria.json` local          | `memoria.json` no servidor (temporário — ver aviso abaixo) |

⚠️ **Aviso sobre a memória:** o armazenamento do Streamlit Cloud é
temporário. Enquanto o app estiver rodando ela fica salva normalmente,
mas um redeploy ou reinício do app pode apagar o `memoria.json`. Se
quiser algo 100% permanente, me avise depois — dá pra ligar num banco
de dados gratuito (ex: Supabase, Google Sheets) sem muita dor de cabeça.

## Passo a passo para publicar

1. **Crie um repositório no GitHub** (pode ser público ou privado) e
   suba estes 3 arquivos nele:
   - `app.py`
   - `requirements.txt`
   - este `README.md` (opcional)

2. **Acesse** https://share.streamlit.io e faça login com sua conta
   GitHub.

3. Clique em **"New app"**, escolha o repositório, a branch (geralmente
   `main`) e defina o caminho do arquivo principal como `app.py`.

4. Clique em **"Deploy"**. Em alguns minutos o Streamlit instala as
   dependências do `requirements.txt` e o app fica online, com uma URL
   tipo `https://seu-app.streamlit.app`.

5. Pronto — esse link funciona em qualquer navegador, celular ou PC,
   sem precisar instalar nada.

## Testando localmente antes de publicar (opcional)

Se quiser testar no seu PC antes de subir pro GitHub:

```bash
pip install -r requirements.txt
streamlit run app.py
```

Isso abre o app em `http://localhost:8501` no seu navegador.
