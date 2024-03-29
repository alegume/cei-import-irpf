# cei-import-irpf

Scripts de importação de extratos do CEI para geração de informações para Imposto de Renda (IRPF). **Aviso:**

> Não há nenhuma garantia de que esses códigos estão corretos.
> Toda e qualquer responsabilidade sobre o informe à Receita Federal é unica e exclusivamente do declarante.
> Verifique todas as informações, pois não há nenhuma garantia da corretude das mesmas. Use por sua conta e risco!

Algumas situações são ignoradas nesta versão e que podem gerar inconsistências. Exemplos:

 - transferência de ativos (entre corretoras, etc);
 - desdobramentos/agrupamentos (splits/implits);
 - IPO/OPA e fechamento de capital na B3;
 - subscrição em emissão de cotas de FIIs;
 - mudança de código do ativo, ou aquisição de empresa que implique na mudança (exemplo: KROT3 -> COGN3, SNSL3 -> SQIA3, FIBR3 -> SUZB33).
 - proventos em ativos

## Como funciona?

Basta baixar as planilhas de transações direto no site da CEI (https://cei.b3.com.br). Use o menu 'Extratos e Informativos' > 'Extrato BM&FBOVESPA'. Coloque as planilhas do ano anterior (2020) no diretório 'import-file-xls' e rode o script. Caso tenha feito operações em 2019, ou antes, copiei a planilha 'pms-anteriores.xls' que está dentro do diretório 'models' para o diretório 'import-file-xls'. Abra essa planilha e preencha com seus ativos e preços médios (provavelmente já informados no Imposto de Renda do ano anterior). Veja as observações mais abaixo.

## Instalar e executar

Após baixar/clonar e acessar o repositório, instale as dependências:

  `python3 -m pip install -r requirements.txt`

Execute o script de importação:

  `python3 bulk_import.py`

Pronto! Foi gerado um arquivo com seus preços médios (preco-medio.csv), um arquivo com suas vendas (vendas.csv) contendo lucros/prejuízos e os arquivos de transações no diretório 'negotiations'. Um arquivo para cada ativo.

### Python 3

Se estiver usando o Windows, instale o Python 3 antes de tudo.

### Customização

Nos arquivos .py existem algumas constantes que podem ser modificadas para customização. A mais importante, talvez, seja a constante 'COST_OF_OPERATION'. Mude o valor para inserir o custo de cada operação em sua corretora. Por padrão, essa contante está setada com valor 0. Se você possui custo de corretagem zero na sua corretora, não precisa mudar nada. Se você tem um custo fixo por operação, apenas defina esse valor para a constante. Se seu custo é proporcional, vai precisar alterar o código após o comentário '# Add the cost of operation on each negotiation'

## IMPORTANTE!!

Na minha conta na CEI, tem um erro nos meses de janeiro/2019 até Abril/2019. Todos os preços de compra estão multiplicados por 10. Abri as planilhas manualmente e editei esses valores. Verifique!


## Observações

Se quiser criar uma planilha de importação dos preços médios anteriores, use o modelo models/pms-anteriores.xls. Copie o modelo para import-file-xls, renomeie se achar necessário e edite os valores. O mesmo pode ser feito para subscrição de cotas de FIIs. Sempre que uma célula não tiver valor, preencha com 0. **NUNCA DEIXE A CELULA VAZIA! Também não deixe linhas vazias entre as informações.**
