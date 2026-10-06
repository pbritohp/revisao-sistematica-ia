# Critérios do Protocolo – Pré-requisitos

> **TEMPLATE – COMO USAR (apague este bloco e todos os blocos "Como preencher" e "Exemplo" depois de preencher)**
>
> 1. Preencha primeiro o plano de pesquisa (`Plano_Trabalho_Template.docx`). Os termos, critérios e perguntas deste protocolo saem dele.
> 2. Substitua todo texto entre `[COLCHETES]`. As seções marcadas como **(padrão)** normalmente podem ficar como estão.
> 3. Os exemplos vêm de uma revisão real sobre **seleção de ferramentas de corte em usinagem com IA**. Servem só de referência de nível de detalhe; não copie os termos.
> 4. Teste as expressões na fonte do levantamento **antes** de congelar o protocolo (veja a checklist da Seção 7). Depois de congelado, este arquivo vira a fonte fixa da execução e não deve mais ser alterado.
> 5. Mantenha o nome do arquivo como `Criterios_Protocolo.md`, pois o `Instructions.md` o referencia por esse nome.

Este arquivo define os elementos **fixos** do protocolo de revisão sistemática. Use-os **exatamente como estão**, sem acréscimos, remoções ou refinamentos. Problemas percebidos devem ser registrados como observação, sem alterar o protocolo (ver `Instructions.md`).

**Tema da revisão:** [TEMA EM UMA FRASE]
**Plano de pesquisa associado:** [NOME DO ARQUIVO DO PLANO]
**Autor(a):** [NOME] | **Orientador(a):** [NOME] | **Versão / data de congelamento:** [vX – AAAA-MM-DD]

---

## 1. Blocos de termos

> **Como preencher**
> - Cada bloco reúne **sinônimos de um mesmo conceito**, ligados por `OR`. Os blocos são combinados entre si por `AND` na Seção 2.
> - Escreva os termos **em inglês** (idioma predominante nas bases). Use aspas para expressões com mais de uma palavra (`"machine learning"`).
> - Não use curingas (`*`, `?`): a fonte do levantamento não os interpreta como na maioria das bases.
> - Evite termos muito genéricos (ex.: `system`, `model`, `optimization` sozinhos), que inflam o número de resultados.
> - Fontes de termos: palavras do título e dos objetivos do plano, palavras-chave de 3 a 5 artigos centrais do tema e termos de tesauros da área.
> - Os blocos A a C são obrigatórios. O bloco D é opcional e serve para marcar o subconjunto mais próximo do seu contexto.

**Bloco A – [Objeto ou problema central]**
```
("[termo 1]" OR "[termo 2]" OR "[termo 3]" OR ...)
```

**Bloco B – [Domínio de aplicação]**
```
([termo 1] OR [termo 2] OR "[termo 3]" OR ...)
```

**Bloco C – [Abordagem ou técnica investigada]**
```
("[termo 1]" OR "[termo 2]" OR "[termo 3]" OR ...)
```

**Bloco D – [Contexto ampliado ou tecnologia complementar] (opcional)**
```
("[termo 1]" OR "[termo 2]" OR ...)
```

> **Exemplo (seleção de ferramentas de corte)**
> - Bloco A – Seleção de ferramenta: `("tool selection" OR "cutting tool selection" OR "tool recommendation" OR "cutter selection" OR "selection of cutting tools")`
> - Bloco B – Usinagem: `(machining OR milling OR turning OR CNC OR "metal cutting")`
> - Bloco C – IA e conhecimento: `("artificial intelligence" OR "machine learning" OR "deep learning" OR "neural network" OR "recommender system" OR "expert system" OR "case-based reasoning" OR "knowledge-based" OR ontology OR fuzzy OR "genetic algorithm" OR "decision support" OR ...)`
> - Bloco D – Indústria 4.0 / CAM / CAPP: `("Industry 4.0" OR "smart manufacturing" OR CAM OR CAPP OR "process planning" OR "digital twin" OR "OPC UA" OR MQTT OR IoT OR ...)`

## 2. Expressões de busca

| Código | Composição | Papel |
|---|---|---|
| E1 | A AND B | Apenas contagem |
| **E2** | **A AND B AND C** | **Expressão principal: única usada no levantamento** |
| E3 | A AND B AND C AND D | Contagem e marcação dos registros de E2 que também aparecem em E3 |

> **Como preencher**
> - A estrutura acima é **(padrão)**. Se você não usar o bloco D, remova a linha E3 e as menções a E3 nas Seções 3 e 6.
> - E1 mostra o tamanho do tema sem a técnica; E2 é o recorte que será avaliado; E3 mostra quanto da literatura já está no seu contexto específico.
> - Calibre E2 para um volume que você consiga triar (como referência, algumas dezenas a poucas centenas de registros). Se vier grande demais, restrinja os termos dos blocos **antes** de congelar o protocolo.

---

## 3. Fontes e parâmetros de execução

### 3.1 Fonte do levantamento (obrigatória)

**OpenAlex**, via API pública (não exige login). É a **única** fonte cujos registros entram no levantamento.

