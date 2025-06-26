---
title: Art. 7º – Hipóteses Legais para o Tratamento
parent: Visão Geral
nav_order: 2
---

# ⚖️ Art. 7º – Hipóteses Legais para o Tratamento de Dados

<style>
  html { font-size: 125%; }
</style>

> Nenhum dado pode ser tratado sem estar vinculado a uma base legal válida.  
> O Art. 7º apresenta os **fundamentos jurídicos** que autorizam esse tratamento.

<div style="border-left: 4px solid #4a90e2; padding: 0.8em 1em; background-color: #f5f8fa;">
  O Art. 7º lista <strong>dez hipóteses legais</strong>.  
  Toda coleta, uso ou compartilhamento de dados pessoais deve estar coberto por uma delas.
</div>

---

## 👨‍💻 Impacto para desenvolvedores

Ignorar a base legal **quebra todo o compliance**; portanto o dev precisa:

- Vincular cada fluxo de dados a uma hipótese (campo `legal_basis`);
- Gravar logs que provem quando/por que o dado foi tratado;
- Ajustar retenção e revogação de acordo com a base escolhida;
- Reavaliar a base legal sempre que a finalidade mudar.

---

## 🔎 O que o Art. 7º exige?

| Hipótese (inciso)         | Quando usar             | Pontos críticos                                  |
| ------------------------- | ----------------------- | ------------------------------------------------ |
| I. Consentimento          | Newsletter, cookies     | Deve ser específico e revogável                  |
| II. Obrigação legal       | Notas fiscais           | Não exige consentimento, mas exige registro      |
| III. Políticas públicas   | Sistemas governamentais | Base definida em lei/convênio oficial            |
| IV. Pesquisa              | Estudos acadêmicos      | Dados devem ser anonimizados sempre que possível |
| V. Execução de contrato   | Entregas, suporte       | Provar a relação contratual                      |
| VI. Exercício de direitos | Processos judiciais     | Guardar documentos comprobatórios                |
| VII. Proteção da vida     | Emergências médicas     | Registrar motivo e duração do uso                |
| VIII. Tutela da saúde     | Prontuários             | Respeitar sigilo profissional                    |
| IX. Legítimo interesse    | Prevenção a fraudes     | Precisa de RIPD e balança de interesses          |
| X. Proteção do crédito    | Consulta a bureaus      | Limitar escopo ao necessário                     |

---

## 💡 Boas Práticas para cada hipótese

### 1. Definir a base legal **desde o design**

- 🔍 Campo obrigatório `legal_basis` em formulários & APIs.
- 🗂️ Tabela de rastreio:

```sql
CREATE TABLE data_purpose_log (
  id SERIAL PRIMARY KEY,
  user_id INTEGER REFERENCES users(id),
  legal_basis VARCHAR(30) NOT NULL,
  specific_purpose TEXT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 2. Consentimento (inciso I) com segurança

- ☑️ Checkbox desmarcado por padrão;
- 📜 Termo separado e claro;
- 🔄 Endpoint de revogação sempre disponível:

```js
app.post("/consent/revoke", async (req, res) => {
  const { userId } = req.body;
  await db("consents")
    .where({ user_id: userId, revoked_at: null })
    .update({ revoked_at: new Date() });
  res.status(200).send({ status: "revogado" });
});
```

### 3. Outras hipóteses: como aplicar com segurança

| ⚙️ Hipótese          | 💡 Como programar                                  |
| -------------------- | -------------------------------------------------- |
| Obrigação legal      | Registre automaticamente, sem exigir consentimento |
| Execução de contrato | Log de aceite com versão/documento assinado        |
| Legítimo interesse   | Exija produção de um RIPD antes da implementação   |

---

## 🎯 Conclusão

O Art. 7º é o **ponto de partida jurídico** de qualquer sistema que trata dados pessoais.  
Seu papel como dev é garantir que:

1. Cada dado possua uma base legal explícita;
2. A implementação respeite os requisitos de cada hipótese;
3. Logs e provas estejam sempre à mão em caso de auditoria.

> 🔐 **Privacidade não é só lei, é qualidade de software.**
