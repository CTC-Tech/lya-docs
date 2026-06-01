# Operações em Lote

Os endpoints de operações em lote permitem criar, atualizar e remover múltiplos registros em uma única requisição, evitando o overhead de chamadas individuais em sincronizações com sistemas legados.

## Como funciona

Todos os endpoints bulk recebem um **array de objetos** e retornam um **array de resultados**, onde cada item tem seu próprio status de processamento.

```
requisição  →  [ item1, item2, item3, ... ]
resposta    →  [ { status, data }, { status, error }, ... ]
```

**Comportamento por item:**

- Cada item é processado de forma independente
- Erros em um item não bloqueiam nem afetam os demais
- O índice da resposta corresponde ao índice da requisição

**Limite:** até **300 itens por requisição**.

## Formato da resposta

=== "Sucesso"

    ```json
    {
      "status": "SUCCESS",
      "data": { ... }
    }
    ```

=== "Erro"

    ```json
    {
      "status": "ERROR",
      "data": null,
      "error": "Descrição do erro"
    }
    ```

## Endpoints disponíveis

### Pacientes

| Método | Rota | Descrição |
|--------|------|-----------|
| `POST` | `/organizations/{org_id}/patients/bulk/` | Cria múltiplos pacientes |
| `PATCH` | `/organizations/{org_id}/patients/bulk/` | Atualiza múltiplos pacientes |
| `DELETE` | `/organizations/{org_id}/patients/bulk/` | Remove múltiplos pacientes |

### Resources FHIR

| Método | Rota | Descrição |
|--------|------|-----------|
| `POST` | `/organizations/{org_id}/patients/resources/bulk/` | Vincula múltiplos resources |
| `PATCH` | `/organizations/{org_id}/patients/resources/bulk/` | Atualiza múltiplos resources |
| `DELETE` | `/organizations/{org_id}/patients/resources/bulk/` | Remove múltiplos resources |

## Exemplos

### Criar pacientes em lote

```bash
curl -X POST "https://api.lyahealth.com.br/integration/api/v2/organizations/{org_id}/patients/bulk/" \
     -H "Authorization: Bearer SEU_TOKEN" \
     -H "Content-Type: application/json" \
     -d '[
       {
         "name": "Paciente A",
         "document": "111.111.111-11",
         "document_type": "cpf",
         "metadata_external_id": "EXT-001",
         "birth": "1980-01-01"
       },
       {
         "name": "Paciente B",
         "document": "222.222.222-22",
         "document_type": "cpf",
         "metadata_external_id": "EXT-002",
         "birth": "1990-05-20"
       }
     ]'
```

**Resposta 201:**

```json
[
  { "status": "SUCCESS", "data": { "id": 1, "uuid": "abc-...", "name": "Paciente A", ... } },
  { "status": "ERROR",   "data": null, "error": "Paciente com este metadata_external_id já existe" }
]
```

**Com filtros cirúrgicos (Lya Cirurgia):**

```json
[
  {
    "name": "Paciente Cirúrgico",
    "document": "111.111.111-11",
    "document_type": "cpf",
    "metadata_external_id": "EXT-001",
    "birth": "1975-03-10",
    "sector": "Centro Cirúrgico",
    "consultation_code": "CTX-001",
    "consultation_date": "2024-01-15T08:00:00",
    "filters": [
      {
        "name": "Procedimento Cirúrgico",
        "query_parameter": "surgical_procedure",
        "values": [
          {
            "value": "artroscopia-joelho",
            "title": "Artroscopia de Joelho",
            "procedures": [
              {
                "surgery_code": "30602031",
                "surgery_description": "Artroscopia diagnóstica do joelho",
                "is_primary": true
              }
            ]
          }
        ]
      }
    ]
  }
]
```

---

### Atualizar pacientes em lote

O campo `uuid` é obrigatório em cada item para identificar o paciente a ser atualizado. Os demais campos são opcionais.

```json
[
  { "uuid": "abc123-...", "sector": "Neurologia" },
  { "uuid": "def456-...", "phone_number": "+5511999999999", "weight": 75.0 }
]
```

---

### Remover pacientes em lote

```json
[
  { "uuid": "abc123-..." },
  { "uuid": "def456-..." }
]
```

---

### Vincular resources FHIR em lote

O campo `patient_id` é o **ID numérico** do paciente (campo `id`), não o UUID.

```json
[
  { "patient_id": 1, "url": "https://...observation/?patient_id=1" },
  { "patient_id": 2, "url": "https://...observation/?patient_id=2" }
]
```

---

### Atualizar resources em lote

```json
[
  { "patient_id": 1, "resource_id": 10, "url": "https://nova-url/..." }
]
```

---

### Remover resources em lote

```json
[
  { "patient_id": 1, "resource_id": 10 },
  { "patient_id": 2, "resource_id": 20 }
]
```

## Quando usar

| Cenário | Recomendação |
|---------|-------------|
| Importação inicial do sistema legado | Bulk — envie todos os pacientes de uma vez |
| Sincronização diária incremental | Bulk — processe apenas os registros alterados |
| Atualização de um único paciente em tempo real | Individual (`PATCH /patients/{uuid}/`) |
| Cadastro de paciente durante o atendimento | Individual (`POST /patients/`) |
