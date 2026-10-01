# Template de projeto

Ponto de partida para um site novo com o Claude Code, com as skills, os agentes e as instruções já configurados. Saiu do projeto Gema Lisboa (`site-teste`), sem os arquivos daquele cliente.

## O que tem aqui

| Arquivo / pasta | Para que serve |
|---|---|
| `CLAUDE.md` | Instruções que o Claude lê sozinho ao abrir o projeto: idioma, estilo de escrita, regras de commit, fluxo de trabalho, convenções. Edite para ajustar ao projeto. |
| `briefing.md` | Onde você escreve o pedido do cliente. Primeiro arquivo a preencher. |
| `feedback.md` | Vazio. Pedidos de ajuste do cliente, um por linha, para o Claude aplicar e conferir. |
| `.claude/skills/impeccable/` | Skill de design: cria `PRODUCT.md` e `DESIGN.md`, define a direção visual, constrói e revisa telas. |
| `.claude/skills/brandkit/` | Skill para pranchas de identidade visual (logo, cores, aplicações) em imagem. |
| `.claude/agents/` | Agentes que a impeccable usa: revisor final, documentador do design, produtor de imagens e aplicador de edições. |
| `.claude/settings.json` | Hooks: depois de cada edição de tela a impeccable confere o design e, ao fim de cada resposta, faz uma revisão mais completa. |
| `.gitattributes` | Mantém as quebras de linha iguais no Mac e no Windows quando o projeto passa pelo git (o projeto anterior quebrou por causa disso). |
| `.editorconfig` | A mesma regra para o editor, para arquivos salvos no Windows não voltarem com CRLF. |
| `.gitignore` | Ignora arquivos de sistema, o cache da impeccable e o lixo de zip do Mac. |

## Preparar o computador (uma vez)

### Mac
1. Google Chrome.
2. Git: rode `git --version` no Terminal. Se não tiver, o Mac oferece instalar.
3. Claude Code: `curl -fsSL https://claude.ai/install.sh | bash`

### Windows
1. Google Chrome.
2. **Git for Windows** (https://git-scm.com/download/win), com as opções padrão do instalador. Ele traz o Git Bash, que é obrigatório aqui: o Claude Code usa o Git Bash como terminal e para rodar os hooks da impeccable. Sem ele, os hooks caem no PowerShell e falham a cada edição.
3. Claude Code, no PowerShell: `irm https://claude.ai/install.ps1 | iex`
4. Se usar VS Code, instale a extensão "EditorConfig for VS Code".

## Levar o template para o outro computador

O jeito mais seguro é pelo GitHub: subir o template num repositório e clonar no outro computador. O `.gitattributes` acerta as quebras de linha sozinho.

Copiando por pendrive, nuvem ou zip, confira se a pasta `.claude` foi junto. Ela começa com ponto e fica oculta no Mac (`Cmd + Shift + .` no Finder mostra). No Windows ela aparece normalmente.

## Começar um projeto novo

1. Copie a pasta com o nome do projeto (não edite o template direto). Use nome sem acento nem espaço.
   - Mac (Terminal): `cp -R template-projeto nome-do-projeto`
   - Windows (PowerShell): `robocopy template-projeto nome-do-projeto /E`
2. Preencha o `briefing.md`.
3. Abra o terminal na pasta e rode `claude` (no Windows, pode ser PowerShell ou Git Bash).
4. Na primeira vez em cada computador, peça ao Claude: `roda .claude/skills/impeccable/scripts/impeccable context`. Isso baixa o programa da impeccable (precisa de internet) e confirma que ela funciona. Sem esse passo o download acontece no primeiro hook, que tem só 5 segundos e pode não terminar numa conexão lenta.
5. Peça: `/impeccable init`. O Claude lê o briefing, faz algumas perguntas e escreve o `PRODUCT.md`.
6. Peça a construção, por exemplo: `cria a landing page do briefing em site/`. A impeccable propõe direções visuais, você escolhe uma e ela grava o `DESIGN.md` e constrói.
7. No fim, ela passa pelo revisor e registra o design final no `DESIGN.md`.

Se a marca ainda não existe, dá para usar a skill brandkit antes ou depois do passo 6 para montar a prancha de identidade.

## Comandos úteis da impeccable

| Comando | O que faz |
|---|---|
| `/impeccable` | Mostra o menu de opções conforme o estado do projeto |
| `/impeccable init` | Cria ou atualiza o `PRODUCT.md` |
| `/impeccable shape` | Discute e define uma tela antes de construir |
| `/impeccable critique` ou `audit` | Avalia o que já existe (design, acessibilidade, desempenho) |
| `/impeccable polish` | Acabamento final |
| `/impeccable adapt` | Ajuste para celular e outros tamanhos de tela |
| `/impeccable clarify` | Melhora textos de botões, rótulos e mensagens |
| `/impeccable live` | Ajusta elementos direto no navegador, escolhendo entre variações |
| `/impeccable document` | Grava o `DESIGN.md` a partir do que foi construído |
| `/impeccable hooks off` | Desliga a conferência automática depois das edições (`on` liga de novo) |
| `/impeccable doctor` | Verifica se os arquivos da impeccable estão desatualizados |

## Se algo não funcionar

- **Erro `bad interpreter`, `$'\r': command not found` ou `set: -: invalid option`:** algum arquivo de `.claude/` ficou com quebra de linha do Windows. Peça ao Claude para converter os arquivos de `.claude/` para LF, menos o `impeccable.cmd`, que precisa continuar como está.
- **No Windows, erro de hook mencionando PowerShell, `[` ou `sh` não reconhecido:** o Git for Windows não está instalado ou o Claude Code não o encontrou. Instale o Git e abra o Claude de novo. Se o Git estiver num lugar diferente do padrão, aponte o caminho do `bash.exe` no arquivo `C:\Users\<seu usuário>\.claude\settings.json` (crie se não existir):
  ```json
  { "env": { "CLAUDE_CODE_GIT_BASH_PATH": "C:\\Program Files\\Git\\bin\\bash.exe" } }
  ```
- **Antivírus bloqueou o download da impeccable no Windows:** o programa vem de github.com/pbakaus/impeccable e é conferido por hash antes de rodar. Libere o arquivo na quarentena ou baixe pelo link que a mensagem de erro mostra.
- **Hooks não rodam depois de copiar por zip ou pendrive:** os hooks chamam a impeccable com `sh`, então não dependem da permissão de execução. Se mesmo assim falhar, confira se a pasta `.claude` foi copiada inteira.
- Para conferir o estado geral, peça `/impeccable doctor`.
