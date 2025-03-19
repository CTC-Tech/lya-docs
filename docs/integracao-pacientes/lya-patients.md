# Lya Patients

Serviço dedicado à criação e gerenciamento de adaptadores de autenticação para os serviços dos clientes. Ele permite que a Lya utilize as credenciais configuradas para autenticar-se nos sistemas do cliente e recuperar os dados dos pacientes de maneira segura e eficiente.

## Informações Gerais

* **Base URL (homologação):** <https://api.lya-health-hml.ctctech.link/patients/>
* **Base URL (produção):** <https://api.lyahealth.com.br/patients/>
* **Formato de Respostas:** JSON
* **Versão da API:** v1
* **Status da API:** Ativa

## **Validação de autenticação**

Para verificar a validade do token de acesso, utilize o endpoint abaixo. Essa verificação permite garantir que o token está ativo e autorizado para acessar os serviços da API.

#### Endpoint

Método: `GET`
Rota: `/v1/auth/me/`

#### Exemplo de Requisição

```bash
curl -X GET "https://api.lyahealth.com.br/patients/v1/auth/me/" \
     -H "Authorization: Bearer SEU_TOKEN_AQUI"
```

Se o token for válido, a resposta será um código de sucesso com as informações associadas ao acesso. Caso contrário, a resposta indicará um erro de autenticação.