Consulta, em que `<EXPR>` é a expressão sem nenhuma alteração (codificada para URL):
```
https://api.openalex.org/works?filter=title_abstract_keywords.search.exact:<EXPR>,from_publication_date:[AAAA]-01-01,to_publication_date:[AAAA]-12-31,type:article|review|conference-paper,language:en|pt&per_page=200&cursor=*
```
- **Nº de resultados**: valor de `meta.count`.
- **Registros**: percorra todas as páginas com `cursor` (use `meta.next_cursor`) até esgotar os resultados.
- **Resumo**: reconstrua-o a partir de `abstract_inverted_index`.
- **Marcação E3**: execute a mesma consulta com E3 e marque os registros de E2 cujo `id` também aparece nela.

> **Como preencher**
> - Ajuste apenas o período (`from_publication_date` / `to_publication_date`), os tipos (`type:`) e os idiomas (`language:`). Esses valores devem ser **idênticos** aos de CI2 e CI3 (Seção 4).
> - Justifique o ano inicial no plano ou no template da revisão (ex.: surgimento de uma tecnologia, uma revisão anterior que cobre o período até X).
> - Cole a URL no navegador com a sua E2 para confirmar que a consulta funciona e conferir o `meta.count`.
> - Exemplo de período: `from_publication_date:2010-01-01,to_publication_date:2026-12-31`.

### 3.2 Fontes de contagem (opcionais, só número de resultados)

Os registros destas fontes **não** entram no levantamento. Se uma fonte não puder ser acessada, registre "Não acessada" e siga em frente; não a substitua por outra.

| Fonte | Link | Como executar |
|---|---|---|
| Portal de Periódicos CAPES | https://www.periodicos.capes.gov.br | Busca simples com a expressão sem alteração, ano de publicação [AAAA]–[AAAA]. |
| [FONTE DA ÁREA] | [LINK] | [Modo de busca, sintaxe dos campos e filtros de ano. Indique como a expressão deve ser adaptada à sintaxe da base, sem alterar os termos.] |

> **Como preencher**
> - Escolha de 1 a 3 bases relevantes para a sua área e que você consiga acessar (VPN/CAFe da universidade, se necessário). Exemplos: IEEE Xplore (engenharia e computação), ACM Digital Library (computação), PubMed (saúde), Scopus e Web of Science (multidisciplinares).
> - Descreva a sintaxe com precisão suficiente para outra pessoa repetir a busca. Exemplo para o IEEE Xplore: *Command Search; prefixe cada termo com `"All Metadata":` (exemplo: `"All Metadata":"tool selection"`), mantendo parênteses e operadores; anos 2010–2026.*

### 3.3 Deduplicação **(padrão)**
1. Compare pelo DOI normalizado (minúsculas, sem `https://doi.org/`).
2. Na falta de DOI, compare pelo título normalizado (minúsculas, sem acentos nem pontuação) e pelo ano.
3. Duas versões do mesmo trabalho com DOIs diferentes (conferência e periódico, preprint e versão publicada, cópia em repositório) são tratadas na seleção por CE5.

### 3.4 Ordenação e numeração **(padrão)**
Ordene os registros únicos por ano (crescente) e depois por título (ordem alfabética), e numere-os nessa ordem. Se o artigo de avaliação obrigatória anexado tiver sido recuperado, ele fica na sua posição normal, com Origem "levantamento e arquivo anexado". Caso contrário, entra ao final, com Origem "arquivo anexado".

---

## 4. Critérios de inclusão

| Código | Critério |
|---|---|
| CI1 | Trata de **[objeto ou problema central]** em **[domínio]** ([detalhe o que conta como objeto: variantes, componentes, decisões envolvidas]) por meio de **[abordagem]**[, com ou sem a técnica do Bloco C]. |
| CI2 | Artigo de periódico, artigo de revisão ou artigo completo de conferência, revisado por pares. |
| CI3 | Publicado entre [AAAA] e [AAAA], em [idiomas] (confirmar nos metadados). |

> **Como preencher**
> - **CI1 é o critério temático** e o mais importante: deve permitir decidir só pelo resumo se o artigo trata do seu problema. Seja específico sobre o que entra.
> - Decida se CI1 exige a técnica do Bloco C ou se admite abordagens sem ela. Admitir abordagens sem a técnica amplia o retrato do estado da arte; exigi-la deixa a revisão mais focada.
> - CI2 é **(padrão)**. CI3 deve repetir exatamente o período e os idiomas da consulta (Seção 3.1).
>
> **Exemplo de CI1:** *Trata da **seleção ou recomendação de ferramentas de corte** em usinagem (tipo, geometria, dimensão, inserto, classe ou material da ferramenta) por meio de **abordagem computacional**, com ou sem IA.*

## 5. Critérios de exclusão

