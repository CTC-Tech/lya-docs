# Lya API

Serviço principal da integração, responsável pelo gerenciamento dos pacientes dentro do sistema. Os pacientes cadastrados por meio desse serviço estarão disponíveis na Lya, permitindo que os profissionais de saúde os selecionem e realizem atendimentos diretamente pela plataforma.

## Informações Gerais

* **Base URL (homologação):** <https://api.lya-health-hml.ctctech.link/integration/api/v2/>
* **Base URL (produção):** <https://api.lyahealth.com.br/integration/api/v2/>
* **Formato de Respostas:** JSON
* **Versão da API:** v2
* **Status da API:** Ativa

## **Validação de autenticação**

Para verificar a validade do token de acesso, utilize o endpoint abaixo. Essa verificação permite garantir que o token está ativo e autorizado para acessar os serviços da API.

#### Endpoint

Método: `GET`
Rota: `/actors/current/`

#### Exemplo de Requisição

```bash
curl -X GET "https://api.lyahealth.com.br/integration/api/v2/actors/current/" \
     -H "Authorization: Bearer SEU_TOKEN_AQUI"
```

Se o token for válido, a resposta será um código de sucesso com as informações associadas ao acesso. Caso contrário, a resposta indicará um erro de autenticação.
