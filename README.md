# TESTE PARA PYTHON CANDIDATOS 2022
## Scripts:

O front-end foi desenvolvido utilizando [React](https://github.com/facebook/react), desta forma, fornecemos o build da aplicação.

Para rodar o frontend em sua maquina local utilize a extensão [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) ou outro mecanismo de fornecimento de página estáticas, compatível com javascript, de sua preferência.

Em caso de dúvidas, entre em contato conosco.

## Desafio dashboard backend

O teste tem como objetivo fornecer um dashboard de vendas realizadas durante o ano de 2018 e auxiliar o gestor na tomada de decisão.

O projeto final deve apresentar dois gráficos:

1. Responsável por exibir a quantidade e o valor dos produtos vendidos por mês.
2. Responsável por exibir os produtos mais vendidos em ordem decrescente.

Para isso, crie um projeto backend utilizando seus conhecimentos em **node.js**

### Atenção:

- O backend deve ser disponibilizado em `http://localhost:5000`;
- Todas as rotas mencionadas neste teste devem estar dentro do recurso `/api/v1/sales/`;
- Utilize um banco de dados de sua preferência.

### Ticket 1:
O dashboard é apresentado somente quando temos dados disponíveis, portanto implemente na rota `/number-of-sales` uma função que retorne à quantidade de registros disponíveis no banco de dados.

A API deve retornar um JSON no seguinte formato: 
```JAVASCRIPT
{ 
  "number_of_sales": number
} 
```

### Ticket 2:
Para popular os dados das vendas, utilize o arquivo **dados.csv** fornecido neste repositório, implemente na rota `/upload` uma função capaz de receber o arquivo, ler seu conteúdo e registrá-lo no banco de dados.
Os dados devem ser registrados no seguinte formato:
```JAVASCRIPT
{
  "date": string, // data da venda
  "product_code": string, // código do produto
  "product_description": string,// descrição do produto
  "quantity": number, // quantidade de produtos vendidos
  "price": number, // preço comercializado
  "total": number // valor total da venda
} 
```
Utilize o **multer** (https://github.com/expressjs/multer ) para fazer upload do arquivo csv.

O frontend enviará o arquivo csv no campo **file**, portanto sua rota deve ser algo como:
```JAVASCRIPT
salesRouter.route('/upload').post(upload.single('file’), ....); 
``` 

### Ticket 3:
Para limpar os dados das vendas, implemente uma função que espera o verbo **DELETE** na rota `/all`, de forma que ao ser executada, todos os registros devem ser removidos. 

### Ticket 4:
Implemente na rota `/by-month`, uma função capaz de retornar à quantidade e valor total dos produtos vendidos por mês.

A API deve retornar um JSON no seguinte formato:
```JAVASCRIPT
[
  {
    "month": number, // mês;
    "quantity": number, // quantidade total vendido 
    "amount": number // valor total vendido
  },
  {
    "month": number, // mês;
    "quantity": number, // quantidade total vendido 
    "amount": number // valor total vendido
  },
  {...}
]
```

### Ticket 5:
Implemente na rota `/best-selling-products` uma função que retorne os dados dos produtos mais vendidos no ano de 2018.

A quantidade de resultados a serem exibidos será determinada pelo parâmetro `entries_per_page` enviado para a rota, exemplo:

```JAVASCRIPT
/best-selling-products/?entries_per_page=20
```
Ao executar a função a API deve retornar JSON no seguinte formato:
```JAVASCRIPT
{
	"products": [
		{
			"product_code": string, // código do produto,
			"product_description": string, // descrição do produto
			"quantity": number // quantidade de produtos vendidos
		},
		{
			"product_code": string, // código do produto,
			"product_description": string, // descrição do produto
			"quantity": number // quantidade de produtos vendidos
		},
		{...}
	],
	"entries_per_page":number,
	"total_results": number
}
```
