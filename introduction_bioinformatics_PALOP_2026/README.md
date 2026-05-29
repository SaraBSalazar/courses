# Introdução à Bioinformática — PALOP 2026

Curso prático de introdução à bioinformática, com aulas em **Jupyter Notebook** (Python) que aplicam ferramentas computacionais a problemas reais da Biologia e da Medicina. O material é orientado para trabalho em **grupos**, em que cada grupo analisa um organismo, conjunto de primers, categoria de doença ou síndrome diferente.

> **PALOP** — Países Africanos de Língua Oficial Portuguesa. Todo o material está em português.

---

## Objetivos de aprendizagem

No final do curso, os alunos serão capazes de:

- Carregar, filtrar e visualizar dados biológicos com **pandas** e **matplotlib**;
- Extrair parâmetros biológicos de curvas de crescimento e aplicar **testes estatísticos** (teste-t, ANOVA);
- Interpretar resultados de **RT-PCR** (valores Ct, ΔCt, ΔΔCt, *fold change*);
- Manipular sequências de DNA/proteína com **BioPython** (*reverse complement*, tradução, alinhamentos);
- Consultar bases de dados do **NCBI** (nucleotide, gene, BLAST) por código;
- Detetar e **classificar mutações** genéticas e compreender o seu impacto clínico (PGT-M, PGT-A, PGT-SR).

---

## Estrutura do curso

O curso está organizado num fio condutor: começa por caracterizar microrganismos em cultura pura (Aula 1), verifica quais sobrevivem em co-cultura (Aula 2) e termina na análise de mutações em contexto clínico (Aula 3).

| Aula | Pasta | Tema | Ferramentas-chave |
|---|---|---|---|
| **1** | `Aula_1_Growth_Curves/` | Curvas de crescimento microbiano e estatística | pandas, numpy, matplotlib, scipy, statsmodels |
| **2** | `Aula_2_RT_PCR/` | RT-PCR: deteção e quantificação em co-cultura | BioPython, NCBI BLAST, pandas, scipy |
| **3** | `Aula_3_Mutações/` | Análise de mutações e diagnóstico genético (PGT) | BioPython, NCBI (Entrez/BLAST), alinhamentos |

---

### Aula 1 — Curvas de crescimento microbiano

Análise do crescimento de **6 microrganismos** em cultura pura, a partir de leituras de densidade ótica (**OD600**) ao longo de 24 horas, com 3 réplicas biológicas cada.

**Organismos em estudo:**

| Grupo | Organismo | Tipo | Patogenicidade |
|---|---|---|---|
| 1 | *E. coli* K12 | Bactéria Gram− | Comensal |
| 2 | *Salmonella enterica* | Bactéria Gram− | Patogénico |
| 3 | *L. acidophilus* | Bactéria Gram+ | Comensal/probiótico |
| 4 | *C. difficile* | Bactéria Gram+ | Patogénico (oportunista) |
| 5 | *S. cerevisiae* | Levedura | Comensal/probiótico |
| 6 | *C. albicans* | Levedura | Patogénico (oportunista) |

**O que se faz:**
1. Carregar e visualizar os dados (média ± desvio-padrão, réplicas individuais);
2. Identificar as fases do crescimento (lag, exponencial, estacionária);
3. Estimar os parâmetros do modelo de **Gompertz**: plateau (**A**), taxa máxima de crescimento (**μ_max**) e fase lag (**λ**);
4. Comparar estatisticamente os organismos.

**Dados:** `crescimento_microbiano.csv` (colunas: `Strain`, `Replicate`, pontos temporais em horas).

---

### Aula 2 — RT-PCR: deteção e quantificação em co-cultura

Utiliza dados de **Real-Time PCR** para verificar quais espécies sobreviveram numa co-cultura e qual a sua abundância relativa face à cultura pura. O valor **Ct (Cycle Threshold)** é a métrica central: Ct baixo → espécie abundante; Ct > 35 → abaixo do limite de deteção.

**Exercício 1 — Análise dos primers:**
- Cálculo do *reverse complement* dos primers reversos;
- Avaliação da qualidade (comprimento 18–25 bp, %GC 40–60%, Tm pela Regra de Wallace: `Tm = 2(A+T) + 4(G+C)`);
- Identificação da espécie-alvo e verificação de especificidade via **NCBI BLAST**.

**Exercício 2 — Análise dos resultados de RT-PCR:**
- Visualização dos Ct brutos;
- Cálculo de **ΔCt → ΔΔCt → *fold change***;
- **Teste-t** (cultura pura vs co-cultura) e **ANOVA one-way**.

**Dados:** `primer_pairs.csv` (separador `;`), `rtpcr_cocultura.csv` (`Condicao`, `Primer`, `Replicate`, `Ct_gene`, `Ct_ref`).

---

### Aula 3 — Análise de mutações e diagnóstico genético (PGT)

Aplica bioinformática à deteção e classificação de alterações genéticas em embriões — **Diagnóstico Genético Pré-implantação (PGT)**.

