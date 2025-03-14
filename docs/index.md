# Sobre

Bem-vindo à Lya Health API! A definição completa da API pode ser encontrada na página [Definição da API](api.md).

## Autenticação

Nossa API utiliza **Bearer Token** para autenticação. Para acessar os endpoints protegidos, você deve incluir o token no cabeçalho `Authorization` da sua requisição.

## Exemplo de Requisição

Aqui está um exemplo de como realizar uma requisição **GET** autenticada para buscar informações da API:

=== "cURL"
    ```sh
    curl -X GET "https://api.lyahealth.com.br/tenants/validate/" \
         -H "Authorization: Bearer SEU_TOKEN_AQUI"
    ```

=== "Python (requests)"
    ```python
    import requests

    url = "https://api.lyahealth.com.br/tenants/validate/"
    headers = {"Authorization": "Bearer SEU_TOKEN_AQUI"}

    response = requests.get(url, headers=headers)
    print(response.json())
    ```

=== "JavaScript (fetch)"
    ```javascript
    fetch("https://api.lyahealth.com.br/tenants/validate/", {
        method: "GET",
        headers: { "Authorization": "Bearer SEU_TOKEN_AQUI" }
    })
    .then(response => response.json())
    .then(data => console.log(data));
    ```

Agora você está pronto para interagir com a API! 🚀
