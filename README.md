### README

# Identificação de Serviços por latitude e longitude 

Este projeto utiliza BigQuery para consultar dados de serviços de rua e calcula a proximidade com locais pré-definidos utilizando a fórmula de Haversine. O objetivo é identificar serviços próximos a determinadas filiais da Mottu.

---

## Estrutura do Código

1. **Instalação de Dependências**

   - `google-cloud-bigquery`: Biblioteca para consultas ao BigQuery.
   - `pandas`: Biblioteca para manipulação de dados.

2. **Autenticação**

   - Autenticação no Google Colab utilizando `auth.authenticate_user()`.

3. **Consulta ao BigQuery**

   - Uma query é executada para obter serviços de rua abertos no dia atual com a descrição "Inadimplência".

4. **Criação de Arquivos**

   - \`\`: Contém as informações de latitude e longitude das filiais.
   - \`\`: Resultado dos serviços associados às filiais.

5. **Fórmula de Haversine**

   - Utilizada para calcular a distância entre dois pontos geográficos.

6. **Processamento de Dados**

   - Para cada serviço:
     - Verifica-se a filial mais próxima.
     - Classifica o serviço como dentro ou fora de alcance (500 metros).

7. **Saída**

   - Resultado salvo em `matching_services.json`.
   - Exibição dos 5 primeiros resultados no console.

---

## Configuração e Execução

### Dependências

Certifique-se de ter as seguintes bibliotecas instaladas:

```bash
pip install google-cloud-bigquery pandas
```

### Autenticação

No Google Colab, execute:

```python
from google.colab import auth
auth.authenticate_user()
```

### Execução do Código

Basta executar o script. Ele realizará:

1. Consulta ao BigQuery.
2. Processamento de serviços e filiais.
3. Criação dos arquivos de entrada e saída.

---

## Estrutura dos Arquivos

### Entrada: `locations.json`

Arquivo JSON com as informações das filiais:

```json
{
  "lugares": [
    {
      "id": 1,
      "nome": "Mottu Butantã",
      "latitude": -23.57049468,
      "longitude": -46.70487346
    },
    ...
  ]
}
```

### Saída: `matching_services.json`

Arquivo JSON com os serviços correspondentes:

```json
[
  {
    "placa": "ABC1234",
    "filial": "Mottu Butantã",
    "local": "Mottu Butantã",
    "distancia_metros": 250.5,
    "tipo_situacao": "Indisponível",
    "tipo_situacao_detalhe": "06-Alugada"
  },
  ...
]
```

---

## Notas Técnicas

1. **Fórmula de Haversine**

   - Considera a Terra como uma esfera para calcular a distância entre dois pontos geográficos.

2. **Classificação de Distância**

   - Serviços a menos de 500 metros são considerados dentro do alcance.
   - Serviços acima de 500 metros são marcados como fora de alcance.

3. **Logs e Validações**

   - O código realiza verificações para lidar com coordenadas inválidas ou ausentes.

---

## Próximos Passos

1. **Otimizações**

   - Parâmetros dinâmicos para a query do BigQuery.
   - Suporte a diferentes critérios de distância.

2. **Integração**

   - Possibilidade de envio dos resultados via API para sistemas de monitoramento.

3. **Visualizações**

   - Criação de um dashboard para exibir os resultados.
   - Ativação de webhooks 
