## Documentação da API do Sinai Online

### **URL**
`https://api.sinaionline.com.br`


### **Autorização**  
Todas as requisições devem incluir um cabeçalho de autorização com o token da imobiliária, fornecido pela Sinaionline. Exemplo:

```
Authorization: XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX
```

### **Endpoint para Busca de Imóveis**  
`GET /api/v1/agencies/<codigo_da_imobiliaria>/properties/search`

Este endpoint permite realizar buscas de imóveis, aplicando filtros conforme os parâmetros fornecidos na query. Os parâmetros que podem ser utilizados são explicados abaixo.

### **Parâmetros da Query**  
Todos os parâmetros são **opcionais** e podem ser combinados para refinar a busca:

- **offerType**: Tipo da oferta do imóvel. Aceita os valores `'VENDA'` ou `'ALUGUEL'`.
- **neighborhoods**: Nomes dos bairros separados por vírgula. Para obter a lista de bairros válidos, consulte o endpoint [distinctTypesAndNeighborhoods](#distincttypesandneighborhoods).
- **propertyTypes**: Tipos de imóveis separados por vírgula. Para obter a lista de tipos válidos, consulte o endpoint [distinctTypesAndNeighborhoods](#distincttypesandneighborhoods).
- **cities**: Nomes das cidades separados por vírgula. Para obter a lista de cidades válidas, consulte o endpoint [distinctTypesAndNeighborhoods](#distincttypesandneighborhoods).
- **captador**: Nome do captador (corretor) responsável pelo imóvel.
- **codes**: IDs específicos dos imóveis.
- **isTop**: Flag que indica se o imóvel é destacado como "top" (`true` ou `false`).
- **isExclusive**: Flag que indica se o imóvel é exclusivo (`true` ou `false`).
- **isHighlight**: Flag que indica se o imóvel é destacado como "highlight" (`true` ou `false`).
- **isNewRelease**: Flag que indica se o imóvel é lançamento (`true` ou `false`).
- **minPrice**: Preço mínimo do imóvel.
- **maxPrice**: Preço máximo do imóvel.
- **minArea**: Área mínima do imóvel em metros quadrados.
- **maxArea**: Área máxima do imóvel em metros quadrados.
- **bedrooms**: Número de dormitórios.
- **suites**: Número de suítes.
- **garages**: Número de vagas de garagem.
- **page**: Página de resultados (para paginação).
- **limit**: Limite de resultados por página.
- **sortBy**: Critério de ordenação. Pode ser `'price'`, `'registerDate'` ou `'updateDate'` (valor padrão: `'price'`).
- **sortDir**: Direção da ordenação. Pode ser `'ASC'` (ascendente) ou `'DESC'` (descendente).
- **randomOrder**: Se `true`, os resultados serão retornados de forma aleatória, ignorando a ordenação especificada.

### **Exemplos de Requisições**

1. **Busca por imóveis à venda em bairros específicos com preço máximo:**
   ```http
   GET https://api.sinaionline.com.br/api/v1/agencies/12345/properties/search?offerType=VENDA&neighborhoods=Centro,Boqueirão&maxPrice=500000
   Authorization: XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX
   ```

2. **Busca por imóveis para aluguel com área mínima e 2 dormitórios:**
   ```http
   GET https://api.sinaionline.com.br/api/v1/agencies/12345/properties/search?offerType=ALUGUEL&minArea=50&bedrooms=2
   Authorization: XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX
   ```

3. **Busca por imóveis exclusivos, com 3 suítes, ordenados por preço em ordem descendente:**
   ```http
   GET https://api.sinaionline.com.br/api/v1/agencies/12345/properties/search?isExclusive=true&suites=3&sortBy=price&sortDir=DESC
   Authorization: XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX
   ```

4. **Busca por imóveis aleatórios sem filtros adicionais:**
   ```http
   GET https://api.sinaionline.com.br/api/v1/agencies/12345/properties/search?randomOrder=true
   Authorization: XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX
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
                "https://sistemasinaionline.com.br/sinaionline/imagens/9999_2801_03.jpg",
                "https://sistemasinaionline.com.br/sinaionline/imagens/9999_2801_04.jpg",
                "https://sistemasinaionline.com.br/sinaionline/imagens/9999_2801_05.jpg",
                "https://sistemasinaionline.com.br/sinaionline/imagens/9999_2801_06.jpg",
                "https://sistemasinaionline.com.br/sinaionline/imagens/9999_2801_07.jpg",
                "https://sistemasinaionline.com.br/sinaionline/imagens/9999_2801_08.jpg",
                "https://sistemasinaionline.com.br/sinaionline/imagens/9999_2801_09.jpg",
                "https://sistemasinaionline.com.br/sinaionline/imagens/9999_2801_10.jpg",
                "https://sistemasinaionline.com.br/sinaionline/imagens/9999_2801_11.jpg",
                "https://sistemasinaionline.com.br/sinaionline/imagens/9999_2801_12.jpg"
            ],
            "proprietario": "********",
            "endereco": "********",
            "chaves": "********"
        },
    ],
    "total": 6,
    "page": 1,
    "limit": 1,
    "total_pages": 1
}
```

---

### **[Endpoint DistinctTypesAndNeighborhoods](#distincttypesandneighborhoods)**

Este endpoint retorna a lista de bairros, cidades e tipos de imóveis válidos que podem ser usados nos filtros de busca.

#### **Endpoint**  
`GET https://api.sinaionline.com.br/api/v1/agencies/<codigo_da_imobiliaria>/properties/distinctTypesAndNeighborhoods`

#### **Resposta Esperada**

A resposta será um JSON contendo três listas:

- **neighborhoods**: Lista de bairros válidos.
- **cities**: Lista de cidades válidas.
- **propertyTypes**: Lista de tipos de imóveis válidos.

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
