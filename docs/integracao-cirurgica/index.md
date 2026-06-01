# Integração Cirúrgica

## 1. Introdução

A API de Integração Cirúrgica permite que sistemas terceiros cadastrem e gerenciem os **procedimentos cirúrgicos** e **equipes cirúrgicas (providers)** da organização na plataforma Lya. Esses dados são utilizados durante as consultas para pré-popular os campos cirúrgicos da sessão.

## 2. Informações Gerais

* **Base URL (homologação):** <https://api.lya-health-hml.ctctech.link/integration/api/v2/>
* **Base URL (produção):** <https://api.lyahealth.com.br/integration/api/v2/>
* **Formato de Respostas:** JSON
* **Versão da API:** v2

## 3. Endpoints Disponíveis

### Procedimentos Cirúrgicos

| Método | Rota | Descrição |
|--------|------|-----------|
| `GET` | `/organizations/{org_id}/surgical-procedures/` | Lista procedimentos (paginado) |
| `POST` | `/organizations/{org_id}/surgical-procedures/` | Cadastra um procedimento |
| `PATCH` | `/organizations/{org_id}/surgical-procedures/{id}/` | Atualiza um procedimento |
| `DELETE` | `/organizations/{org_id}/surgical-procedures/{id}/` | Desativa um procedimento |

### Equipe Cirúrgica (Providers)

| Método | Rota | Descrição |
|--------|------|-----------|
| `GET` | `/organizations/{org_id}/surgical-providers/` | Lista membros da equipe (paginado) |
| `POST` | `/organizations/{org_id}/surgical-providers/` | Cadastra um membro |
| `PATCH` | `/organizations/{org_id}/surgical-providers/{id}/` | Atualiza um membro |
| `DELETE` | `/organizations/{org_id}/surgical-providers/{id}/` | Desativa um membro |

> **Nota:** O `DELETE` realiza **desativação lógica** (`is_active=false`), o registro não é removido do banco.

## 4. Procedimentos Cirúrgicos

### 4.1 Cadastrar Procedimento

**`POST /organizations/{org_id}/surgical-procedures/`**

#### Campos do corpo da requisição

| Campo | Tipo | Obrigatório | Descrição |
|-------|------|-------------|-----------|
| `surgery_description` | string | ✅ | Descrição do procedimento |
| `surgery_code` | string | — | Código interno do procedimento |
| `sigtap_code` | string | — | Código SIGTAP |
| `sia_procedure_code` | string | — | Código SIA |
| `sih_procedure_code` | string | — | Código SIH |
| `is_active` | boolean | — | Padrão: `true` |

#### Exemplo de requisição

```bash
curl -X POST "https://api.lyahealth.com.br/integration/api/v2/organizations/minha-org/surgical-procedures/" \
  -H "Authorization: Bearer SEU_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "surgery_description": "Colecistectomia laparoscópica",
    "surgery_code": "COL-001",
    "sigtap_code": "0407010074"
  }'
```

#### Exemplo de resposta (`201 Created`)

```json
{
  "id": 1,
  "surgery_description": "Colecistectomia laparoscópica",
  "surgery_code": "COL-001",
  "sigtap_code": "0407010074",
  "sia_procedure_code": null,
  "sih_procedure_code": null,
  "is_active": true,
  "organization_id": 42,
  "created_at": "2026-06-01T10:00:00Z",
  "updated_at": "2026-06-01T10:00:00Z"
}
```

### 4.2 Atualizar Procedimento

**`PATCH /organizations/{org_id}/surgical-procedures/{id}/`**

Todos os campos são opcionais. Apenas os campos enviados serão atualizados.

```bash
curl -X PATCH "https://api.lyahealth.com.br/integration/api/v2/organizations/minha-org/surgical-procedures/1/" \
  -H "Authorization: Bearer SEU_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"sigtap_code": "0407010099"}'
```

### 4.3 Desativar Procedimento

**`DELETE /organizations/{org_id}/surgical-procedures/{id}/`**

Retorna `204 No Content`. O procedimento é marcado como `is_active=false`.

## 5. Equipe Cirúrgica (Providers)

### 5.1 Cadastrar Membro

**`POST /organizations/{org_id}/surgical-providers/`**

#### Campos do corpo da requisição

| Campo | Tipo | Obrigatório | Descrição |
|-------|------|-------------|-----------|
| `provider_name` | string | ✅ | Nome do profissional |
| `activity_type` | string | ✅ | `surgeon` ou `anesthesiologist` |
| `provider_code` | string | — | Código interno |
| `crm_number` | string | — | Número do CRM |
| `activity_code` | string | — | Código de atividade |
| `is_active` | boolean | — | Padrão: `true` |

#### `activity_type` — valores aceitos

| Valor | Descrição |
|-------|-----------|
| `surgeon` | Cirurgião |
| `anesthesiologist` | Anestesiologista |

#### Exemplo de requisição

```bash
curl -X POST "https://api.lyahealth.com.br/integration/api/v2/organizations/minha-org/surgical-providers/" \
  -H "Authorization: Bearer SEU_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "provider_name": "Dr. João Silva",
    "activity_type": "surgeon",
    "crm_number": "CRM/SP 123456"
  }'
```

#### Exemplo de resposta (`201 Created`)

```json
{
  "id": 1,
  "provider_name": "Dr. João Silva",
  "activity_type": "surgeon",
  "provider_code": null,
  "crm_number": "CRM/SP 123456",
  "activity_code": null,
  "is_active": true,
  "organization_id": 42,
  "created_at": "2026-06-01T10:00:00Z",
  "updated_at": "2026-06-01T10:00:00Z"
}
```

### 5.2 Atualizar Membro

**`PATCH /organizations/{org_id}/surgical-providers/{id}/`**

Todos os campos são opcionais. Apenas os campos enviados serão atualizados.

```bash
curl -X PATCH "https://api.lyahealth.com.br/integration/api/v2/organizations/minha-org/surgical-providers/1/" \
  -H "Authorization: Bearer SEU_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"crm_number": "CRM/SP 654321"}'
```

### 5.3 Desativar Membro

**`DELETE /organizations/{org_id}/surgical-providers/{id}/`**

Retorna `204 No Content`. O membro é marcado como `is_active=false`.

## 6. Definição completa da API

A definição OpenAPI completa com todos os schemas e parâmetros de filtro está disponível em:

🔗 [Documentação completa dos endpoints](../api.md)