| Código | Critério |
|---|---|
| CE1 | [Termo do Bloco A] fora do [domínio] ([liste os outros domínios em que o termo aparece]). |
| CE2 | [Objeto adjacente que não é o alvo da revisão]. |
| CE3 | Trabalho de [domínio] **sem [a decisão ou o problema central]**: [liste os casos típicos que aparecem na busca mas não interessam]. |
| CE4 | [Processo, contexto ou tecnologia fora do escopo]. |
| CE5 | Duplicata ou outra versão do mesmo trabalho (mantém-se a versão de periódico; preprints e cópias de repositório são excluídos). |
| CE6 | Não revisado por pares: tese, dissertação, capítulo de livro, resumo de congresso, editorial, preprint ou trabalho retratado. |

> **Como preencher**
> - CE1 a CE4 devem cobrir os **falsos positivos mais frequentes** da sua E2. Para descobri-los, leia os títulos dos primeiros 30 a 50 resultados no teste da Seção 7.
> - Você pode ter menos ou mais critérios temáticos (CE1 a CEn), mas mantenha CE5 e CE6 **(padrão)** como os dois últimos e atualize a ordem de decisão na Seção 6.2.
>
> **Exemplo (seleção de ferramentas de corte)**
> - CE1: "Tool selection" fora da usinagem (software, ferramentas gerenciais, robótica, construção, saúde, entre outros).
> - CE2: Seleção apenas de máquina-ferramenta ou de centro de usinagem.
> - CE3: Trabalho de usinagem **sem decisão de seleção de ferramenta**: só trajetória, só desgaste/monitoramento/vida da ferramenta, só parâmetros de corte, só sequenciamento ou só reconhecimento de features.
> - CE4: Processo-alvo de manufatura aditiva.

---

## 6. Regras de aplicação

### 6.1 Fases **(padrão)**
| Fase | Base | Para quem |
|---|---|---|
| 1 – Triagem | Título, resumo, palavras-chave e metadados do OpenAlex | Todos os registros |
| 2 – Confirmação | Texto completo de **acesso aberto** | Somente os incluídos e os casos em Dúvida da Fase 1, até o limite definido em `Instructions.md` |

- Sem texto completo aberto, a decisão da Fase 1 é mantida e a base fica registrada como "apenas resumo". **A falta de acesso não é motivo de exclusão.**
- O artigo de avaliação obrigatória anexado usa o arquivo como texto completo.

### 6.2 Resultado e regra de decisão **(padrão)**
- Cada critério recebe **Atende**, **Não atende** ou **Indeterminado**.
- **Excluir** quando algum CE for "Atende" ou algum CI for "Não atende". Registre o **primeiro** critério decisivo nesta ordem: CE1 → CE6, depois CI1 → CI3.
- **Incluir** quando todos os CI forem "Atende" e todos os CE forem "Não atende".
- **Dúvida** quando nada for decisivo para excluir e ao menos um critério for "Indeterminado".
- Para registros **excluídos**, basta informar o critério decisivo e um trecho de evidência. O preenchimento de todos os critérios é obrigatório apenas para os incluídos e os casos em Dúvida.

### 6.3 Notas de interpretação (não alteram os critérios)
- [Caso de fronteira 1 e como decidir.]
- [Caso de fronteira 2 e como decidir.]
- [Caso de fronteira 3 e como decidir.]
- As palavras-chave do OpenAlex podem ser geradas automaticamente. Se [o objeto central] aparecer **só** nas palavras-chave, CI1 é "Indeterminado".
- [Se CI1 admitir abordagens sem a técnica do Bloco C: "Como CI1 admite abordagens sem [técnica], um artigo incluído pode não usar [técnica]; nesse caso, QA2 avalia a abordagem efetivamente usada."]

> **Como preencher**
> - Registre aqui os casos que geraram dúvida no teste: combinações de critérios, revisões, trabalhos que tratam do tema só de passagem.
> - As notas **esclarecem** os critérios; não podem criar critérios novos.
>
> **Exemplo (seleção de ferramentas de corte)**
> - A seleção conjunta de máquina **e** ferramenta de corte não é CE2.
> - Trabalhos de trajetória, monitoramento ou planejamento de processo que **também** selecionam a ferramenta, com isso explícito no resumo, atendem CI1.
> - A usinagem de peças obtidas por manufatura aditiva não é CE4.
> - Revisões cujo foco é a seleção de ferramentas atendem CI1. Revisões amplas de IA na usinagem, não.

---

## 7. Checklist antes de congelar o protocolo

> Apague esta seção depois de concluída.

- [ ] Os blocos A, B e C correspondem ao título, ao problema e aos objetivos do plano de pesquisa.
- [ ] E2 foi testada na URL do OpenAlex e o `meta.count` é viável para triagem.
- [ ] Li os títulos dos primeiros 30 a 50 resultados de E2 e os falsos positivos frequentes estão cobertos por CE1 a CE4.
- [ ] Ao menos 3 artigos que considero centrais para o tema aparecem nos resultados de E2 (se não aparecem, revise os termos).
- [ ] O período, os tipos e os idiomas da consulta (3.1) coincidem com CI2 e CI3.
- [ ] A sintaxe de cada fonte de contagem (3.2) está descrita de modo que outra pessoa consiga repetir a busca.
- [ ] Os campos `[COLCHETES]` e os blocos "Como preencher" e "Exemplo" foram removidos.
- [ ] A versão e a data de congelamento foram registradas no topo.
