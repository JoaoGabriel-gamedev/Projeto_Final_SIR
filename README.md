<p align="center">
    <img src="assets/Logo_Ilum.png" alt = "Logo Ilum" widht="100%">
</p>
# Projeto_Final_Simulador_de_Epidemia(SIR)

## Informações do Autor

**Nome:** João Gabriel Coutinho Oliveira  
**Turma:** 26  
**Instituição:** Ilum – Escola de Ciência e Tecnologia

---

# 1. Introdução

A modelagem matemática de epidemias é uma ferramenta fundamental para compreender como doenças infecciosas se propagam em uma população. Através de modelos computacionais, é possível prever tendências de crescimento, identificar picos de infecção e analisar o impacto de diferentes parâmetros na evolução de uma epidemia.

Neste projeto foi desenvolvido um simulador baseado no modelo epidemiológico SIR (*Susceptible-Infected-Recovered*), um dos modelos mais clássicos da epidemiologia matemática. O programa foi implementado integralmente na linguagem Python e utiliza bibliotecas científicas amplamente empregadas em pesquisa e análise de dados.

O modelo permite acompanhar a evolução temporal de três grupos populacionais:

- **Suscetíveis (S):** indivíduos que podem contrair a doença;
- **Infectados (I):** indivíduos que estão contaminados e podem transmitir a doença;
- **Recuperados/Removidos (R):** indivíduos que não participam mais da transmissão, seja por recuperação ou remoção do sistema.

Ao final da simulação, o programa gera um gráfico que representa a dinâmica da epidemia ao longo do tempo.

---

# 2. Objetivos

## Objetivo Geral

Desenvolver uma simulação computacional baseada no modelo SIR para estudar a propagação de doenças infecciosas em uma população.

## Objetivos Específicos

- Implementar o modelo SIR em Python;
- Resolver numericamente as equações diferenciais do sistema;
- Visualizar a evolução dos grupos S, I e R ao longo do tempo;
- Analisar o efeito das taxas de transmissão e recuperação sobre a dinâmica da epidemia.

---

# 3. Metodologia e Métodos

## 3.1 Ferramentas Utilizadas

O projeto foi desenvolvido em Python utilizando as seguintes bibliotecas:

### NumPy

A biblioteca NumPy é utilizada para operações matemáticas e manipulação eficiente de vetores e matrizes.

**Principais funções:**

- Criação de arrays numéricos;
- Operações matemáticas vetorizadas;
- Geração do vetor de tempo utilizado na simulação.

### SciPy

A biblioteca SciPy fornece ferramentas para computação científica.

Neste projeto, utiliza-se o módulo de integração numérica para resolver o sistema de equações diferenciais do modelo SIR.

**Principais funções:**

- Resolução numérica de equações diferenciais ordinárias (EDOs);
- Cálculo da evolução temporal da epidemia.

### Matplotlib

A biblioteca Matplotlib é utilizada para gerar gráficos científicos.

**Principais funções:**

- Plotagem das curvas S, I e R;
- Personalização dos gráficos;
- Visualização dos resultados da simulação.

---

## 3.2 Modelo Matemático SIR

O modelo SIR divide a população em três compartimentos:

### Suscetíveis (S)

Representam indivíduos saudáveis que podem ser infectados.

### Infectados (I)

Representam indivíduos que possuem a doença e podem transmiti-la.

### Recuperados (R)

Representam indivíduos que já não transmitem a doença.

A população total é dada por:

```math
N = S + I + R
```

O comportamento do sistema é descrito pelas seguintes equações diferenciais:

### Variação dos suscetíveis

```math
\frac{dS}{dt} = -\beta \frac{SI}{N}
```

### Variação dos infectados

```math
\frac{dI}{dt} = \beta \frac{SI}{N} - \gamma I
```

### Variação dos recuperados

```math
\frac{dR}{dt} = \gamma I
```

Onde:

- **β (beta)** = taxa de transmissão da doença;
- **γ (gama)** = taxa de recuperação;
- **N** = população total.

---

## 3.3 Variáveis do Projeto

### N

População total considerada na simulação.

**Tipo:** `int`

### I0

Número inicial de infectados.

**Tipo:** `int`

### R0

Número inicial de recuperados.

**Tipo:** `int`

### S0

Número inicial de suscetíveis.

Calculado por:

```math
S0 = N - I0 - R0
```

**Tipo:** `int`

### beta

Taxa de transmissão da doença.

**Tipo:** `float`

### gamma

