# Autenticação

## 1. Introdução

A API de Integração de Pacientes utiliza um mecanismo de autenticação baseado em **token de acesso** para garantir a segurança e o controle do uso da API. Todas as requisições aos endpoints protegidos devem incluir um token válido no cabeçalho da requisição.

## 2. Obtenção do Token

O token de acesso será fornecido manualmente aos usuários autorizados. Para solicitar um token, entre em contato com o suporte ou siga as instruções fornecidas pelo administrador do sistema.

## 3. Uso do Token de Acesso

Para autenticar-se na API, é necessário incluir o token de acesso no cabeçalho da requisição HTTP utilizando o formato **Bearer Token**.

### Exemplo de Cabeçalho de Autenticação:

`Authorization: Bearer <token_de_acesso>`

### Exemplo de Requisição Autenticada:

```bash
curl -X GET "https://api.lyahealth.com.br/tenants/validate/" \
     -H "Authorization: Bearer SEU_TOKEN_AQUI" \
     -H "Content-Type: application/json"
```

## 4. Validação do Token

Caso seja necessário verificar a validade do token de acesso e suas permissões, utilize os endpoints disponíveis na seção **"Validação de autenticação"** na documentação técnica dos projetos **Lya Tenants, Lya Patients** e **Lya API**. Essa verificação pode ser utilizada para garantir que o token está ativo e devidamente configurado.

## 5. Considerações Importantes

* O token de acesso deve ser mantido em sigilo e não deve ser compartilhado.
* Tokens inválidos resultarão em erro de autenticação.
* Caso haja problemas com a autenticação, entre em contato com o suporte para verificar a situação do token.

## 6. Contato e Suporte

Se houver dúvidas ou problemas relacionados à autenticação, entre em contato com o suporte [clicando aqui](https://lyahealth.com.br/contato).