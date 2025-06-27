---
title: Art. 10º – Uso com base em legítimo interesse
parent: Visão Geral
nav_order: 5
---

# ⚖️ Art. 10º – Uso com base em legítimo interesse

> Permite o tratamento de dados pessoais sem consentimento explícito,
desde que o objetivo seja legítimo, necessário e respeite os direitos do titular.


O Art. 10 da LGPD permite que uma empresa use os dados das pessoas com base no seu interesse legítimo, mesmo sem pedir permissão. No entanto, isso só é permitido se houver um motivo plausível, com uma finalidade clara e específica. Além disso, o uso desses dados não pode prejudicar os direitos ou as expectativas da pessoa dona das informações.

---
## 👨‍💻 Impacto para desenvolvedores
Tratar dados com base em legítimo interesse exige justificativa clara e transparência. Ao contrário do consentimento, essa base legal depende de uma **análise de risco** e da criação de um relatório de impacto quando exigido. Portanto o dev precisa:

- Manter histórico de quem acessou os dados, quando e com qual finalidade  
- Evitar coleta de dados desnecessários em formulários, APIs e bancos  
- Exibir de forma clara a finalidade do uso de dados no sistema (ex: política de privacidade)  
- Garantir que o usuário possa acessar, corrigir ou excluir seus dados pessoais  
- Implementar logs de acesso e uso de dados pessoais  
- Criar mecanismos para informar o usuário em caso de mudança de finalidade  



## 🔎 O que o Art. 10 da LGPD exige?

| Hipótese (inciso/parágrafo) | Quando usar | Pontos críticos |
|-----------------------------|-------------|------------------|
| **I** – Apoio e promoção das atividades do controlador | Quando a empresa precisa usar dados pessoais para ações como marketing, melhoria de serviços ou análise interna | A atividade deve ser legítima, trazer benefício claro para o negócio e o uso dos dados deve ser proporcional e necessário |
| **II** – Proteção dos direitos do titular ou prestação de serviços que o beneficiem | Quando o uso dos dados ajuda o titular diretamente, como em serviços personalizados ou proteção contra fraudes | Deve respeitar as expectativas do titular e garantir que não haja prejuízo aos seus direitos e liberdades |
| **III** – Dados estritamente necessários | Sempre que o uso dos dados for baseado em legítimo interesse | Só pode tratar os dados **mínimos necessários** para atingir a finalidade declarada |
| **IV** – Transparência no tratamento | Durante todo o tratamento de dados baseado em legítimo interesse | É obrigação da empresa informar claramente ao titular por que e como os dados estão sendo usados |
| **V** – Relatório de impacto à proteção de dados | Quando a ANPD solicitar ou o tratamento representar risco relevante aos direitos dos titulares | A empresa deve estar pronta para apresentar documentação clara, respeitando os segredos comercial e industrial |


## 💡 Boas Práticas para Transparência

### 1. Exiba a finalidade do uso dos dados diretamente na interface
- 🔍 Seja transparente: diga por que os dados estão sendo usados.
- 💡 Exemplo: mostrar abaixo de um campo de e-mail —  
  _“Usaremos seu e-mail para enviar ofertas personalizadas com base no seu perfil de compra.”_

---

### 2. Coleta mínima de dados
- ✂️ Só colete o que for realmente necessário para a finalidade informada.
- 💡 Exemplo: se o objetivo é enviar promoções por e-mail, **não peça CPF** ou telefone.

---

### 3. Crie um endpoint para mostrar ao usuário como os dados dele são usados
- 📬 Dê ao usuário acesso fácil às informações sobre o uso dos dados.
- 💡 Exemplo:  
  `GET /meus-dados/info` → retorna:  
  _“Seus dados são usados para: 1) personalizar ofertas; 2) melhorar nossos serviços. Dados compartilhados com: Google Ads.”_

---

### 4. Registre que o usuário foi informado
- 🧾 Guarde evidências de que o usuário viu e foi informado sobre a finalidade.
- 💡 Exemplo: ao mostrar a política de privacidade, registrar:  
  _“Usuário ID 123 aceitou política versão 3.1 em 26/06/2025 às 21:42.”_

---

### 5. Liste com quem os dados são compartilhados
- 🔗 Informe quais empresas/parceiros terão acesso aos dados.
- 💡 Exemplo: exibir na interface ou política:  
  _“Compartilhamos seus dados com Google Analytics e Mailchimp para análise e envio de e-mails.”_

---

## 🎯 Conclusão

O Art. 10 da LGPD permite o uso de dados pessoais **sem consentimento**, desde que haja um **motivo legítimo, necessário e proporcional**.

Seu papel como dev é garantir que:

1. A finalidade seja clara, concreta e realmente necessária;
2. O sistema colete apenas os dados estritamente essenciais;
3. O usuário seja informado de forma acessível e objetiva;
4. Logs e registros comprovem que houve transparência;
5. O uso dos dados respeite as expectativas e os direitos do titular.

> 🧭 **Legítimo interesse não é atalho – é compromisso com ética e propósito.**