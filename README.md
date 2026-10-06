# Revisão Sistemática da Literatura com IA – Templates

Templates para planejar e executar uma **revisão sistemática da literatura (RSL)** com um assistente de IA (Claude, ChatGPT ou similar). Cada pessoa adapta o tema e os critérios. A IA executa as buscas, faz a triagem dos artigos, avalia a qualidade e extrai as informações, seguindo um protocolo fixo e reprodutível.

O fluxo foi testado com Claude e ChatGPT na disciplina DAS410036 (PosAutomação/UFSC), em uma revisão sobre seleção de ferramentas de corte em usinagem com IA. Esse caso aparece como exemplo dentro dos templates.

---

## Estrutura do repositório

```
.
├── README.md
└── AI_import/                                        ← pacote enviado à IA
    ├── Instructions.md                               ← instruções de execução (prompt)            [opcional editar]
    ├── Criterios_Protocolo.md                        ← termos, buscas, fontes e critérios         [EDITAR]
    ├── Plano_Trabalho_Template.docx                  ← modelo do plano de pesquisa                [EDITAR → exportar PDF]
    ├── Revisa_o_Sistema_tica_template.docx           ← template da RSL que a IA preenche          [não editar]
    ├── aula_2_revisao_sistematica.pdf                ← método de RSL (slides)                     [não editar]
    ├── t10_11-PLANEJAMENTO DA PESQUISA CIENTÍFICA.pdf ← apoio para formular as perguntas          [não editar]
    ├── Como_Classificar_as_Pesquisas_Antonio_Gil.doc ← base para classificar os artigos           [não editar]
    └── Adicionar Arquivos de referencia/             ← seus arquivos de referência                [ADICIONAR]
```

---

## O que alterar (resumo)

| Arquivo | Ação |
|---|---|
| `Plano_Trabalho_Template.docx` | **Editar.** Preencha os campos em amarelo, apague os quadros de orientação e exemplo e exporte em PDF para `Adicionar Arquivos de referencia/`. |
| `Criterios_Protocolo.md` | **Editar.** Preencha os campos `[ENTRE COLCHETES]`: blocos de termos, período, fontes de contagem, CI1, CE1 a CE4 e notas de interpretação. Siga a checklist da Seção 7 e apague as orientações. |
| `Adicionar Arquivos de referencia/` | **Adicionar** o plano em PDF (obrigatório) e os artigos de avaliação obrigatória (opcional). Veja a seção abaixo. |
| `Instructions.md` | **Opcional.** Edite só para adaptar as perguntas de qualidade (QA1 a QA5) ou o limite de textos completos, sempre **antes** da execução. |
| Demais arquivos | **Não alterar.** |

> **Mantenha os nomes** `Criterios_Protocolo.md` e `Instructions.md`, porque um arquivo cita o outro pelo nome.

---

## Arquivos de referência

A pasta `AI_import/Adicionar Arquivos de referencia/` reúne os arquivos **específicos da sua pesquisa**. Ela vem vazia no repositório.

| Arquivo | Obrigatório? | Nome sugerido | Papel na execução |
|---|---|---|---|
| Plano de pesquisa preenchido (PDF) | **Sim** | `Plano_Pesquisa_<SeuNome>.pdf` | Define tema, problema e objetivos. A IA deriva dele a pergunta central e as perguntas adicionais da revisão. |
| Artigo(s) de avaliação obrigatória (PDF) | Não | `Artigo_Obrigatorio_<Autor>_<Ano>.pdf` | Artigo indicado pelo orientador ou considerado central para o tema. A IA o inclui na planilha e o avalia pelo texto completo (seleção, qualidade e extração). **Ele não substitui o levantamento.** |

Orientações:

- **Use PDFs com texto selecionável.** Arquivos escaneados como imagem dificultam a leitura pela IA.
- **Use os prefixos** `Plano_Pesquisa_` e `Artigo_Obrigatorio_`. Eles ajudam a IA a reconhecer o papel de cada arquivo, já que o `Instructions.md` os descreve por função e não por nome.
- **Sem artigo obrigatório?** Deixe só o plano na pasta. O `Instructions.md` já trata esse artigo como "se houver".
- **Prefira um ou dois artigos obrigatórios.** Cada um é lido por inteiro, além do limite de 15 textos completos do levantamento, o que aumenta o tempo de execução.
- **Não coloque aqui artigos para a IA "considerar" na busca.** O levantamento usa somente a busca definida no `Criterios_Protocolo.md`. Artigos extras anexados fora desse papel não entram na revisão. Para conferir se um artigo conhecido é encontrado, use o teste da checklist (Seção 7 do protocolo).
- **Cuidado com dados pessoais e direitos autorais.** O plano contém seus dados de contato e artigos pagos não podem ser redistribuídos. Por isso, o `.gitignore` do repositório já ignora o conteúdo dessa pasta (exceto o `.gitkeep`). Remova essas linhas do `.gitignore` só se quiser versionar seus arquivos em um repositório privado.

