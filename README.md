# Segundo cérebro: Linux para infraestrutura

Notebook de estudo feito no Gemini Notebook (antigo NotebookLM), que responde somente com base nas fontes que eu selecionei e mostra de onde tirou cada resposta.

**Link do notebook compartilhado:** https://notebook.google.com/notebook/aad5f85c-95d2-4713-a289-d5ec750d2c7b

## Tema e objetivo

> Quero um especialista em Linux para infraestrutura que me explique, em linguagem simples, comandos, permissões, serviços e logs, para aplicar no meu dia a dia do trainee e montar meu portfólio de estudo.

## Fontes que entraram e por que confio nelas

| # | Fonte | Formato | Por que confio |
|---|---|---|---|
| 1 | Ubuntu Server documentation | Site | Documentação oficial do Ubuntu, com tutorial, guias práticos e referência |
| 2 | Guia Foca GNU/Linux | Site, em português | Guia clássico em português, dividido em iniciante, intermediário e avançado |
| 3 | Introduction to Linux (LFS101), Linux Foundation | Curso escrito | Curso gratuito da própria Linux Foundation |
| 4 | Introduction to Linux, curso completo para iniciantes (canal freeCodeCamp) | Vídeo | Feito com apoio da Linux Foundation |
| 5 | Como usar Systemctl para gerenciar serviços e unidades do systemd (DigitalOcean) | Artigo | Tutorial em português, com exemplos de comandos |
| 6 | Como usar o Journalctl para visualizar e manipular registros do systemd (DigitalOcean) | Artigo | Tutorial em português, com exemplos de comandos |

### Como escolhi as fontes

As quatro primeiras foram escolhidas por mim, antes de abrir a ferramenta. As duas da DigitalOcean vieram do Deep Research, que encontrou dezenas de páginas (print em `prints/02-deep-research.png`). Importei só as que passaram nestes critérios: quem escreve, se está atualizado, se abre sem login e se não tem dado pessoal.

Recusei, por exemplo:

- Capítulos repetidos do Guia Foca, porque o guia já era uma fonte.
- Arquivo do Scribd, enviado por usuário, sem autoria confiável.
- Documentos da Red Hat e da ArchWiki sobre boot, contêineres e outros assuntos fora do meu tema.

Também removi os dois relatórios que o próprio Deep Research gerou. Eles eram texto escrito pela IA, não fontes externas.

Painel final de fontes: `prints/01-fontes-notebook.png`.

## Diretriz de comportamento

```
Comporte-se como um especialista em Linux para infraestrutura, que ensina uma iniciante.

- Responda somente com base nas fontes do notebook. Se a resposta não estiver nelas, diga que não encontrou, em vez de inventar.
- Explique em português simples, um passo por vez.
- Quando mostrar um comando, explique o que faz cada parte e qual resultado esperar.
- Prefira comandos simples, sem one-liners complexos.
- Só mencione o editor vi/vim quando a pergunta envolver editar um arquivo.
- No fim de cada resposta, indique de qual fonte veio a informação.
```

Print da configuração: `prints/03-diretriz-chat.png`.

**Ajustes que fiz:**

- Na primeira tentativa, colei a diretriz no campo de resumo do notebook, e o chat não a seguiu. Corrigi colocando na configuração do chat.
- A linha do `vi` gerava dicas sobre edição de arquivos que não vinham das fontes. Troquei por uma condição.

## Perguntas, respostas e fontes

### Pergunta de teste: o comando `ls`

**Pergunta:** O comando `ls` é um dos utilitários essenciais do Linux. O que faz e quais opções são mais usadas?

**Resposta (resumo):** Lista arquivos e diretórios. As opções mais usadas são `-a` (inclui ocultos), `-l` (formato longo), `-i` (inode), `-L` (segue links simbólicos) e `-S` (ordena por tamanho).

**Fontes:** as citações numeradas aparecem no print. Esta pergunta foi feita antes de configurar a diretriz do chat.

Print: `prints/04-ls-citacoes.png`

### Pergunta 1: permissões de arquivos

**Pergunta:** Como funcionam as permissões de arquivos no Linux? Explique rwx e o chmod com exemplos simples.

