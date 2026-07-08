# Análise de Produtividade por Variedade com ANOVA e Teste de Tukey

Este projeto apresenta uma análise estatística em Python para comparar a produtividade de diferentes variedades de soja. O notebook utiliza estatística descritiva, verificação de pressupostos, ANOVA, teste post-hoc de Tukey e visualizações gráficas para apoiar a interpretação dos resultados.

## Objetivo

Avaliar se existem diferenças estatisticamente significativas de produtividade entre variedades de soja e, quando aplicável, identificar quais variedades diferem entre si.

Além da comparação entre variedades, o notebook também propõe uma análise crítica de possíveis fatores confundidores, como setor geográfico e textura do solo, para evitar conclusões simplificadas baseadas apenas na produtividade média.

## Ideia central do projeto

A ideia do projeto é adequada para uma atividade acadêmica ou introdutória de análise de dados agrícolas, pois integra:

- dados agronômicos de produtividade;
- comparação entre grupos de variedades;
- aplicação de ANOVA;
- teste de Tukey para comparações múltiplas;
- gráficos para interpretação visual;
- discussão sobre fatores que podem interferir na produtividade.

Entretanto, para uma recomendação agronômica real, a análise precisa de um conjunto de dados maior e mais balanceado, com mais repetições por variedade, setor e textura de solo.

## Bibliotecas utilizadas

O notebook utiliza as seguintes bibliotecas:

```python
pandas
numpy
matplotlib
seaborn
scipy
statsmodels
```

## Estrutura esperada dos dados

O código trabalha com um DataFrame chamado `dados`. Esse DataFrame precisa estar carregado antes da execução das análises.

As principais colunas esperadas são:

| Coluna | Descrição |
|---|---|
| `gp_variedade` | Nome ou grupo da variedade de soja |
| `produtividade` | Produtividade observada, em sc/ha |
| `setor` | Setor geográfico ou área de produção |
| `textura` | Classe de textura do solo |

Exemplo de estrutura esperada:

```text
gp_variedade | produtividade | setor  | textura
TMG2776IPRO  | 65.90         | Centro | Argiloso
TMG 4182     | 47.39         | Sul    | Médio argiloso
```

## Etapas da análise

### 1. Importação das bibliotecas

O notebook inicia importando os pacotes necessários para manipulação dos dados, análise estatística e geração de gráficos.

### 2. Estatísticas descritivas

São calculadas estatísticas por variedade, incluindo:

- número de observações;
- média;
- desvio padrão;
- valores mínimo e máximo;
- quartis.

Essa etapa permite observar a produtividade média de cada variedade antes da aplicação dos testes estatísticos.

### 3. Verificação dos pressupostos da ANOVA

O notebook verifica dois pressupostos importantes:

- **Normalidade dos dados**, por meio do teste de Shapiro-Wilk;
- **Homogeneidade das variâncias**, por meio do teste de Levene.

Esses pressupostos são importantes porque a ANOVA pressupõe que os resíduos tenham distribuição aproximadamente normal e que as variâncias entre os grupos sejam semelhantes.

### 4. ANOVA

A ANOVA é aplicada para testar se há diferença significativa de produtividade entre as variedades.

Hipóteses utilizadas:

- **H0:** não há diferença significativa de produtividade entre as variedades;
- **H1:** há pelo menos uma variedade com produtividade significativamente diferente.

No resultado salvo no notebook, a ANOVA apresentou:

```text
F = 3.7218
p-valor = 0.1135
```

Como o p-valor foi maior que 0,05, a conclusão correta é **não rejeitar H0**. Portanto, com os dados disponíveis no notebook, não há evidência estatística suficiente para afirmar que as variedades diferem em produtividade.

### 5. Teste post-hoc de Tukey

O teste de Tukey é utilizado para comparar pares de variedades.

No resultado salvo no notebook, nenhuma comparação apresentou diferença significativa. Isso está coerente com o resultado da ANOVA, que também não indicou diferença estatística significativa entre variedades.

### 6. Visualizações gráficas

O notebook gera gráficos para apoiar a interpretação dos resultados:

- boxplot da produtividade por variedade;
- violinplot da produtividade por variedade;
- gráficos comparando variedade, setor e textura;
- heatmaps de produtividade média por variedade, setor e textura.

