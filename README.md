## Modelo de difusão com mudança de regime por limiares lineares afins

Implementação de um modelo de movimento browniano geométrico com dois regimes,
em que a comutação entre regimes é ativada pelo cruzamento de duas
fronteiras lineares no tempo, $M(t) = a_1 t + b_1$ e $m(t) = a_2 t + b_2$. Ao
contrário de um modelo com limiares horizontais, as fronteiras podem ter declive,
acompanhando uma tendência de fundo do preço.

O repositório contém os dois notebooks: um relativo à estimação e validação em dados reais, e outro à validação em dados simulados.

## Conteúdo

- **`modelo_dados_reais.ipynb`** — pipeline completo: simulação do processo,
  classificação em regimes e estimação por máxima verosimilhança, geração de
  estimativas iniciais (quatro estratégias de inicialização), otimização por
  Nelder–Mead, comparação de modelos (MBG, limiares constantes, limiares
  afins) por AIC/BIC, diagnóstico dos parâmetros por regime,
  identificabilidade, validação fora da amostra, e aplicação a uma amostra de
  25 ativos do S&P 500 (cinco setores) em dez janelas de treino/teste.
- **`cenarios_simulados.ipynb`** — validação com verdade conhecida: gera
  trajetórias com parâmetros fixos, compara a recuperação dos
  parâmetros por dois métodos (classificação de regime conhecida vs.
  estimada), agrega viés, RMSE, cobertura empírica dos intervalos de
  confiança e identificabilidade sobre uma bateria de doze cenários e várias
  centenas de réplicas de Monte Carlo por cenário.

Cada notebook é **autocontido**: todas as funções do núcleo do modelo estão
definidas nas suas próprias células, sem dependências de outros ficheiros do
repositório.

## Como correr

Ambos os notebooks correm de ponta a ponta em qualquer ambiente Jupyter
(`jupyter notebook`, `jupyter lab`, ou VS Code/JupyterLab).
`modelo_dados_reais.ipynb` requer ligação à internet, para descarregar preços históricos via
`yfinance`.
`cenarios_simulados.ipynb` não tem dependências externas.

## Reprodutibilidade

- **Dados simulados**: a geração das trajetórias usa sementes fixas por
  omissão nos parâmetros das funções. `semente_ref=42` para a réplica de
  referência e `semente_base=0` para o estudo de Monte Carlo.
- **Validação fora da amostra em dados reais**: as simulações de Monte Carlo
  da banda de previsão usam uma semente fixa por simulação (`seed=0,...,1999`),
  embutida na própria função.
