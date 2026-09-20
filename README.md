* Notas em MD
* Extrair em PDF
* Gerênciador de arquivos a esquerda(bem completo)
* Calendário com agendamento completo
* Suporte a fontes(com ligaduras)
* Poder mudar a cor de certa seção do texto
* Versionamento das notas
* Desing bem bonito, simples e intuitivo
* Escrito em rust
* As notas precisam ser separadas em cofres, assim como é no obsidian para que fique de fácil sincronização
* Pode ser possível criar linkns entre as notas
* Terá suporte também ao mermaid para criar diagramas
* E também terá suporte a criação de notas no estilo do xcalidraw
* As notas também podem ter TODO
* As tabelas das notas podem ter um comportamento parecido com planilhas
* As notas podem suportar tags
* As imagens nas notas ficam diretamente na nota, e não precisa fazer o link para o arquivo
* Temas bonitos e harmônicos
* O app terá a opção de modo leitura e escrita
* Terá contagem de palavras e caracteres
* Terá a opção de colocar senha nas pastas e notas
* Atalhos totalmente configuráveis

1. Busca extremamente poderosa

Além da busca textual normal:

busca por título;
busca por conteúdo;
busca por tags;
busca por links;
busca por data de criação/modificação;
filtros por cofre;
filtros por tipo de conteúdo;
busca com operadores, por exemplo:
tag:rust
tag:programming
created:2026
modified:yesterday
type:note
busca dentro de código;
busca em PDFs/anexos, se posteriormente houver OCR.

Backlinks e grafo de conhecimento

Como você já terá links entre notas, eu adicionaria:

backlinks;
links não resolvidos;
notas órfãs;
grafo de relações;
visualização local do grafo;
aliases para notas.

Por exemplo:

Rust
 ├── Ownership
 ├── Async
 ├── Tokio
 └── MLOps
       └── Docker

E seria interessante poder clicar em uma nota e ver:

“5 notas apontam para esta nota.”

Command Palette

Algo como:

Ctrl + K

abrindo:

> Criar nota
> Abrir cofre
> Exportar PDF
> Inserir tabela
> Inserir Mermaid
> Criar link
> Alternar modo leitura
> Buscar notas
> Criar TODO
> Abrir calendário
> Restaurar versão

Autosave + recuperação

Como o aplicativo será local-first, eu faria:

edição
   ↓
autosave
   ↓
snapshot
   ↓
versionamento

Histórico de versões mais sofisticado

Você já colocou versionamento, mas dá para ir além.

Algo como:

Nota: Rust Async

Version 18
19/09/2026 22:31

Version 17
19/09/2026 21:42

Version 16
18/09/2026 18:20

Ao selecionar duas versões:

Version 16
        ↓
     DIFF
        ↓
Version 18

Templates

Eu colocaria templates desde cedo.

Por exemplo:

# {{title}}

Created: {{date}}

## Objetivo

## Conteúdo

## TODO

- [ ]

## Referências

E templates especializados:

Reunião
Aula
Projeto
Livro
Pessoa
Diário
Tarefa
Pesquisa

Sistema de TODO realmente integrado

Em vez de tratar TODO apenas como Markdown:

- [ ] Estudar Rust

o aplicativo poderia reconhecer isso como uma entidade.

Então seria possível ter:

TODOs

☐ Estudar Rust
☑ Criar API
☐ Implementar sincronização

E no calendário:

19 SET

☐ Estudar Rust
☐ Implementar parser Markdown

A mesma tarefa continuaria existindo dentro da nota.

Isso cria uma ponte interessante entre notas + agenda + tarefas.

Datas e referências temporais

Como você terá calendário, eu adicionaria suporte a coisas como:

[[2026-09-25]]

ou:

@2026-09-25

E eventualmente:

Hoje
Amanhã
Próxima segunda

poderiam ser interpretados pelo aplicativo.

Uma nota poderia ter:

Projeto RaceHub

Deadline: 30/09/2026