| Tipo | Deteta | Exemplo clínico |
|---|---|---|
| **PGT-M** | Mutação num gene específico | Fibrose Quística, Huntington |
| **PGT-A** | Número errado de cromossomas | Trissomia 21, Monossomia X |
| **PGT-SR** | Rearranjos estruturais | Translocação Robertsoniana |

**Atribuição de genes por grupo (Exercício 1 — PGT-M):**

| Grupo | Categoria | Genes |
|---|---|---|
| 1 | Autossómicas recessivas | `CFTR`, `HBB`, `HEXA`, `SMN1` |
| 2 | Autossómicas dominantes | `HTT`, `FBN1`, `DMPK`, `NF1` |
| 3 | Ligadas ao cromossoma X | `DMD`, `FMR1`, `F8`, `F9` |
| 4 | Cancros hereditários | `BRCA1`, `BRCA2`, `MLH1`, `MSH2` |
| 5 | Metabólicas e de armazenamento | `GBA`, `PAH`, `GALT`, `ABCD1` |
| 6 | Neurológicas e neuromusculares | `PMP22`, `MPZ`, `TSC1`, `TSC2` |

**Pipeline por gene:** buscar referência no **NCBI** → alinhar com sequência mutada → identificar tipo e posição da mutação → traduzir para proteína → classificar impacto (sinónima / *missense* / *nonsense* / *frameshift*) → confirmar patogenicidade (ClinVar/OMIM, *guidelines* ACMG/AMP).

**Exercício 2 — PGT-A e PGT-SR:** buscar cromossomas no NCBI, simular contagem de cópias e detetar rearranjos.

**Dados:** `mutacoes_reais_genes.fasta` e `mutacoes_reais_genes.csv` (IDs no formato `GENE_mutX`, ex: `CFTR_mut1`).

---

## Pré-requisitos e instalação

- **Python 3.8+** (o ambiente do curso usa Python 3.8.10)
- Jupyter Notebook ou JupyterLab

### Pacotes necessários

```bash
pip install pandas numpy matplotlib scipy statsmodels biopython jupyter
```

### Configuração do ambiente (recomendado)

```bash
# A partir da pasta do curso
python3 -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install pandas numpy matplotlib scipy statsmodels biopython jupyter
jupyter notebook
```

> ⚠️ **NCBI / BioPython (Aulas 2 e 3):** as consultas ao NCBI (Entrez e BLAST) exigem que substituas `"o_teu_email@exemplo.com"` pelo **teu email real** nos notebooks. O NCBI bloqueia scripts sem identificação. Estes passos requerem **ligação à internet** e podem demorar (o BLAST online é lento).

---

## Como usar

1. Define o **número do teu grupo** na célula indicada de cada notebook (ex.: variável `MEU_GRUPO` ou `estirpe`).
2. Corre as células por ordem, de cima para baixo.
3. Responde às **Questões** assinaladas ao longo dos notebooks — são parte integrante do trabalho.

Cada aula tem versões dos notebooks:
- `Aula_*.ipynb` — versão de trabalho;
- `*_com_markdowns*.ipynb` — versão com explicações teóricas detalhadas (recomendada para estudo);
- `*_com_resultados.ipynb` — versão com resultados preenchidos (referência).

---

## Estrutura de ficheiros

```
introduction_bioinformatics_PALOP_2026/
├── Aula_1_Growth_Curves/        # Curvas de crescimento + estatística
│   ├── Aula_crescimento_microbiano.ipynb
│   ├── Aula_crescimento_microbiano_com_resultados.ipynb
│   └── crescimento_microbiano.csv
├── Aula_2_RT_PCR/               # RT-PCR, primers e BLAST
│   ├── Aula_2_RT_PCR.ipynb
│   ├── Aula_2_RT_PCR_com_markdowns.ipynb
│   ├── exercicios_tarde.ipynb
│   ├── primer_pairs.csv
│   └── rtpcr_cocultura.csv
├── Aula_3_Mutações/             # Mutações e diagnóstico genético (PGT)
│   ├── Aula_3.ipynb
│   ├── Aula_3_com_markdowns_v2.ipynb
│   ├── mutacoes_reais_genes.fasta
│   └── mutacoes_reais_genes.csv
├── Relatórios alunos/           # Relatórios entregues pelos grupos
└── README.md
```

---

## Conceitos abordados

**Análise de dados e estatística:** dataframes, média e desvio-padrão, barras de erro, ajuste de modelos (Gompertz), teste-t, ANOVA one-way, comparações múltiplas.

**Biologia molecular:** OD600 e crescimento microbiano, RT-PCR e Ct, primers e *reverse complement*, Tm e %GC, dogma central (DNA → RNA → proteína), tipos de mutação.

**Bioinformática:** BioPython (`Bio.Seq`, `Bio.Blast`, alinhamentos), NCBI (Entrez: nucleotide/gene/omim/clinvar; BLAST: nucleotide e BLASTx), interpretação de alinhamentos e *scoring*, classificação de variantes (ACMG/AMP).
