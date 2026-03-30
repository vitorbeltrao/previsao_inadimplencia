# Predição de Inadimplência e Estratégia de Crédito

Este projeto desenvolve uma solução completa, unindo um modelo preditivo de probabilidade de default em tempo real e uma proposta de política de crédito para orientar decisões de negócio.
***

## Como Executar o Projeto
Este projeto utiliza o Poetry para garantir a reprodutibilidade do ambiente.

1. Instalação do Ambiente
Certifique-se de ter o Python 3.12+ e o Poetry instalados. Na raiz do projeto, execute:

`poetry install` (para instalar as bibliiotecas necessárias).
`poetry shell` (ativar o ambiente virtual).

2. Criação das pastas de dados
Na raiz do projeto, crie uma pasta chamada `data/raw` e nela coloque todos os arquivos de dados (cadastral, submissao, histórico empresticos, histórico parcelas e dicionário).

3. Uso dos Notebooks
Siga a ordem abaixo para processar os dados e gerar os resultados:

`data_engineering.ipynb`: Realiza a limpeza e agregação dos históricos de empréstimos e parcelas desde 2017. Gera a base curada para modelagem.
`ml_models.ipynb`: Contém o treinamento do modelo final e a aplicação das previsões na `base_submissao.parquet`.
*** 

# Metodologia e Resultados

**Definição de Inadimplência**: Foi adotada a régua de atraso superior a 90 dias (norma BACEN) para definir o target.

**Engenharia de Features**: Criação de variáveis de comportamento histórico e razões financeiras (LTV, Parcela/Renda) sem vazamento de dados.

**Performance**: O modelo atingiu um AUC de 0.7823, permitindo um ranqueamento eficaz dos clientes por nível de risco.
***

# Proposta de Política de Crédito

A política de crédito define os critérios e procedimentos para a concessão, visando minimizar perdas e garantir a saúde financeira. Com base no score gerado pelo modelo, propõe-se a seguinte estratégia:

1. Segmentação por Faixas de Risco

Os clientes devem ser classificados em grupos de acordo com a probabilidade de default (PD): 

* **Faixa A (Risco Mínimo)**: Aprovação automática com taxas de juros competitivas.

* **Faixas B e C (Risco Moderado)**: Aprovação condicionada a garantias adicionais (colaterais) ou redução do limite solicitado.

* **Faixa D (Risco Alto)**: Revisão manual pela mesa de crédito ou exigência de entrada mais elevada.

* **Faixa E (Risco Crítico)**: Rejeição automática da solicitação para proteger o fluxo de caixa.

2. Ajuste de Limites e Prazos

* **Cálculo de Limite**: O limite de crédito deve ser um múltiplo da renda comprovada, ajustado pelo percentual de risco da faixa do cliente.

* **Prazos**: Clientes de maior risco devem ter acesso a prazos de pagamento mais curtos para reduzir a exposição temporal da instituição.

3. Ações Preventivas e Cobrança
* **Monitoramento**: Clientes com scores que degradam ao longo do tempo (Behavior Scoring) devem sofrer redução preventiva de limite.

* **Cobrança Ágil**: Clientes identificados pelo modelo com alta propensão ao atraso devem receber lembretes preventivos antes do vencimento da fatura.
***

# Entregáveis

* **submissao_case.csv**: Probabilidades geradas para a base de teste.

* **Código-fonte**: Scripts organizados e dependências via Poetry.

* **README**: Definição da variável alvo e propostas de políticas de crédito.
