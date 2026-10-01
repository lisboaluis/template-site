# Instruções do projeto

## Idioma e escrita
- Responder e escrever tudo em português do Brasil, salvo pedido diferente.
- Nunca usar emojis, em nada: respostas, commits, PRs, código, documentação.
- Linguagem natural, direta e simples, como uma pessoa escreveria. Sem tom de marketing, sem formatação enfeitada, sem frases infladas.

## Git / commits / push
- Nunca incluir atribuição ao Claude em mensagens de commit, PR ou push.
- Proibido: linhas `Co-Authored-By: Claude ...`, `Claude-Session: ...`, `Generated with Claude Code`, links `claude.ai/code` ou qualquer menção ao Claude/Anthropic no corpo ou rodapé.
- Mensagens de commit e descrições de PR contêm apenas o conteúdo técnico da mudança.
- Só fazer commit ou push quando pedido.

## Fluxo de trabalho
1. O pedido do cliente fica em `briefing.md`. Ler antes de qualquer coisa.
2. Contexto do produto em `PRODUCT.md`, criado pela skill impeccable (`/impeccable init`) a partir do briefing. Fonte única para público, objetivo, contatos e restrições.
3. Sistema visual em `DESIGN.md`, criado pela impeccable ao definir a direção visual e atualizado ao fim da construção (`/impeccable document`). Toda tela nova segue esse arquivo.
4. Antes de dar uma tela por terminada: revisão com o agente `impeccable-finish-reviewer`, capturas em desktop e celular, e correção do que ele apontar.
5. Pedidos de ajuste do cliente vão para `feedback.md`. Ao aplicar, conferir item por item.

## Regras de conteúdo
- Não inventar depoimentos, preços, números de clientes, prazos ou prêmios. O que não foi informado fica marcado como pendente no `PRODUCT.md` e com espaço reservado na página.
- Sem fotos reais ainda: deixar espaços de imagem claramente marcados, prontos para receber a foto.
- Celular primeiro: a maior parte do público chega pelo celular, vindo de rede social ou indicação.

## Convenções técnicas
- Preferir site estático (HTML, CSS e JS puro) sem etapa de build, publicável em qualquer hospedagem, salvo quando o projeto pedir outra coisa.
- O site publicado fica em `site/`, com repositório git próprio. A raiz do projeto guarda briefing, documentos, marca e rascunhos.
- Ao gerar materiais de marca (logos, impressos, posts), colocar em `brand/` e documentar cada arquivo num `brand/LEIA-ME.md`.

## Mac e Windows
O mesmo projeto é aberto em Mac e em Windows. Tudo que for criado precisa funcionar nos dois.
- No Windows, o Claude tem o Bash (Git Bash) e o PowerShell. Preferir o Bash, para que os mesmos comandos funcionem no Mac e no Windows.
- Quebra de linha LF em todos os arquivos de texto, exceto `.cmd`, `.bat` e `.ps1`, que usam CRLF (ver `.gitattributes` e `.editorconfig`). Arquivo com CRLF quebra scripts no Git Bash e no Mac.
- Scripts não podem depender de caminhos fixos de um sistema (`C:\Program Files`, `/Applications`, `cygpath`): detectar o sistema ou aceitar o caminho por variável de ambiente.
- Evitar diferenças entre ferramentas do Mac (BSD) e do Git Bash (GNU), como `sed -i` e `grep -P`. Para manipular arquivos em script, preferir Python.
- Python: no Mac o comando é `python3`, no Windows costuma ser `python`. Detectar com `command -v python3 || command -v python`.
- Chrome (capturas de tela, PDF): Mac em `/Applications/Google Chrome.app/Contents/MacOS/Google Chrome`, Windows em `C:\Program Files\Google\Chrome\Application\chrome.exe`.
- Nomes de arquivo sem acento, espaço ou caractere especial, e sem diferenciar só por maiúscula/minúscula (o Windows não diferencia).