e aparecer automaticamente no calendário.

Propriedades/metadados

Eu colocaria um sistema de propriedades no início da arquitetura.

Por exemplo:

---
title: Rust Async
tags:
  - rust
  - programming
status: studying
created: 2026-09-19
updated: 2026-09-19

Tabelas híbridas

Sua ideia de tabelas com comportamento de planilha é particularmente interessante.

Eu faria dois níveis.

Markdown normal:

| Nome | Idade |
|------|------:|
| João | 22 |
| Ana  | 25 |

Mas, quando o usuário clica na tabela:

┌────────┬──────┬─────────┐
│ Nome   │ Idade│ Salário │
├────────┼──────┼─────────┤
│ João   │ 22   │ 5000    │
│ Ana    │ 25   │ 6500    │
└────────┴──────┴─────────┘

poderia ter:

fórmulas;
ordenação;
filtros;
células numéricas;
soma;
média;
porcentagem;
importação CSV;
exportação CSV.

Mas aqui existe uma decisão importante: não tentar transformar Markdown em Excel. Eu manteria as tabelas simples compatíveis com Markdown e adicionaria recursos de planilha apenas quando a tabela explicitamente suportar isso.

12. Imagens embutidas

Sua decisão de não obrigar o usuário a gerenciar arquivos de imagem é boa para UX.

Eu faria:

nota.md

com recursos incorporados, mas manteria internamente algo como:

Vault/
├── Notes/
│   ├── Rust.md
│   └── Python.md
│
├── Assets/
│   └── ...
│
└── .app/

A diferença é que o usuário não precisa saber que Assets existe.

Ele simplesmente arrasta uma imagem para a nota:

[imagem]

e o aplicativo gerencia o armazenamento.

Isso mantém o cofre sincronizável sem poluir a experiência.

Drag & Drop

Eu consideraria obrigatório:

arrastar arquivos;
arrastar imagens;
arrastar notas;
reorganizar pastas;
mover notas entre cofres;
arrastar uma nota para outra para criar link.

Por exemplo:

Rust.md

arrastada para:

Python.md

poderia gerar:

[[Rust]]
14. Split view

Uma funcionalidade que eu considero muito importante para esse tipo de aplicativo:

┌──────────────┬───────────────────────┐
│ Arquivos     │ Rust Async            │
│              │                       │
│ Rust         │ conteúdo...           │
│ Python       │                       │
│ Go           │                       │
│              │                       │
└──────────────┴───────────────────────┘

E permitir:

1 painel
2 painéis
3 painéis

Além de tabs.

15. Modo foco

Além de leitura/escrita:

Edit
Read
Focus

No modo Focus:

sidebar desaparece;
toolbar desaparece;
apenas a nota;
largura confortável;
atalhos continuam funcionando.

Muito útil para escrita.

16. Mermaid + Excalidraw

Eu manteria os dois como conceitos diferentes.

Mermaid:

é diagram-as-code.

Excalidraw é diagram-as-canvas.

Seria interessante permitir inclusive:

Nota
 ├── texto
 ├── Mermaid
 └── Canvas

E salvar tudo de forma vinculada à própria nota.

17. Blocos de código

Eu adicionaria:

syntax highlighting;
copiar código;
linguagem detectada automaticamente;
line numbers;
folding;
seleção de código;
eventualmente execução de código em ambientes controlados.

Por exemplo:

fn main() {
    println!("Hello");
}

Isso seria particularmente importante considerando que seu público provavelmente incluirá desenvolvedores.

18. Plugins

Eu não implementaria um sistema de plugins inicialmente, mas projetaria a arquitetura para permitir plugins posteriormente.

Algo como:

Core
 ├── Markdown
 ├── Storage
 ├── Search
 ├── Versioning
 ├── Graph
 └── Sync

Plugins
 ├── Calendar
 ├── Mermaid
 ├── Excalidraw
 ├── Git
 └── ...

Isso pode ser muito valioso se o projeto crescer.

