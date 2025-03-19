# Lya Tenants

Serviço responsável por gerenciar os acessos à API, assegurando que apenas aplicações autorizadas possam utilizá-la. Esse serviço gerencia e verifica permissões e credenciais antes de conceder acesso aos recursos da API.

## Informações Gerais

* **Base URL (homologação):** [https://api.lya-health-hml.ctctech.link/tenants/](https://api.lya-health-hml.ctctech.link//tenants/)
* **Base URL (produção):** [https://api.lyahealth.com.br/tenants/](https://api.lyahealth.com.br//tenants/)
* **Formato de Respostas:** JSON
* **Versão da API:** v1
* **Status da API:** Ativa

## **Validação de autenticação**

Para verificar a validade do token de acesso, utilize o endpoint abaixo. Essa verificação permite garantir que o token está ativo e autorizado para acessar os serviços da API.

#### Endpoint

Método: `GET`
Rota: `/validate/`

#### Exemplo de Requisição

```bash
curl -X GET "https://api.lyahealth.com.br/tenants/validate/" \
     -H "Authorization: Bearer SEU_TOKEN_AQUI"
```

Se o token for válido, a resposta será um código de sucesso com as informações associadas ao acesso. Caso contrário, a resposta indicará um erro de autenticação.
