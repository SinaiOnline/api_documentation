## Documentação da API do Sistema Sinaionline

### URL
```text
https://api.sinaionline.com.br
```

### Autorização
Todas as requisições devem incluir um cabeçalho de autorização com o token da imobiliária, fornecido pela Sinaionline. Exemplo:

```http
Authorization: XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX
```

---

### Endpoint para Busca de Imóveis
```http
GET /api/v1/agencies/<codigo_da_imobiliaria>/properties/search
```
Este endpoint permite realizar buscas de imóveis, aplicando filtros conforme os parâmetros fornecidos na query.

### Parâmetros da Query
Todos os parâmetros são **opcionais** e podem ser combinados para refinar a busca:

- `offerType`: Tipo da oferta do imóvel. Aceita os valores `VENDA` ou `ALUGUEL`.
- `neighborhoods`: Nomes dos bairros separados por vírgula. Para obter a lista de bairros válidos, consulte o endpoint [`filter-data`](#endpoint-para-dados-de-filtro-de-busca) abaixo.
- `propertyTypes`: Tipos de imóveis separados por vírgula.
- `cities`: Nomes das cidades separados por vírgula.
- `captador`: Nome do captador (corretor) responsável pelo imóvel.
- `codes`: IDs específicos dos imóveis.
- `isTop`: Flag que indica se o imóvel é destacado como "top" (`true` ou `false`).
- `isExclusive`: Flag que indica se o imóvel é exclusivo (`true` ou `false`).
- `isHighlight`: Flag que indica se o imóvel é destacado como "highlight" (`true` ou `false`).
- `isNewRelease`: Flag que indica se o imóvel é lançamento (`true` ou `false`).
- `minPrice`: Preço mínimo do imóvel.
- `maxPrice`: Preço máximo do imóvel.
- `minArea`: Área mínima do imóvel em metros quadrados.
- `maxArea`: Área máxima do imóvel em metros quadrados.
- `bedrooms`: Número de dormitórios.
- `suites`: Número de suítes.
- `garages`: Número de vagas de garagem.
- `page`: Página de resultados (para paginação).
- `limit`: Limite de resultados por página.
- `sortBy`: Critério de ordenação. Pode ser `price`, `registerDate` ou `updateDate` (valor padrão: `price`).
- `sortDir`: Direção da ordenação. Pode ser `ASC` ou `DESC`.
- `randomOrder`: Se `true`, os resultados serão retornados de forma aleatória.

### Exemplos de Requisições

**1. Busca por imóveis à venda em bairros específicos com preço máximo:**
```http
GET https://api.sinaionline.com.br/api/v1/agencies/12345/properties/search?offerType=VENDA&neighborhoods=Centro,Boqueirão&maxPrice=500000
```

**2. Busca por imóveis para aluguel com área mínima e 2 dormitórios:**
```http
GET https://api.sinaionline.com.br/api/v1/agencies/12345/properties/search?offerType=ALUGUEL&minArea=50&bedrooms=2
```

**3. Busca por imóveis exclusivos, com 3 suítes, ordenados por preço em ordem descendente:**
```http
GET https://api.sinaionline.com.br/api/v1/agencies/12345/properties/search?isExclusive=true&suites=3&sortBy=price&sortDir=DESC
```

**4. Busca por imóveis aleatórios sem filtros adicionais:**
```http
GET https://api.sinaionline.com.br/api/v1/agencies/12345/properties/search?randomOrder=true
```

**Exemplo de resposta:**
```json
{
  "properties": [
    {
      "codimobiliaria": "9999",
      "codimovel": "2801",
      "cadastro": "19/11/2014",
      "update": "03/10/2024",
      "imovel": "APARTAMENTO",
      "nquartos": "4",
      "numero": "2323",
      "complemento": "",
      "bairro": "BELVEDERE",
      "cep": "3333333",
      "regiao": "CONDOMÍNIOS FECHADOS",
      "cidade": "BELO HORIZONTE",
      "uf": "MG",
      "quartos": "4",
      "suites": "2",
      "salas": "2",
      "banho": "0",
      "elevadores": "2",
      "apandar": "0",
      "pavimentos": "0",
      "garagens": "4",
      "m2util": "500",
      "m2terreno": "0",
      "idade": "0",
      "posicao": "",
      "armquartos": "1",
      "blindex": "0",
      "dce": "0",
      "armcozinha": "0",
      "varanda": "1",
      "arprivativa": "0",
      "arlazer": "0",
      "piscina": "0",
      "desocupado": "0",
      "salafestas": "0",
      "salajogos": "0",
      "esportes": "0",
      "porteiro": "0",
      "vagassep": "0",
      "preco": "2000000",
      "condominio": "0",
      "iptu": "0",
      "obs": "<br><br>",
      "img": "01,02,03,04,05,06,07,08,09,10,11,12",
      "captador": "",
      "url_video": "",
      "lancamento": 0,
      "observ": "",
      "seo_titulo": "",
      "seo_palavras_chaves": "",
      "seo_descricao": "",
      "offer_type": "VENDA",
      "imageURLs": [
        "https://sistemasinaionline.com.br/sinaionline/imagens/9999_2801_01.jpg",
        "https://sistemasinaionline.com.br/sinaionline/imagens/9999_2801_02.jpg",
        ...
      ],
      "proprietario": "********",
      "endereco": "********",
      "chaves": "********"
    }
  ],
  "total": 6,
  "page": 1,
  "limit": 1,
  "total_pages": 1
}
```

---

### Endpoint para dados de filtro de busca

Este endpoint retorna as opções disponíveis de tipos de imóveis, cidades e bairros que podem ser utilizados nos filtros de busca. É possível enviar parâmetros opcionais na query para refinar os resultados, fazendo com que as opções retornadas sejam compatíveis com os critérios informados.

#### Endpoint
```http
GET /api/v1/agencies/<codigo_da_imobiliaria>/properties/filter-data
```
### Parâmetros da query

- offerType: ao informar VENDA, o endpoint retorna as opções relacionadas aos imóveis disponíveis para venda. Ao informar ALUGUEL, retorna as opções relacionadas aos imóveis disponíveis para aluguel.
- propertyTypes: ao informar um ou mais tipos de imóveis, as listas de cidades e bairros são limitadas às opções que possuem imóveis correspondentes aos tipos selecionados, respeitando também o tipo de oferta informado.
- cities: ao informar uma ou mais cidades, a lista de bairros é limitada aos bairros disponíveis nas cidades selecionadas, respeitando os demais filtros informados.

Todos os parâmetros são opcionais e podem ser combinados para refinar progressivamente as opções disponíveis. Por exemplo, uma aplicação pode primeiro consultar os tipos de imóveis para venda, depois buscar as cidades que possuem imóveis desses tipos e, por fim, apresentar apenas os bairros disponíveis nas cidades selecionadas.

1. Obter opções relacionadas a imóveis à venda
```http
GET /api/v1/agencies/12345/properties/filter-data?offerType=VENDA
```
Retorna as opções de tipos de imóveis, cidades e bairros relacionadas à oferta de venda.

2. Filtrar as opções por tipo de imóvel
```http
GET /api/v1/agencies/12345/properties/filter-data?offerType=VENDA&propertyTypes=APARTAMENTO
```
Retorna as opções de cidades e bairros que possuem apartamentos disponíveis para venda, além das demais opções de tipos de imóveis conforme o comportamento do endpoint.

3. Filtrar os bairros por cidade
```http
GET /api/v1/agencies/12345/properties/filter-data?offerType=VENDA&propertyTypes=APARTAMENTO&cities=NOVA%20LIMA
```
Retorna os bairros disponíveis em Nova Lima que possuem apartamentos à venda, respeitando os filtros informados.

#### Resposta Esperada

A resposta será um JSON contendo três listas:

- `neighborhoods`: Lista de bairros válidos.
- `cities`: Lista de cidades válidas.
- `propertyTypes`: Lista de tipos de imóveis válidos.

**Exemplo de resposta:**

```json
{
  "neighborhoods": [
    "ALPHAVILLE", "ANCHIETA", "BELVEDERE", "CENTRO", "FLORESTA", "JARDINS DAS MANGABEIRAS", "MANGABEIRAS", "SAVASSI", "VALE DO SERENO"
  ],
  "cities": [
    "BELO HORIZONTE", "BRUMADINHO", "CONTAGEM", "NOVA LIMA", "SABARA"
  ],
  "propertyTypes": [
    "ANDAR", "AP DUPLEX", "APARTAMENTO", "CASA", "CASA EM CONDOMINIO", "COBERTURA", "LOJA", "PREDIO COMERCIAL"
  ]
}
```

---

### Endpoint para Imóveis Similares

```http
GET /api/v1/agencies/<codigo_da_imobiliaria>/properties/<codigo_do_imovel>/similar
```

Retorna um array com até 4 imóveis similares ao imóvel base. Caso não haja imóveis similares, retorna um array vazio.

As propriedades são consideradas como similares com base nos seguintes critérios:

- Preço entre 80% e 120% do valor do imóvel base.
- Mesma quantidade de quartos.
- Mesmo tipo de imóvel (ex: casa, apartamento).
- Mesmo tipo de oferta: `VENDA` ou `ALUGUEL`.

---

### Endpoint para armazenamento de leads

O endpoint permite salvar mensagens de leads e pode ser utilizado por sites imobiliários, landing pages, formulários de contato e outras aplicações integradas ao Sinaionline.

### Endpoint

```http
POST /api/v1/agencies/<codigo_da_imobiliaria>/leads
```

### Corpo da requisição

O corpo deve ser enviado no formato JSON.

| Campo         | Tipo                             | Obrigatório               | Descrição                                 |
| ------------- | -------------------------------- | ------------------------- | ----------------------------------------- |
| `lead_origin` | String                           | Sim                       | Origem do lead, como `SITE DA EMPRESA`    |
| `timestamp`   | String, formato de data ISO 8601 | Sim                       | Data e hora de criação ou envio do lead   |
| `property_id` | String                           | Não                       | Código do imóvel relacionado ao interesse |
| `name`        | String                           | Sim                       | Nome completo do interessado              |
| `email`       | String                           | Sim                       | E-mail do interessado                     |
| `ddd`         | String                           | Sim                       | DDD do telefone                           |
| `phone`       | String                           | Sim                       | Número do telefone, sem o DDD             |
| `message`     | String                           | Sim                       | Mensagem ou descrição do interesse        |
| `offer_type`  | String                           | Sim                       | Tipo de interesse: `VENDA` ou `ALUGUEL`   |

### Exemplo de requisição cURL

```bash
curl -X POST "https://api.sinaionline.com.br/api/v1/agencies/12345/leads" \
  -H "Authorization: XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX" \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -d '{
    "lead_origin": "SITE DA EMPRESA",
    "timestamp": "2026-10-23T10:23:00-03:00",
    "property_id": "2801",
    "name": "João da Silva",
    "email": "joao@example.com",
    "ddd": "31",
    "phone": "999998888",
    "message": "Tenho interesse neste imóvel. Gostaria de agendar uma visita.",
    "offer_type": "VENDA"
  }'
```

Substitua o código da imobiliária, o token de autorização e os dados de exemplo pelos valores reais.

### Exemplo de corpo JSON

```json
{
  "lead_origin": "SITE DA EMPRESA",
  "timestamp": "2026-10-23T10:23:00-03:00",
  "property_id": "2801",
  "name": "João da Silva",
  "email": "joao@example.com",
  "ddd": "31",
  "phone": "999998888",
  "message": "Tenho interesse neste imóvel. Gostaria de agendar uma visita.",
  "offer_type": "VENDA"
}
```

### Regras de preenchimento

- **`lead_origin`:** identifique a origem do contato, por exemplo, `SITE DA EMPRESA`, `LANDING PAGE`.
- **`timestamp`:** envie a data e a hora em formato ISO 8601, preferencialmente com o deslocamento de fuso horário. Exemplo: `2026-10-23T10:23:00-03:00`.
- **`property_id`:** campo opcional. Deve ser informado quando o lead estiver relacionado a um imóvel específico. Quando não houver imóvel associado, o campo pode ser omitido.
- **`ddd`:** informe o código de área como texto, sem parênteses.
- **`phone`:** informe o número do telefone separado do DDD.
- **`message`:** utilize este campo para registrar a mensagem enviada pelo interessado.
- **`offer_type`:** utilize este campo para registrar o tipo de interesse do lead, comprar ou alugar, utilize exclusivamente `VENDA` ou `ALUGUEL`.

### Exemplo de envio sem imóvel associado

Quando o contato não estiver vinculado a um imóvel específico, omita o campo `property_id`.

```json
{
  "lead_origin": "LANDING PAGE",
  "timestamp": "2026-10-23T10:23:00-03:00",
  "name": "Maria Oliveira",
  "email": "maria@example.com",
  "ddd": "31",
  "phone": "988887777",
  "message": "Gostaria de receber informações sobre imóveis disponíveis.",
  "offer_type": "ALUGUEL"
}
```

### Possíveis respostas da API

| Código HTTP                 | Significado                                    |
| --------------------------- | ---------------------------------------------- |
| `200 OK`                    | Requisição processada com sucesso              |
| `400 Bad Request`           | Dados enviados inválidos                       |
| `401 Unauthorized`          | Token ausente ou inválido                      |
| `404 Not Found`             | Recurso ou imobiliária não encontrado          |
| `500 Internal Server Error` | Erro interno no servidor                       |
