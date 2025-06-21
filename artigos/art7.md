---
title: Art. 7º – Hipóteses Legais para o Tratamento
parent: Visão Geral
nav_order: 2
---

## Art. 7º – Hipóteses Legais para o Tratamento de Dados

O artigo 7º da LGPD apresenta os **fundamentos jurídicos** que autorizam o uso de dados pessoais. Isso significa que **todo processamento de dados em um sistema** deve se apoiar em **uma das hipóteses descritas nesse artigo**, sob pena de ilegalidade.

### Interpretação prática: como isso se aplica no desenvolvimento?

A aplicação do Art. 7º começa no momento em que se decide **coletar qualquer tipo de dado** de uma pessoa.  
Antes mesmo de escrever código, é necessário responder:  
> "Qual é a base legal que justifica essa coleta ou esse armazenamento?"

Essa escolha influencia não apenas a **forma de coleta**, mas também os **registros que devem ser salvos**, o **comportamento do sistema** diante de pedidos do usuário e até **regras de retenção**.

---

### Principais hipóteses e seus contextos

| Hipótese (inciso) | Quando aplicar no sistema? |
|-------------------|----------------------------|
| I. Consentimento | Newsletter, campanhas, cookies |
| II. Obrigação legal | Emissão de notas fiscais, declarações obrigatórias |
| III. Políticas públicas | Sistemas de governo e convênios públicos |
| IV. Pesquisa | Estudos acadêmicos com anonimização |
| V. Execução de contrato | Entregas, pagamentos, suporte |
| VI. Exercício de direitos | Registro de interações judiciais ou legais |
| VII. Proteção da vida | Sistemas médicos, emergências |
| VIII. Tutela da saúde | Prontuários, exames clínicos |
| IX. Legítimo interesse | Prevenção a fraudes, marketing interno (com cautela) |
| X. Proteção do crédito | Consulta a bureaus como Serasa, SPC |

---

### Aplicações técnicas: o que considerar ao programar

#### 1. Amarrar o tratamento à hipótese legal no código

- Defina campos como `legal_basis` e `purpose` em suas tabelas principais.
- Documente o motivo de cada base legal em APIs e contratos de serviço.

```sql
CREATE TABLE data_purpose_log (
  id SERIAL PRIMARY KEY,
  user_id INTEGER REFERENCES users(id),
  legal_basis VARCHAR(30) NOT NULL,
  specific_purpose TEXT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

#### 2. Consentimento: cuidados obrigatórios

- Checkbox desmarcado por padrão;
- Registro da data/hora e finalidade específica;
- Função para permitir revogação posterior.

```javascript
// Exemplo Express.js
app.post("/consent", async (req, res) => {
  const { userId, purpose } = req.body;

  await db("consents").insert({
    user_id: userId,
    legal_basis: "consent",
    purpose,
    consented_at: new Date()
  });

  res.status(201).send({ status: "registrado" });
});
```

#### 3. Outras hipóteses – como codificar de forma segura

- **Obrigação legal**: registre a base diretamente, sem exigir consentimento.
- **Contrato**: registre aceite com versão e hash do documento aceito.
- **Legítimo interesse**: exija a produção de um RIPD antes de ativar.

---

### Cuidados recomendados para conformidade

| Recomendação                                   | Finalidade                    |
|------------------------------------------------|-------------------------------|
| Armazenar base legal por usuário               | Rastreabilidade legal         |
| Isolar finalidades por módulo do sistema       | Clareza e segmentação         |
| Permitir auditoria de decisões automáticas     | Transparência regulatória     |
| Validar o uso contínuo da base legal a cada versão | Atualização e aderência    |

---

### Considerações finais

O artigo 7º é o **marco inicial da responsabilidade jurídica sobre os dados**.

Sua função como desenvolvedor(a) é garantir que as decisões técnicas acompanhem a base legal definida — desde o front-end até o banco de dados.

Fazer isso **não é só uma obrigação legal**, mas uma prática essencial de qualidade e ética no desenvolvimento de sistemas.
