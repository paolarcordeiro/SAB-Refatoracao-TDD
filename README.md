# Relatório de Refatoração – Tarefa Coursera

## Contexto
Este repositório apresenta a refatoração do método `registraUsuario` da classe `Biblioteca`.  
O objetivo foi melhorar a **legibilidade**, reduzir a **complexidade condicional** e tornar o código mais simples de manter, **sem alterar o comportamento externo**, conforme os princípios de refatoração descritos por Martin Fowler.

---

## Código Original (Antes da Refatoração)
O código original apresentava o mau cheiro de **Complexidade Condicional**, caracterizado por múltiplos níveis de `if` aninhados (código em escada), o que dificultava a leitura e a manutenção.


---

## Técnica de Refatoração Aplicada
- Replace Nested Conditional with Guard Clauses
- Aplicação do princípio fail-fast, tratando os casos inválidos logo no início do método
- Redução do aninhamento e maior clareza do fluxo principal


---

## Código Final (Depois da Refatoração)
- Após a refatoração, o método passou a utilizar cláusulas de guarda, tornando o fluxo principal mais simples, direto e legível.

