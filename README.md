# Courses

Materiais de cursos de bioinformática e estatística.

## Estrutura do repositório

```
courses/
└── introduction_bioinformatics_PALOP_2026/   # Curso "Introdução à Bioinformática" (PALOP 2026)
    ├── Aula_1_Growth_Curves/                 # Curvas de crescimento microbiano + estatística
    ├── Aula_2_RT_PCR/                        # RT-PCR: deteção/quantificação + primers e BLAST
    ├── Aula_3_Mutações/                      # Análise de mutações e diagnóstico genético (PGT)
    ├── Relatórios alunos/                    # Relatórios entregues pelos grupos (não versionados)
    └── README.md                             # Detalhes do curso, instalação e como usar
```

> Cada aula tem versões dos notebooks: a de trabalho, a `_com_markdowns` (com teoria) e, na Aula 1, a `_com_resultados` (referência).

## Tópicos abordados

- Análise de curvas de crescimento microbiano (fases lag/exponencial/estacionária, μ_max, modelo de Gompertz);
- Estatística aplicada (média ± desvio-padrão, teste-t, ANOVA);
- RT-PCR e quantificação relativa (Ct, ΔCt, ΔΔCt, *fold change*);
- Bioinformática de sequências com BioPython e NCBI (Entrez, BLAST): *reverse complement*, qualidade de primers, alinhamentos, tradução;
- Deteção e classificação de mutações e diagnóstico genético pré-implantação (PGT-M, PGT-A, PGT-SR).

## Requisitos

- Python 3.8+
- pandas, numpy, matplotlib, scipy, statsmodels, biopython, jupyter

```bash
pip install pandas numpy matplotlib scipy statsmodels biopython jupyter
```

Consulta o [README do curso](introduction_bioinformatics_PALOP_2026/README.md) para instruções detalhadas de instalação e utilização.
