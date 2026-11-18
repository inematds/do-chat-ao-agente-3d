# Do Chat ao Agente 3D

[![Do Chat ao Agente 3D](guia/assets/banner.jpg)](https://inematds.github.io/do-chat-ao-agente-3d/guia/)

**🇧🇷 [Português](README.md) · 🇺🇸 [English](README.en.md) · 🇪🇸 [Español](README.es.md)**

## O que é

Este repositório mostra como o curso "Do chat ao agente" virou uma casa 3D de pedra e madeira, aberta no navegador. Serve para quem cria cursos ou páginas e quer ver um projeto assim por dentro. Você encontra os pedidos feitos às IAs, as respostas, os testes, as revisões, os erros e os números medidos. O curso tem 4 estações, 37 aulas e 23 exercícios. Cada sequência concluída acende um degrau e, com as 4, a porta amarela abre para o terraço. Há também uma versão sem 3D.

- **Entrar na casa:** https://eventos.inema.club/do-chat-ao-agente-3d/
- **Como foi feito, no site:** https://eventos.inema.club/do-chat-ao-agente-3d/processo/

## 📖 Guia

Guia completo: **https://inematds.github.io/do-chat-ao-agente-3d/guia/**

## Quer analisar um curso ou uma página sua?

Cole este pedido em um chat de IA que consiga abrir links, junto com o link ou um arquivo do seu curso. Para a IA alterar arquivos, use o Claude Code ou o Codex na pasta do projeto.

```text
Leia o projeto "Do Chat ao Agente 3D" em https://github.com/inematds/do-chat-ao-agente-3d (comece pelo README e por FALHAS.md) e veja a casa em https://eventos.inema.club/do-chat-ao-agente-3d/.
Use esse projeto só como referência. Depois olhe o meu curso ou a minha página (no link ou no arquivo que eu enviar; se você tiver acesso a uma pasta, nela) e me responda em português simples:
1. O que aqui poderia virar lugares ou etapas, com um sinal claro de "pronto"?
2. O que a pessoa veria mudar quando avança?
3. Vale a pena fazer em 3D, ou uma página comum resolve?
4. Como eu conferiria o resultado em um navegador real antes de aprovar?
Não mude nada ainda. Mostre o plano e espere eu dizer sim.
```

## Como foi construído

Nei, do INEMA, pediu para partir de um evento 3D anterior, a [Imersão Jarvis 3D](https://github.com/inematds/imersao-jarvis-3d), e recriar a casa de pedra e madeira de um conjunto de fotos, com o conteúdo do curso "Do chat ao agente".

- **Codex com GPT-6.2 Astra**, em esforço alto e pela assinatura, gerou imagens, texturas, textos e código em 9 rodadas.
- **Claude Code** escreveu o briefing, os pedidos e os testes, conferiu o resultado em navegador real e devolveu o que não passava.
- **Revisores independentes** usaram o curso como visitante.

### O que foi medido

| Medida | Valor |
|---|---|
| Rodadas do Codex | 9 |
| Tempo somado das rodadas | 8.459 s, cerca de 2 h 21 min, sem contar preparação e revisões. Algumas rodadas correram ao mesmo tempo |
| Equivalente em tabela de API, só do Codex | US$ 26,32, só para comparação. Esse valor não foi pago: o uso real foi pela assinatura |
| Cota semanal do Codex medida | de 89% para 96% |
| Revisores independentes | nota 6 (reprovado), nota 7 (reprovado) e nota 7,5 (aprovado com pontos a ajustar, com orientação mais branda que nas duas primeiras) |

As rodadas são numeradas de 00 a 07, com uma 00b. A última foi conferida no site publicado, com clique e teclado reais, sem novo revisor. Os números por rodada estão em `processo/dados.json`. As notas vêm do acompanhamento do projeto, e os pareceres completos dos revisores não estão publicados: os pontos apontados aparecem nos pedidos das rodadas 05, 06 e 07.

### O que deu errado

A lista completa, com a correção de cada item, está em [FALHAS.md](FALHAS.md). Alguns exemplos:

- O forro saiu vermelho e o piso saiu vinho.
- A pedra pareceu tijolo pintado e, depois, bloco de jogo.
- Uma imagem de teste saiu toda preta, porque a tela era apagada logo depois de desenhada.
- A mureta prendia o clique no vão da porta.
- A barra de avisos anunciava a chegada à estação quando a pessoa ainda estava a caminho.

### Limites

- A fluidez não foi medida em placa de vídeo real nem em celular físico. Os testes usaram renderização por software e emulação.
- Cadeiras, poltrona e pedra vista de perto ainda são simples.
- Não foi medido se a casa faz as pessoas aprenderem ou concluírem mais.
- O curso é grátis, mas os exercícios pedem computador e assinatura do Claude ou do ChatGPT. Alguns usam o terminal.

---

## Instalação técnica

O site é estático, sem etapa de build. Você precisa de Python 3 para servir os arquivos e de um navegador com WebGL para o modo 3D. Sem WebGL, o curso abre na versão sem 3D.

```bash
git clone https://github.com/inematds/do-chat-ao-agente-3d.git
cd do-chat-ao-agente-3d
python3 -m http.server 8792
```

Depois abra `http://localhost:8792/`.

### Arquivos

| Caminho | O que guarda |
|---|---|
| `index.html`, `src/` | O site: interface, casa 3D, controles e progresso |
| `conteudo/base.json` | Aulas, exercícios e vídeos, já prontos |
| `conteudo/curso.json`, `conteudo/roteiro.md` | Textos da casa e percurso |
| `assets/` | Texturas, vista do vale e fontes |
| `vendor/three/` | Three.js, sem CDN |
| `processo/` | Briefing, pedidos, respostas, medidas e capturas das rodadas 2, 4 e 7 |
| `tools/` | Validador, captura em navegador e execução das rodadas |
| `guia/`, `capa/` | Este guia em português, inglês e espanhol, e a capa |

### O que esta cópia pública muda

Este repositório foi montado à parte, com um histórico novo. Ficaram de fora a pasta `fonte/`, as fotos de referência, os registros brutos de execução e as capturas das outras rodadas. Os nomes das fotos ainda aparecem nos pedidos.

Os registros de `processo/` foram saneados: caminhos da máquina, links da página de origem e regras internas foram trocados ou retirados. Por isso, alguns trechos dos pedidos diferem do texto original enviado ao Codex. Em `conteudo/base.json`, saíram os links da página de origem, que o site não usa.

`tools/gerar_base.py` depende de `fonte/` e fica como registro. A base já vem pronta em `conteudo/base.json`.

### Testes

```bash
python3 tools/validar_conteudo.py
for f in src/*.js; do node --check "$f"; done
```

O validador aceita uma lista opcional de termos proibidos em `tools/termos-fora.local.txt`, fora do Git, com uma expressão regular por linha.

`node tools/capturar.mjs <rotulo>` abre o site em Chromium e guarda capturas em `processo/revisoes/`. Ele espera o Playwright em `~/.npm-global` (`npm install -g --prefix ~/.npm-global playwright`, depois `npx playwright install chromium`).

### Custo

`tools/resumir_rodada.py` grava tempo, tokens e custo equivalente de cada rodada em `processo/dados.json`. Ele e `tools/vigia_cota.py` leem os registros locais do Codex. Use `PASTA_CODEX` se eles não estiverem em `~/.codex`.

## O processo, do início ao fim

🧠 é o trabalho de Nei, do INEMA, com o Claude Code. ⚙️ é um script. 🤖 é o Codex ou um revisor independente.

| Passo | O que acontece | Comando | Quem faz |
|---|---|---|---|
| 1 | Reunir a página do curso, as aulas, os exercícios e as fotos sem pessoas | pasta `fonte/`, fora deste repositório | 🧠 sessão com o Nei |
| 2 | Escrever briefing, regras e validador | `processo/BRIEFING.md`, `tools/validar_conteudo.py` | 🧠 sessão com o Nei |
| 3 | Gerar a base do curso | `python3 tools/gerar_base.py` (pede `fonte/`) | ⚙️ script |
| 4 | Criar imagens, texturas e a vista do vale | `tools/rodar_codex.sh processo/prompts/00-ambiente.md <fotos>` e `00b-vista.md` | 🤖 Codex |
| 5 | Escrever os textos do curso | `tools/rodar_codex.sh processo/prompts/01-conteudo.md` | 🤖 Codex |
| 6 | Construir a casa e o curso | `tools/rodar_codex.sh processo/prompts/02-casa.md <fotos>` | 🤖 Codex |
| 7 | Conferir com capturas em navegador real | `node tools/capturar.mjs <rotulo>` | 🧠 sessão com o Nei |
| 8 | Aproximar das fotos e dar acabamento, com trava de cota | `tools/vigia_cota.py 96`, `03-fidelidade.md`, `04-acabamento.md` | 🤖 Codex |
| 9 | Revisão independente: nota 6, reprovado | agente novo, sem as notas do autor | 🤖 revisor |
| 10 | Corrigir o que a revisão apontou | `tools/rodar_codex.sh processo/prompts/05-revisao.md` | 🤖 Codex |
| 11 | Segunda revisão: nota 7, reprovado | agente novo | 🤖 revisor |
| 12 | Corrigir de novo | `tools/rodar_codex.sh processo/prompts/06-revisao2.md` | 🤖 Codex |
| 13 | Terceira revisão: nota 7,5, aprovado | agente novo, com orientação mais branda | 🤖 revisor |
| 14 | Fechamento | `tools/rodar_codex.sh processo/prompts/07-fechamento.md` | 🤖 Codex |
| 15 | Conferir a última rodada com clique e teclado reais | navegador + `node tools/capturar.mjs r7` | 🧠 sessão com o Nei |
| 16 | Validar | `python3 tools/validar_conteudo.py` e `node --check` em `src/*.js` | ⚙️ script |
| 17 | Publicar o site, com o OK do Nei | script de publicação, fora deste repositório | 🧠 sessão com o Nei |
| 18 | Montar esta cópia pública, saneada, e escrever o guia | branch `publico`, `guia/`, `inema-traduz` | 🧠 sessão com o Nei |