Os gráficos gerados são salvos como arquivos `.png`.

## Arquivos de saída

O notebook gera os seguintes arquivos de imagem:

```text
anova_produtividade_variedade_viz1.png
analise_fatores_confundidores.png
```

Esses arquivos podem ser utilizados em relatórios, apresentações ou discussão dos resultados.

## Pontos fortes do projeto

- A proposta está bem alinhada com análise de dados agrícolas.
- O uso de ANOVA e Tukey é adequado para comparar médias entre variedades.
- A inclusão de fatores confundidores torna a análise mais crítica e próxima da realidade agronômica.
- Os gráficos facilitam a apresentação dos resultados.
- O notebook possui boa estrutura didática, com explicações impressas durante a execução.

## Limitações importantes

Apesar da ideia ser adequada, alguns pontos precisam de atenção:

1. **O DataFrame `dados` não é criado no notebook**

   O notebook usa a variável `dados`, mas não há uma célula carregando os dados com `pd.read_csv()`, `pd.read_excel()` ou criando o DataFrame manualmente. Para o notebook ficar completo, é necessário adicionar uma etapa de importação dos dados.

2. **Poucas observações por variedade**

   No resultado salvo no notebook, há 10 talhões avaliados e 6 variedades. Algumas variedades possuem apenas uma observação. Isso limita bastante a confiabilidade da ANOVA, do teste de Tukey e das conclusões agronômicas.

3. **Grupos desbalanceados**

   Como algumas variedades possuem mais repetições que outras, a comparação entre médias fica menos robusta.

4. **Pressupostos pouco confiáveis com amostra pequena**

   O teste de normalidade não é bem avaliado quando há poucas observações por grupo. Em variedades com apenas uma observação, não é possível avaliar normalidade nem calcular desvio padrão de forma confiável.

5. **Análise de fatores confundidores exige mais dados**

   A análise envolvendo setor e textura é interessante, mas precisa de mais repetições em cada combinação de variedade, setor e textura. Com poucos dados, o modelo pode gerar interpretações instáveis.

6. **Ranking não deve ser tratado como recomendação definitiva**

   O ranking de produtividade média é útil como estatística descritiva, mas não deve ser usado sozinho como recomendação técnica, principalmente quando as diferenças não foram significativas.

## Sugestão de melhoria no notebook

Para tornar o notebook mais completo, recomenda-se adicionar uma célula de carregamento dos dados, por exemplo:

```python
dados = pd.read_csv("dados_produtividade.csv", sep=";")
```

Ou, caso esteja usando Excel:

```python
dados = pd.read_excel("dados_produtividade.xlsx")
```

Também é recomendável reorganizar o notebook na seguinte ordem:

1. Importação das bibliotecas;
2. Carregamento dos dados;
3. Tratamento das colunas;
4. Estatísticas descritivas;
5. Verificação dos pressupostos;
6. ANOVA;
7. Tukey;
8. Visualizações;
9. Análise de fatores confundidores;
10. Conclusão final.

## Como executar

1. Instale as dependências:

```bash
pip install pandas numpy matplotlib seaborn scipy statsmodels
```

2. Abra o notebook no Jupyter Notebook, JupyterLab ou Google Colab.

3. Certifique-se de que o arquivo de dados esteja na mesma pasta do notebook.

4. Execute as células na ordem correta.

## Interpretação resumida do resultado atual

Com os dados salvos na execução do notebook, a análise indicou que:

- a produtividade média geral foi de aproximadamente 60,88 sc/ha;
- foram avaliados 10 talhões;
- foram comparadas 6 variedades;
- a ANOVA apresentou p-valor de 0,1135;
- nenhuma comparação pelo teste de Tukey foi significativa;
- não há evidência estatística suficiente para afirmar que uma variedade foi superior às demais.

Assim, a conclusão técnica mais adequada é que a análise serve como demonstração metodológica, mas ainda não sustenta uma recomendação agronômica definitiva.

## Conclusão

O projeto é adequado como exercício acadêmico de análise estatística aplicada à agricultura. Ele demonstra bem como comparar produtividade entre variedades usando Python.

Para transformar a análise em uma recomendação técnica mais forte, seria necessário ampliar o número de observações, equilibrar as repetições por variedade e controlar melhor fatores como setor, textura do solo, manejo e condições ambientais.
