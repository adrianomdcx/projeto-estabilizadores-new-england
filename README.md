# CGERI: projeto de PSSs para o sistema New England

Este repositório reúne os arquivos do trabalho de CGERI sobre o projeto de estabilizadores de sistemas de potência (PSSs) para o sistema New England modificado. O estudo parte do caso sem estabilizadores e acompanha a inclusão dos PSSs nas máquinas, usando análise modal, resíduos e respostas em frequência para orientar os ajustes.

O trabalho foi desenvolvido com ANAREDE, ANATEM e PacDyn. O [relatório completo](docs/relatorio.pdf), com 61 páginas, apresenta a metodologia, os parâmetros dos controladores e a comparação das respostas no domínio do tempo para o caso base, sete PSSs e nove PSSs.

## Por onde começar

Para conhecer o estudo, comece pelo [relatório](docs/relatorio.pdf). Para explorar os casos, o projeto salvo está em [pacdyn/neweng.pac](pacdyn/neweng.pac). Os arquivos de entrada e os resultados ficam junto dele, dentro de `pacdyn/`.

```text
CGERI/
├── README.md
├── docs/
│   └── relatorio.pdf
└── pacdyn/
    ├── neweng.pac
    ├── neweng.sav
    ├── neweng.blt
    ├── neweng.cdu
    ├── neweng.lst
    ├── neweng.stb e suas variantes
    ├── pacdyn.stp
    ├── PSSs/
    └── Case#01, Case#05, ..., Case#17/
```

## O que tem em cada arquivo

| Arquivo ou pasta | Para que serve |
| --- | --- |
| [docs/relatorio.pdf](docs/relatorio.pdf) | Relatório do trabalho, com a fundamentação, o projeto dos PSSs, os gráficos e as conclusões. |
| [pacdyn/neweng.pac](pacdyn/neweng.pac) | Projeto salvo do PacDyn, usado para organizar as análises do estudo. |
| [pacdyn/neweng.sav](pacdyn/neweng.sav) | Histórico do ANAREDE com o ponto de operação da rede. Os arquivos `.stb` restauram o caso 01 desse histórico. |
| [pacdyn/neweng.blt](pacdyn/neweng.blt) | Dados dos modelos de geradores e das curvas de saturação. |
| [pacdyn/neweng.cdu](pacdyn/neweng.cdu) | Modelos dos reguladores automáticos de tensão das máquinas. |
| [pacdyn/neweng.lst](pacdyn/neweng.lst) | Dados gráficos do diagrama da rede, como posições dos componentes, linhas e legendas. |
| `pacdyn/neweng*.stb` | Arquivos de entrada dos casos dinâmicos. Reúnem as associações dos modelos, os controladores carregados, o evento e as variáveis de saída. |
| [pacdyn/PSSs/](pacdyn/PSSs/) | Modelos CDU dos estabilizadores das barras 30 a 38. O arquivo da barra 34 se chama `barra34.cdu`; os demais seguem o nome `PSS<número da barra>.cdu`. |
| [pacdyn/pacdyn.stp](pacdyn/pacdyn.stp) | Configuração auxiliar com os nomes dos arquivos de saída usados pelo PacDyn. |
| `pacdyn/Case#*/` | Resultados guardados de cada etapa, incluindo o relatório de execução e os arquivos de gráficos. |

## Como os casos se relacionam

Os números das pastas são os identificadores usados no projeto. Eles não correspondem à quantidade de PSSs. A tabela abaixo ajuda a localizar cada etapa; as barras indicadas são as que têm estabilizadores associados no caso.

| Resultados | Arquivo de entrada | PSSs | Barras com estabilizador |
| --- | --- | ---: | --- |
| [Case#01](pacdyn/Case%2301/) | [neweng.stb](pacdyn/neweng.stb) | 0 | Caso base |
| [Case#05](pacdyn/Case%2305/) | [neweng.4.stb](pacdyn/neweng.4.stb) | 1 | 31 |
| [Case#06](pacdyn/Case%2306/) | [neweng.5.stb](pacdyn/neweng.5.stb) | 2 | 31, 38 |
| [Case#07](pacdyn/Case%2307/) | [neweng.6.stb](pacdyn/neweng.6.stb) | 3 | 31, 33, 38 |
| [Case#08](pacdyn/Case%2308/) | [neweng.7.stb](pacdyn/neweng.7.stb) | 4 | 31, 33, 37, 38 |
| [Case#09](pacdyn/Case%2309/) | [neweng.8.stb](pacdyn/neweng.8.stb) | 5 | 31, 33, 36, 37, 38 |
| [Case#10](pacdyn/Case%2310/) | [neweng.9.stb](pacdyn/neweng.9.stb) | 6 | 31, 33, 35, 36, 37, 38 |
| [Case#12](pacdyn/Case%2312/) | [neweng.11.stb](pacdyn/neweng.11.stb) | 7 | 31, 32, 33, 35, 36, 37, 38 |
| [Case#16](pacdyn/Case%2316/) | [neweng.14.stb](pacdyn/neweng.14.stb) | 8 | 31, 32, 33, 34, 35, 36, 37, 38 |
| [Case#17](pacdyn/Case%2317/) | [neweng.15.stb](pacdyn/neweng.15.stb) | 9 | 30, 31, 32, 33, 34, 35, 36, 37, 38 |

Dentro dessas pastas, `printout.out` é o relatório em texto da execução. Os arquivos `.plt` guardam resultados para abrir nas ferramentas de gráficos do CEPEL:

| Nome | Conteúdo |
| --- | --- |
| `eigen.plt` | Autovalores da análise modal. |
| `freq.plt` | Respostas em frequência. |
| `resid.plt` | Resíduos. |
| `mdshp.plt` | Mode shapes. |
| `prtfct.plt` | Fatores de participação. |
| `NLtime.plt` | Respostas da simulação no domínio do tempo. |
| `gep.plt` | Arquivo auxiliar vazio, preservado como estava no `Case#06`. |

Cada pasta contém os resultados que foram guardados naquela etapa. Por exemplo, as respostas temporais estão nos casos base, com sete PSSs e com nove PSSs.

## Para abrir em outro computador

Baixe o repositório inteiro e mantenha a estrutura de `pacdyn/`. Os arquivos `.stb` usam caminhos relativos para `neweng.sav`, `neweng.blt`, `neweng.cdu` e `PSSs/`.

Abra `pacdyn/neweng.pac` no PacDyn. Se o projeto procurar os arquivos no diretório antigo, ajuste os caminhos dos casos para a pasta `pacdyn/` da sua cópia. Para trabalhar diretamente com uma entrada, escolha o `.stb` correspondente na tabela e use essa mesma pasta como diretório de trabalho.

Os resultados de execução identificam o PacDyn 9.9.18. ANAREDE e ANATEM são usados nas etapas de fluxo de potência e simulação dinâmica; o CDU Edit pode ser usado para visualizar e editar os controladores. Os programas precisam estar instalados separadamente.

## Autores

Adriano Macena da Costa, Leonardo de Lima Rodrigues e Raquel Grillo.

Trabalho de CGERI, julho de 2026.