Taxa de recuperação da doença.

**Tipo:** `float`

### t

Vetor que representa o período de tempo analisado.

**Tipo:** `numpy.ndarray`

---

## 3.4 Funcionamento do Código

O programa segue as seguintes etapas:

### 1. Definição dos parâmetros

São definidos:

- população total;
- número inicial de infectados;
- número inicial de recuperados;
- taxa de transmissão;
- taxa de recuperação;
- período da simulação.

### 2. Cálculo dos suscetíveis iniciais

O programa calcula automaticamente:

```math
S0 = N - I0 - R0
```

### 3. Implementação das equações SIR

É criada uma função responsável por calcular as taxas de variação dos grupos:

```python
def sir(y, t, N, beta, gamma):
    S, I, R = y

    dSdt = -beta * S * I / N
    dIdt = beta * S * I / N - gamma * I
    dRdt = gamma * I

    return dSdt, dIdt, dRdt
```

Essa função calcula:

- dS/dt;
- dI/dt;
- dR/dt.

### 4. Resolução Numérica

O método de integração numérica da biblioteca SciPy resolve o sistema de equações diferenciais.

O resultado é uma tabela contendo os valores de:

- S(t);
- I(t);
- R(t).

### 5. Geração do gráfico

Utilizando Matplotlib, são geradas três curvas:

- Azul: Suscetíveis;
- Vermelho: Infectados;
- Verde: Recuperados.

---

# 4. Resultados e Discussão

A simulação produz um gráfico que descreve a evolução da doença ao longo do período analisado.

Inicialmente, a maior parte da população encontra-se suscetível e apenas uma pequena parcela está infectada. À medida que o tempo passa, ocorre um aumento no número de infectados devido à transmissão da doença.

O crescimento da curva de infectados continua até atingir um valor máximo, conhecido como **pico epidêmico**. Após esse ponto, o número de infectados começa a diminuir porque cada vez mais indivíduos passam para o grupo dos recuperados.

Simultaneamente, observa-se uma redução contínua da população suscetível, uma vez que novos indivíduos são infectados. Já a população recuperada cresce continuamente até estabilizar-se quando a epidemia chega ao fim.

Os resultados obtidos estão de acordo com o comportamento esperado do modelo SIR descrito na literatura científica. Além disso, a simulação permite observar como alterações nos parâmetros β e γ podem modificar significativamente a velocidade de propagação da doença e a intensidade do pico epidêmico.

---

# 5. Conclusão

O projeto permitiu implementar e analisar computacionalmente o modelo epidemiológico SIR utilizando Python. A utilização das bibliotecas NumPy, SciPy e Matplotlib possibilitou realizar cálculos numéricos eficientes e visualizar graficamente a evolução da epidemia.

Os resultados demonstraram que o modelo é capaz de representar adequadamente a dinâmica básica de transmissão de doenças infecciosas, evidenciando a interação entre indivíduos suscetíveis, infectados e recuperados.

Além de reforçar conceitos de programação científica, o projeto contribuiu para a compreensão de modelos matemáticos aplicados à epidemiologia, mostrando como ferramentas computacionais podem auxiliar no estudo e na previsão da propagação de doenças em populações.

---

# Como Executar o Projeto

O projeto encontra-se no arquivo:

```text
Simulador_epidemia.ipynb
```

Para executar ou modificar a simulação:

1. Baixe o arquivo para seu computador;
2. Abra-o em um ambiente compatível com Python, como:
   - JupyterLab;
   - Jupyter Notebook;
   - Visual Studio Code;
   - Google Colab;
3. Altere os parâmetros desejados diretamente no código:
   - população total;
   - número inicial de infectados;
   - número inicial de recuperados;
   - taxa de transmissão (`beta`);
   - taxa de recuperação (`gamma`);
   - tempo de simulação;
4. Execute todas as células do notebook;
5. Observe o gráfico gerado pelo programa.

---

# Referências

- KERMACK, W. O.; MCKENDRICK, A. G. *A Contribution to the Mathematical Theory of Epidemics*. Proceedings of the Royal Society A, 1927.
- Python Software Foundation. *Python Documentation*.
- HARRIS, C. R. et al. *Array Programming with NumPy*. Nature, 2020.
- VIRTANEN, P. et al. *SciPy 1.0: Fundamental Algorithms for Scientific Computing in Python*. Nature Methods, 2020.
- HUNTER, J. D. *Matplotlib: A 2D Graphics Environment*. Computing in Science & Engineering, 2007.