19. Sincronização

Aqui existe uma decisão arquitetural muito importante.

Eu faria o conceito:

Vault
   ↓
pasta normal do sistema
   ↓
arquivos locais

Ou seja, o cofre deveria ser uma estrutura que o usuário pode sincronizar utilizando:

Syncthing
Dropbox
Google Drive
OneDrive
Git
etc.

sem que seu aplicativo precise necessariamente possuir um serviço próprio de sincronização.

Depois você poderia criar sincronização nativa.

Isso é muito mais simples e mantém o projeto realmente local-first.

20. Criptografia

A sua ideia de senha merece uma distinção importante.

Não faria apenas:

senha → esconder pasta

Eu faria:

senha
  ↓
KDF
  ↓
chave criptográfica
  ↓
conteúdo criptografado

Assim:

senha de nota;
senha de pasta;
cofre criptografado.

E o usuário deveria entender que senha de acesso e criptografia dos dados são coisas diferentes.

Para um aplicativo local-first, isso pode virar uma das funcionalidades mais importantes.

21. Lixeira

Eu adicionaria:

Trash

com:

notas excluídas;
pastas excluídas;
restauração;
exclusão definitiva.

E versionamento + lixeira podem trabalhar juntos.

22. Importação e exportação

Além de PDF:

Importar
├── Markdown
├── HTML
├── TXT
├── CSV
├── JSON
└── ZIP

Exportar
├── Markdown
├── PDF
├── HTML
├── TXT
└── ZIP

Principalmente exportar o cofre inteiro.

O usuário nunca deveria ficar preso ao aplicativo.

Uma arquitetura que eu consideraria

Como você quer Rust, eu pensaria em algo próximo de:

                 ┌───────────────────┐
                 │       UI          │
                 │                   │
                 │ Editor            │
                 │ File Manager      │
                 │ Calendar          │
                 │ Graph             │
                 │ Canvas            │
                 └─────────┬─────────┘
                           │
                    Application Layer
                           │
          ┌────────────────┼────────────────┐
          │                │                │
       Markdown          Notes           Search
          │                │                │
          ├─────────────── Storage ────────┤
          │                │                │
       Versioning        Vault            Tags
          │                │                │
          └────────────────┼────────────────┘
                           │
                       Filesystem

E no Rust você poderia separar algo como:

src/
├── app/
├── editor/
├── markdown/
├── vault/
├── filesystem/
├── search/
├── versioning/
├── calendar/
├── tasks/
├── graph/
├── tables/
├── canvas/
├── export/
├── security/
└── sync/
Uma coisa que eu mudaria no escopo

O conjunto que você descreveu já é enorme.

Na prática, você está propondo:

Obsidian + Notion + VS Code/Typora + Excalidraw + calendário + gerenciador de arquivos + mini-spreadsheet.

Então eu dividiria o projeto em versões.

V0.1 — Core

Rust
Vault
Filesystem
Markdown
Editor
Preview
Links
Tags
Imagens
Busca

V0.2 — Knowledge

Backlinks
Graph
Properties
TODO
Templates
Command Palette

V0.3 — Productivity

Calendar
Scheduling
Tasks
Tables
Split view
Focus mode

V0.4 — Advanced

Versioning
Diff
Mermaid
Excalidraw
PDF
Themes
Fonts

V0.5 — Security/Sync

Encryption
Password-protected vaults
Sync
Conflict resolution
Git

E só depois eu partiria para funcionalidades mais ambiciosas.

A principal decisão que eu tomaria desde o começo, porém, seria esta:

O Markdown/arquivo deve ser a fonte de verdade do sistema.

Ou seja, o aplicativo pode ter banco de dados interno para índice, busca, cache, histórico etc., mas o usuário deve conseguir abrir o cofre e encontrar seus arquivos de forma compreensível.

Isso combina muito bem com a ideia de cofres independentes e fáceis de sincronizar e reduz bastante o risco de criar um sistema proprietário difícil de migrar.
