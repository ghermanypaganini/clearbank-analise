# ClearBank — Análise Financeira com Python

Desafio final do módulo "Análise de Dados e Inteligência de Negócios com IA".
O notebook lê um histórico de transações em CSV valida e limpa os dados, calcula métricas financeiras mensais sinaliza transações suspeitas, exibe um relatório no terminal e exporta o resultado em JSON.
Planilha 'transacoes' contendo erros.

## Arquivos

| Arquivo               | Descrição                                                          |
| --------------------- | ------------------------------------------------------------------ |
| `desafio-clearbank.ipynb` | Notebook com o código (organizado em funções) e as saídas salvas   |
| `transacoes.csv`      | Arquivo de entrada (17 válidos, 5 inválidos, 2 acima de R$ 10.000) |
| `relatorio.json`      | Saída gerada pelo notebook                                         |

## Como executar

1. Abra `desafio-clearbank.ipynb` no Google Colab ou Jupyter (Python 3.10+).
2. Garanta que `transacoes.csv` esteja na mesma pasta.
3. Execute todas as células (no Colab: _Ambiente de execução → Executar tudo_).
4. O relatório aparece na saída da célula de execução principal e o arquivo
   `relatorio.json` é gerado na pasta.

## O que o notebook faz

- **Leitura** com o módulo `csv` nativo (`DictReader`) — sem pandas.
- **Validação e limpeza**: descarta silenciosamente linhas com `id` inválido,
  `cliente_id` vazio, data fora do formato `AAAA-MM-DD`, `tipo` diferente de
  `credito`/`debito` ou `valor` não numérico/≤ 0. Mostra o resumo da limpeza.
- **Datas** com `datetime` (`strptime`/`strftime`), extração do mês `AAAA-MM` e
  cálculo do período (dias entre a transação mais antiga e a mais recente).
- **Métricas mensais**: quantidade, total de crédito, total de débito, saldo,
  média, maior e menor valor por mês.
- **Transações suspeitas**: valor acima de `LIMITE_SUSPEITO = 10000.00`.
- **Exportação** em `relatorio.json` (`ensure_ascii=False, indent=2`).
- **Tratamento de erros** com `try/except` em 3 pontos: abertura do CSV
  (`FileNotFoundError`), conversão de `valor` para `float` e conversão de
  `data` para `datetime`.

## Organização do código

O notebook está dividido em funções com responsabilidades separadas:
`formatar_brl`, `validar_data`, `validar_valor`, `ler_transacoes`,
`validar_transacao`, `limpar_transacoes`, `gerar_relatorio`,
`detectar_suspeitas`, `calcular_periodo`, `salvar_json`, `exibir_relatorio` e
`main`.
