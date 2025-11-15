# Pacote LaTeX wIbgeTex

Pacote LaTeX para a criação de tabelas seguindo as **Normas de Apresentação Tabular (1993)** da Fundação Instituto Brasileiro de Geografia e Estatística (IBGE) e, por cosequência, do item 5.9 da ABNT NBR 14724.

Este pacote foi desenvolvido para facilitar a criação de tabelas em conformidade com o padrão IBGE, muito utilizado em trabalhos técnicos e acadêmicos no Brasil. Ele automatiza a formatação de legendas, fontes, espaçamentos e fornece comandos auxiliares para notas e símbolos.

## Funcionalidades

* **Formatação Automática:** Aplica automaticamente a fonte sem serifa (`\sffamily\footnotesize` por padrão) e os espaçamentos corretos (`\extrarowheight`, `\arraystretch`) a todos os ambientes de tabela.
* **Legendas Padrão IBGE:** Formata automaticamente as legendas das tabelas com o travessão (ex: **Tabela 1 — Título**).
* **Comandos de Notas:** Fornece os comandos `\wIbgeFonte` e `\wIbgeNota` que alinham perfeitamente os rótulos ("Fonte:", "Nota:", "Fontes:") à esquerda.
* **Sinais Convencionais:** Inclui o comando `\wIbgeSinaisConvencionais{...}` para gerar listas de sinais (ex: `...`, `x`, `-`) e as suas descrições oficiais, tratando automaticamente o singular/plural.
* **Tipos de Coluna:** Define tipos de coluna auxiliares (`L`, `C`, `R` para alinhamento de base; `E`, `M`, `D` para alinhamento de meio).
* **Símbolos:** Fornece comandos para símbolos de intervalo (`\wIbgeVdash`, `\wIbgeDashv`) e configura o `siunitx` para formatar ângulos (`\ang{}`) corretamente dentro das tabelas.

## Como Usar

### 1. Pré-requisitos

Este pacote depende de um conjunto de pacotes LaTeX padrão (como `ctable`, `tabularx`, `longtable`, `siunitx`, `tikz`, `caption`, `xparse`, etc.). O `wIbgeTex.sty` carrega-os automaticamente.

Recomenda-se o uso de uma classe moderna como `memoir` ou `abntex2`.

### 2. Instalação e Carregamento

1.  Coloque o arquivo `wIbgeTex.sty` na pasta raiz do seu projeto.
2.  Carregue o pacote no preâmbulo do seu documento `.tex`:

```latex
\documentclass[...]{memoir}
% ou \documentclass[...]{abntex2}

% Carrega o pacote de tabelas
\usepackage{wIbgeTex}

% Carrega as suas fontes de preferência (O PACOTE NÃO FORÇA FONTES)
\usepackage{XCharter}
\usepackage[condensed]{tgheros}
\usepackage{newpxmath}
```

### 3. Exemplo de Tabela (Modelo 1) 

O pacote utiliza o `ctable` como base para a maioria das tabelas.

```latex
\ctable[
  caption = {Pessoas residentes em domicílios particulares...}, 
  label = tabIbge1,
  width = \linewidth, center, pos = !htb, notespar, nosuper
]
{X R{25mm} R{25mm} R{25mm}} % Definição das colunas
{% notas
  % Usa o comando de fonte do pacote
  \wIbgeFonte{Fundação Instituto Brasileiro de Geografia e Estatística (IBGE)}
}
{ % conteúdo da tabela 
  \FL
  Situação do domicílio & Total & Mulheres & Homens \ML
  ...
  \LL
}
```
### 4. Exemplo de Notas e Sinais (Modelo 14)
O pacote facilita a gestão de múltiplas notas e sinais convencionais.

```latex
\ctable[
  caption = {Total de estabelecimentos, pessoal ocupado...}, 
  label = tabIbge14,
  ...
]
{L{35mm} Y Y Y Y Y }
{% notas 
    % 1. Comando de Fonte
    \wIbgeFonte{Pesquisa Industrial - 1982--1984. ...}
    
    % 2. Comando automático para Sinais
    \wIbgeNota{
      \wIbgeSinaisConvencionais{x, -}
    }
    
    % 3. Ativa a fonte correta para o \tnote
   \wIbgeNoteFont
   
   % 4. Notas específicas (ctable)
   \tnote[(1)]{Em 31.12.1982.}
   \tnote[(2)]{Inclui o valor dos serviços prestados...}
}
{ % conteúdo da tabela
  \FL
    Unidade da Federação & ... & Pessoal ocupado \tmark[(1)] & ... \ML
    Brasil \dotfill & 8\,452 & 448\,932 & 4\,637\,512 & 646\,043 \\
    Rondônia \dotfill & 1 & x & x & x \\
    Amapá \dotfill & - & - & - & - \\
    % ...
    \LL
}
```

## Documentação e Exemplos

Este repositório contém uma documentação completa em PDF (`/doc/wIbgeTex-doc.pdf`), gerada a partir do arquivo `wIbgeTex-doc.tex`.

A pasta `/exemplo/` contém:
* `exemplo-memoir.tex`: Um teste de compilação usando a classe `memoir`.
* `exemplo-abntex2-modelo-trabalho-academico.tex`: Um teste de compilação usando a classe `abntex2`.
* `/exemplo/tabelas/`: Os 15 arquivos `.tex` individuais para cada modelo de tabela do manual.

## Licença

Este projeto é distribuído sob os termos da GNU General Public License v3.0. Veja o arquivo `LICENSE` para mais detalhes.
