---
title: Art. 8º – Regras para o Consentimento
parent: Visão Geral
nav_order: 3
---

# ✅ Art. 8º – Regras para o Consentimento

> O consentimento deve ser claro, destacado, específico e revogável.  
> Cabe ao controlador **provar que ele foi dado livremente**.

<div style="border-left: 4px solid #4a90e2; padding: 0.8em 1em; background-color: #f5f8fa;">
  O Art. 8º da LGPD define <strong>como deve ser obtido, documentado e revogado o consentimento</strong> do titular.  
  Ele proíbe o uso de cláusulas genéricas, exige destaque em contratos e impõe que o titular seja informado sempre que houver mudanças nas finalidades.
</div>

---

## 👨‍💻 Impacto para desenvolvedores

Consentimento mal coletado ou mal documentado é **um dos maiores riscos jurídicos**. Isso afeta formulários, bancos de dados, contratos e APIs.

Você será responsável por garantir que:

- O consentimento tenha sido dado de forma inequívoca;
- Ele esteja registrado de forma rastreável;
- O usuário consiga revogar facilmente sua autorização;
- Nenhuma mudança de finalidade ocorra sem nova autorização.

---

## 🔎 O que o Art. 8º exige?

| Dispositivo | Interpretação técnica |
|-------------|------------------------|
| §1º | Consentimento escrito deve estar **em cláusula separada** no contrato |
| §2º | **Você precisa guardar a prova** de que houve consentimento válido |
| §3º | É **proibido** tratar dados com base em consentimento obtido com vício (pressão, engano, etc.) |
| §4º | Autorização genérica = inválida. Sempre cite **a finalidade exata** |
| §5º | O titular pode revogar **a qualquer momento**, e isso deve ser fácil |
| §6º | Se mudar a finalidade, o titular deve ser informado e pode revogar |

---

## 💡 Boas Práticas para Consentimento

### 1. Coleta clara e destacada

- ☑️ Checkbox **desmarcado por padrão**;
- 🧾 Termo de consentimento visível e separado;
- 📅 Registro de data, finalidade e forma de coleta.

```html
<!-- Exemplo de coleta explícita -->
<label>
  <input type="checkbox" name="consent" required>
  Concordo com o uso dos meus dados para envio de ofertas personalizadas.
</label>
```

---

### 2. Registro da manifestação de vontade

- 🔐 Guarde a evidência do consentimento (data, IP, finalidade, hash do termo);
- 🗃️ Utilize tabelas específicas para controle de consentimento;

```sql
CREATE TABLE consents (
  id SERIAL PRIMARY KEY,
  user_id INTEGER REFERENCES users(id),
  purpose TEXT NOT NULL,
  consented_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  revoked_at TIMESTAMP,
  consent_hash TEXT
);
```

---

### 3. Revogação facilitada

- 🔄 O usuário precisa conseguir revogar **sem burocracia**;
- 📩 Links de cancelamento em comunicações;
- 📲 Botões de revogação no painel do usuário.

```js
// Endpoint de revogação de consentimento
app.post("/consent/revoke", async (req, res) => {
  const { userId } = req.body;

  await db("consents")
    .where({ user_id: userId, revoked_at: null })
    .update({ revoked_at: new Date() });

  res.status(200).send({ status: "revogado" });
});
```

---

### 4. Atualização de consentimento

- 🔁 Caso a finalidade mude, **informe claramente** o usuário;
- ❌ Se o usuário discordar, **revogue o consentimento antigo**;
- 🧩 Registre qual versão do termo foi aceita.

---

## 🎯 Conclusão

O Art. 8º transforma o consentimento em um **instrumento técnico e jurídico poderoso — mas frágil** se mal implementado.

Como dev, você deve garantir que ele seja:

- 📌 Específico e destacado;
- 🔄 Revogável e controlável;
- 🧾 Documentado e rastreável.

> ❗ A responsabilidade é de quem coleta e também de quem codifica.