**Resposta (resumo):** Explicou r, w e x e as três categorias (dono, grupo e outros). Mostrou a soma numérica (4, 2, 1) e dois exemplos: `chmod 755 meu_script.sh` e `chmod u+x,g-w meu_script.sh`, cada parte explicada com o resultado esperado. Avisou que as fontes não cobrem SUID, SGID, Sticky Bit nem umask.

**Fonte citada:** Introduction to Linux, curso completo para iniciantes (freeCodeCamp / Linux Foundation).

Print: `prints/05-permissoes.png`

### Pergunta 2: serviços com systemctl

**Pergunta:** Como listar, iniciar, parar e ver o status de um serviço com systemctl?

**Resposta (resumo):** Mostrou `systemctl list-units --type=service`, `systemctl status`, `sudo systemctl start` e `sudo systemctl stop`, cada um com explicação e resultado esperado. Avisou que não encontrou nas fontes como definir um tempo limite para um `stop` travado.

**Fonte citada:** Como usar Systemctl para gerenciar serviços e unidades do systemd (DigitalOcean).

Print: `prints/06-systemctl.png`

### Pergunta 3: logs de um serviço com journalctl

**Pergunta:** Como usar o journalctl para ver os logs de um serviço específico?

**Resposta (resumo):** Mostrou `journalctl -u`, com `--since today` (por período), `-f` (tempo real) e `-b` (desde o último boot). Avisou que não encontrou nas fontes como encaminhar os logs para um servidor syslog remoto.

**Fonte citada:** Como usar o Journalctl para visualizar e manipular registros do systemd (DigitalOcean).

Print: `prints/07-journalctl.png` (versão depois de corrigir a diretriz, sem a dica do `vi`).

### Pergunta 4: /var/log e journal do systemd

**Pergunta:** Qual a diferença entre os arquivos de log em /var/log e o journal do systemd?

**Resposta (resumo):** `/var/log` guarda arquivos de texto, um por serviço, lidos com `tail` e `less`. O journal guarda os registros em formato binário, lidos com `journalctl`, e permite filtrar por serviço, tempo e nível. Avisou que as fontes não comparam o desempenho de leitura e escrita em disco.

**Fontes citadas:** os dois artigos da DigitalOcean e o vídeo da freeCodeCamp.

Print: `prints/08-var-log-vs-journal.png`

### Pergunta 5: comparação entre fontes

**Pergunta:** Compare o que o Guia Foca e o curso LFS101 dizem sobre permissões de arquivos.

**Resposta (resumo):** O LFS101 trouxe o conteúdo completo: rwx, soma octal, `chmod`, `chown` e `chgrp`. Sobre o Guia Foca, o notebook disse que o capítulo de permissões não estava carregado, só a página inicial do site.

**Fontes citadas:** LFS101 e Guia Foca.

**O que aprendi:** o notebook não inventou conteúdo que a fonte não tinha. Páginas que são só índice importam pouco texto, então é melhor adicionar a página do capítulo.

Print: `prints/09-comparacao-foca-lfs101.png`

### Citação aberta

Exemplo de como clicar em uma citação e conferir o trecho da fonte: `prints/10-citacao-aberta.png`

## Materiais gerados no Estúdio

- Mapa mental: [mapa-mental.png](materiais/mapa-mental.png)
- Slides (formato detalhado, tamanho padrão): [slides.pdf](materiais/slides.pdf)

O relatório (guia de estudos) não foi gerado por causa do limite de uso da ferramenta.

## Estrutura do repositório

```
segundo-cerebro-linux/
  README.md
  materiais/
    mapa-mental.png
    slides.pdf
  prints/
    01-fontes-notebook.png
    02-deep-research.png
    03-diretriz-chat.png
    04-ls-citacoes.png
    05-permissoes.png
    06-systemctl.png
    07-journalctl.png
    08-var-log-vs-journal.png
    09-comparacao-foca-lfs101.png
    10-citacao-aberta.png
```

## O que aprendi

- Poucas fontes bem escolhidas rendem mais do que muitas sem critério.
- O Deep Research ajuda a achar fontes, mas quem decide o que entra é quem estuda.
- A diretriz precisa ficar no campo certo (configuração do chat) e deve ser revisada olhando as respostas.
- Conferir as citações mostra quando uma fonte não tem o conteúdo esperado.
