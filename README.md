# Conferência de Guias RET

Aplicação para conferir guias RET em PDF contra a planilha `Apuracao-RET.xlsx`.

# O que o programa faz

1. Lê todos os PDFs da pasta selecionada, inclusive em subpastas.
2. Extrai de cada guia:
   - Razão social;
   - CNPJ RET;
   - CNPJ ostensiva;
   - Código de receita;
   - Período de apuração;
   - Valor da guia.
3. Lê a planilha `Apuracao-RET.xlsx`.
4. Cruza os dados usando a chave:

CNPJ RET + Razão Social + CNPJ Ostensiva + Código Receita + Período de Apuração

5. Compara o valor do PDF com o valor da planilha.
6. Gera o arquivo `resultado_conferencia-RET.xlsx` na pasta onde está a planilha de entrada.

#  Regras de resultado
Situação | Status Final 
Guia localizada e valor igual | `ok`
Guia localizada e valor diferente | `revisar` 
Linha da planilha sem PDF correspondente | `revisar` — Apenas planilha 
PDF sem linha correspondente na planilha | `revisar` — Apenas guia 

A conferência considera o valor correto somente quando a diferença é exatamente `0,00`.

# Normalizações aplicadas

- Razão social: remove acentos, espaços duplicados e diferenças entre maiúsculas/minúsculas;
- CNPJ ostensiva: comparado somente pelos dígitos e exibido formatado como `00.000.000/0000-00`;
- CNPJ RET: padronizado para `XXXX-XX`;
- Código de receita: utiliza somente a parte antes do hífen, por exemplo `1068-07` vira `1068`;
- Período: normalizado internamente para `AAAA-MM`;
- Valores: arredondados para duas casas decimais.

## Utilização
Basta abrir o executável e selecionar:
1) A pasta dos PDFs;
2) A pasta que contém o arquivo Apuracao-RET.xlsx.
