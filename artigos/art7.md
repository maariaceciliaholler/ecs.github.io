---
title: Art. 7º – Hipóteses Legais para o Tratamento
parent: Visão Geral
nav_order: 2
---

# ⚖️ Art. 7º – Hipóteses Legais para o Tratamento de Dados

<div style="border-left: 4px solid #4a90e2; padding: 0.8em 1em; background-color: #f5f8fa;">
  O Art. 7º da LGPD apresenta os <strong>fundamentos jurídicos</strong> que autorizam o uso de dados pessoais.<br>
  Nenhum dado pode ser tratado sem estar vinculado a uma base legal válida.
</div>

---

## 🛠️ Como aplicar isso no desenvolvimento?

Antes mesmo de escrever código, é preciso responder:

> ❓ <strong>“Qual é a base legal que justifica esta coleta ou tratamento de dados?”</strong>

Essa decisão influencia:
- 🧾 O que será registrado
- 🔒 Como o dado será armazenado
- ⏳ Por quanto tempo ele será retido
- 🙋 Como o usuário pode interagir com esse dado

---

## 📚 Principais hipóteses e seus contextos

<table style="width:100%; border-collapse: collapse;">
  <thead style="background-color: #e3f2fd;">
    <tr>
      <th style="text-align:left; padding: 8px;">📌 Hipótese (inciso)</th>
      <th style="text-align:left; padding: 8px;">💡 Quando aplicar no sistema?</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>I. Consentimento</td><td>Newsletter, campanhas, cookies</td></tr>
    <tr><td>II. Obrigação legal</td><td>Emissão de nota fiscal, declarações obrigatórias</td></tr>
    <tr><td>III. Políticas públicas</td><td>Sistemas governamentais, convênios</td></tr>
    <tr><td>IV. Pesquisa</td><td>Estudos acadêmicos com anonimização</td></tr>
    <tr><td>V. Execução de contrato</td><td>Entregas, pagamentos, suporte</td></tr>
    <tr><td>VI. Exercício de direitos</td><td>Registro de interações judiciais ou legais</td></tr>
    <tr><td>VII. Proteção da vida</td><td>Emergências, sistemas de saúde</td></tr>
    <tr><td>VIII. Tutela da saúde</td><td>Prontuários, exames clínicos</td></tr>
    <tr><td>IX. Legítimo interesse</td><td>Prevenção a fraudes, marketing interno (com RIPD)</td></tr>
    <tr><td>X. Proteção do crédito</td><td>Consulta ao Serasa, SPC</td></tr>
  </tbody>
</table>

---

## 💻 Aplicações técnicas: o que considerar ao programar

### 1. Vincular tratamento à base legal no banco de dados

```sql
CREATE TABLE data_purpose_log (
  id SERIAL PRIMARY KEY,
  user_id INTEGER REFERENCES users(id),
  legal_basis VARCHAR(30) NOT NULL,
  specific_purpose TEXT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---

### 2. Consentimento: cuidados obrigatórios

- ☑️ Checkbox desmarcado por padrão
- 📅 Registro de data, hora e finalidade
- 🔁 Função para revogação do consentimento

```js
// Exemplo usando Express.js
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

---

### 3. Outras hipóteses: como aplicar com segurança

| ⚙️ Hipótese              | 💡 Como programar |
|--------------------------|------------------|
| Obrigação legal          | Registre automaticamente, sem exigir consentimento |
| Execução de contrato     | Log de aceite com versão/documento assinado |
| Legítimo interesse       | Exija produção de um RIPD antes da implementação |

---

## 🧭 Recomendações para conformidade técnica

| ✅ Recomendação                                  | 🧠 Objetivo                          |
|--------------------------------------------------|-------------------------------------|
| Armazenar base legal por usuário                 | Rastreabilidade                     |
| Isolar finalidades por módulo                    | Clareza e organização do sistema    |
| Permitir auditoria de decisões automáticas       | Transparência e prestação de contas |
| Revisar a base legal a cada nova versão do sistema | Atualização contínua              |

---

## 🎯 Conclusão

O Art. 7º é a **base jurídica central para todo sistema que trata dados pessoais**.  
Sua missão como dev é garantir que **cada etapa técnica esteja amarrada a uma justificativa legal**.

> 🔐 **Privacidade não é só uma questão legal — é uma responsabilidade ética no desenvolvimento.**