---

## Passo a passo

### 1. Prepare os documentos

1. Clone ou faça um fork do repositório.
2. Preencha o **plano de pesquisa** e exporte o PDF para `Adicionar Arquivos de referencia/`.
3. Se houver artigo de avaliação obrigatória, coloque o PDF na mesma pasta.
4. Preencha o **`Criterios_Protocolo.md`** a partir do plano:
   - título e problema → Blocos A e B;
   - abordagem ou técnica → Bloco C;
   - contexto específico → Bloco D (opcional);
   - objetivo geral → CI1.
5. **Teste a expressão E2** colando a URL do OpenAlex (Seção 3.1) no navegador. Confira `meta.count` e veja se os artigos que você já conhece aparecem.
6. Ajuste os termos e os critérios até a busca ficar boa. Então **congele o protocolo**, registrando versão e data no topo do arquivo. Depois disso, não altere mais nada.

### 2. Execute com a IA

1. Abra uma **conversa nova** (ou um Projeto, ou o Cowork) com **acesso à web** e **execução de código** habilitados. A IA precisa consultar a API do OpenAlex e gerar os arquivos .docx e .xlsx.
2. Anexe **todos os arquivos de `AI_import/`**, exceto o `Plano_Trabalho_Template.docx` (o modelo em branco), e **o conteúdo de `Adicionar Arquivos de referencia/`**:
   - `Instructions.md`
   - `Criterios_Protocolo.md`
   - `Revisa_o_Sistema_tica_template.docx`
   - `aula_2_revisao_sistematica.pdf`
   - `t10_11-PLANEJAMENTO DA PESQUISA CIENTÍFICA.pdf`
   - `Como_Classificar_as_Pesquisas_Antonio_Gil.doc`
   - `Plano_Pesquisa_<SeuNome>.pdf`
   - `Artigo_Obrigatorio_*.pdf` (se houver)
3. Envie o prompt:

   ```
   Siga integralmente as instruções do arquivo Instructions.md, usando os demais
   arquivos anexados. O plano de pesquisa é o arquivo Plano_Pesquisa_*.pdf e os
   arquivos Artigo_Obrigatorio_*.pdf (se houver) são os artigos de avaliação
   obrigatória. Execute todas as etapas sem pedir confirmações e entregue o
   template preenchido (.docx) e a planilha (.xlsx).
   ```

4. Aguarde. A execução pode levar de 20 minutos a 2 horas, dependendo da IA e do volume de registros.

### 3. Revise os resultados

A IA entrega:

- **Template da RSL preenchido** (.docx, itens 1 a 4): perguntas, plano de extração, protocolo e resultados das buscas.
- **Planilha** (.xlsx):
  - aba "Buscas", com strings, datas e número de resultados;
  - aba "Artigos", com seleção, qualidade e extração.
- **No chat**: resumo do levantamento e limitações.

A IA é uma **triagem assistida, não a decisão final**. Revise pessoalmente:

- os registros marcados como **Dúvida**;
- as decisões cuja evidência parecer fraca;
- uma amostra dos excluídos;
- a avaliação do artigo obrigatório, comparando-a com a sua leitura.

As contagens das buscas são reprodutíveis e devem ser iguais entre execuções no mesmo dia. Já a seleção e as notas de qualidade variam entre IAs e entre execuções.

---

## Boas práticas

- **Não altere o protocolo durante a execução.** Problemas encontrados vão como observação na planilha.
- **Uma execução, uma conversa.** Não reaproveite resultados de conversas anteriores; o `Instructions.md` proíbe isso.
- **Registre a IA usada** (modelo, nível de esforço, data) para garantir rastreabilidade.
- **Confira DOIs e links por amostragem.** As instruções proíbem inventar referências, mas vale verificar.
- **Para comparar IAs**, rode o mesmo pacote de arquivos em cada uma e compare as planilhas: concordância da seleção, notas de QA e evidências.
