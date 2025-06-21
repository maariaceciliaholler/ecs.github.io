# Bases Legais e Consentimento (Art. 7º a 10º da LGPD)

## Introdução
Os artigos 7º a 10º da LGPD estabelecem as **bases legais** que autorizam o tratamento de dados pessoais. Isso significa que **todo sistema ou formulário que coleta dados deve se apoiar em uma dessas bases**.

## Artigo 7º – Bases Legais para o Tratamento

Este artigo define **10 hipóteses** em que o tratamento é permitido, como:

- Consentimento do titular
- Cumprimento de obrigação legal
- Execução de contrato
- Exercício regular de direitos
- Proteção da vida
- Legítimo interesse etc.

### O que isso significa para você, desenvolvedor?

Você precisa garantir que **cada coleta de dado em formulários esteja associada a uma base legal clara**. E mais: **documentar essa justificativa no backend**, para fins de auditoria e transparência.

---

## Validação em Formulários

### 1. Consentimento (base mais usada)

**Boas práticas:**

- Checkbox desmarcado por padrão
- Link para Política de Privacidade
- Explicação clara da finalidade
- Registro do consentimento com data/hora

**Exemplo:**

```html
<form>
  <label for="email">E-mail:</label>
  <input type="email" id="email" name="email" required>

  <p>Concordo com o uso dos meus dados para envio de ofertas:</p>
  <label>
    <input type="checkbox" name="consent" required>
    Li e concordo com a <a href="/privacidade">Política de Privacidade</a>
  </label>

  <button type="submit">Enviar</button>
</form>
