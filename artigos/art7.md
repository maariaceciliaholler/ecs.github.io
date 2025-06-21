---
title: Art. 7º – Bases Legais
parent: Visão Geral     # aparece como filho do index
nav_order: 2            # posição na lista
---

# Art. 7º – Bases Legais para o Tratamento

:::info
**Texto legal (caput):**  
“O tratamento de dados pessoais somente poderá ser realizado nas seguintes hipóteses…”
:::

## O que diz a lei — resumo rápido

| Inciso | Hipótese | Cenário comum em sistemas |
| ------ | -------- | ------------------------- |
| I | Consentimento | Newsletter, cookies de marketing |
| II | Obrigação legal | Emissão de nota fiscal |
| III | Políticas públicas | Sistemas de prefeitura, e-Social |
| IV | Pesquisa | Universidades, IBGE |
| V | Execução de contrato | E-commerce processando endereço de entrega |
| VI | Exercício de direitos | Armazenar provas em processos judiciais |
| VII | Proteção da vida | Emergências médicas |
| VIII | Tutela da saúde | Prontuário eletrônico |
| IX | Legítimo interesse | Prevenção a fraudes (com avaliação de RIPD) |
| X | Proteção do crédito | Consulta ao SCPC/Serasa |

## Checklist de implementação

- [ ] Associar **cada campo** do formulário a uma destas bases.  
- [ ] Registrar no banco (`legal_basis_log`) quem coletou, quando e por quê.  
- [ ] Disponibilizar política de privacidade citando todos os incisos usados.  
- [ ] Revisar anualmente se a base legal ainda é válida para aquela finalidade.

## Exemplo de código (Node.js + PostgreSQL)

```js
// salvando base legal ao criar usuário
await db('users').insert({
  email,
  legal_basis: 'consent',        // art. 7º, I
  basis_detail: 'newsletter',
  consented_at: new Date()
});

CREATE TABLE legal_basis_log (
  id SERIAL PRIMARY KEY,
  user_id INT REFERENCES users(id),
  basis VARCHAR(20),          -- ex.: consent, contract, legitimate_interest
  detail TEXT,
  logged_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

