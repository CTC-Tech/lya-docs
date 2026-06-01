# Lya API

Serviço principal da integração, responsável pelo gerenciamento dos pacientes dentro do sistema. Os pacientes cadastrados por meio desse serviço estarão disponíveis na Lya, permitindo que os profissionais de saúde os selecionem e realizem atendimentos diretamente pela plataforma.

## Informações Gerais

* **Base URL (homologação):** <https://api.lya-health-hml.ctctech.link/integration/api/v2/>
* **Base URL (produção):** <https://api.lyahealth.com.br/integration/api/v2/>
* **Formato de Respostas:** JSON
* **Versão da API:** v2
* **Status da API:** Ativa

## Endpoints Disponíveis

### Ator autenticado

| Método | Rota | Descrição |
|--------|------|-----------|
| `GET` | `/actors/current/` | Identifica o ator autenticado |

### Pacientes

| Método | Rota | Descrição |
|--------|------|-----------|
| `GET` | `/organizations/{org_id}/patients/` | Lista pacientes (paginado) |
| `POST` | `/organizations/{org_id}/patients/` | Cadastra um paciente |
| `POST` | `/organizations/{org_id}/patients/bulk/` | Cadastra até 300 pacientes em lote |
| `GET` | `/organizations/{org_id}/patients/{uuid}/` | Busca um paciente |
| `PATCH` | `/organizations/{org_id}/patients/{uuid}/` | Atualiza um paciente |
| `DELETE` | `/organizations/{org_id}/patients/{uuid}/` | Remove um paciente (soft delete) |
| `PATCH` | `/organizations/{org_id}/patients/bulk/` | Atualiza até 300 pacientes em lote |
| `DELETE` | `/organizations/{org_id}/patients/bulk/` | Remove até 300 pacientes em lote |

### Resources (FHIR)

| Método | Rota | Descrição |
|--------|------|-----------|
| `GET` | `/organizations/{org_id}/patients/resources/` | Lista recursos de todos os pacientes |
| `POST` | `/organizations/{org_id}/patients/{id}/resources/` | Vincula um recurso FHIR |
| `POST` | `/organizations/{org_id}/patients/resources/bulk/` | Vincula até 300 recursos em lote |
| `GET` | `/organizations/{org_id}/patients/{id}/resources/{rid}/` | Busca um recurso |
| `PATCH` | `/organizations/{org_id}/patients/{id}/resources/{rid}/` | Atualiza um recurso |
| `DELETE` | `/organizations/{org_id}/patients/{id}/resources/{rid}/` | Remove um recurso |
| `PATCH` | `/organizations/{org_id}/patients/resources/bulk/` | Atualiza até 300 recursos em lote |
| `DELETE` | `/organizations/{org_id}/patients/resources/bulk/` | Remove até 300 recursos em lote |

### Credenciais de Tenant

| Método | Rota | Descrição |
|--------|------|-----------|
| `GET` | `/organizations/{org_id}/tenant-credentials/` | Lista credenciais |
| `POST` | `/organizations/{org_id}/tenant-credentials/` | Cria credencial |
| `GET` | `/organizations/{org_id}/tenant-credentials/{id}/` | Busca credencial |
| `PATCH` | `/organizations/{org_id}/tenant-credentials/{id}/` | Atualiza credencial |
| `DELETE` | `/organizations/{org_id}/tenant-credentials/{id}/` | Remove credencial |

### Sessões e Configuração

| Método | Rota | Descrição |
|--------|------|-----------|
| `GET` | `/organizations/{org_id}/integration-sessions/` | Lista sessões com sumarização |
| `PATCH` | `/organizations/{org_id}/integration-callback-url/` | Define URL de callback |

> **Nota sobre campos obrigatórios:** ao criar um paciente via integração (`POST /patients/` e `POST /patients/bulk/`), os campos `document`, `document_type`, `metadata_external_id` e `birth` são **obrigatórios**.

> **Nota sobre IDs numéricos:** nos endpoints de resources, `{id}` e `{rid}` são IDs numéricos (campo `id`), não UUIDs.

## **Validação de autenticação**

Para verificar a validade do token de acesso, utilize o endpoint abaixo.

#### Endpoint

Método: `GET`
Rota: `/actors/current/`

#### Exemplo de Requisição

```bash
curl -X GET "https://api.lyahealth.com.br/integration/api/v2/actors/current/" \
     -H "Authorization: Bearer SEU_TOKEN_AQUI"
```

Se o token for válido, a resposta retorna o tipo do ator e seus principals. Caso contrário, retorna erro de autenticação.
