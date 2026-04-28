# Relatório de Refatoração – Tarefa Coursera

## Contexto
Este repositório apresenta a refatoração do método `registraUsuario` da classe `Biblioteca`.  
O objetivo foi melhorar a **legibilidade**, reduzir a **complexidade condicional** e tornar o código mais simples de manter, **sem alterar o comportamento externo**, conforme os princípios de refatoração descritos por Martin Fowler.

---

## Código Original (Antes da Refatoração)
O código original apresentava o mau cheiro de **Complexidade Condicional**, caracterizado por múltiplos níveis de `if` aninhados (código em escada), o que dificultava a leitura e a manutenção.

```java
public void registraUsuario(String nome)
        throws UsuarioJaRegistradoException, UsuarioComNomeVazioException,
        UsuarioInexistenteException {
    if (nome != null) {
        if (!nome.isEmpty()) {
            Usuario usuario = new Usuario(nome);
            if (!_usuarios.contains(usuario)) {
                _usuarios.add(usuario);
            } else
                throw new UsuarioJaRegistradoException("--->Já existe usuário com o nome \""
                        + nome + "\"! Use outro nome!");
        } else
            throw new UsuarioComNomeVazioException("--->Não pode registrar usuario com nome vazio!");
    } else
        throw new UsuarioInexistenteException("--->Não pode registrar usuario inexistente!");
}
```
---

## Lista de Maus Cheiros Identificados
Relacionados aos tipos exercitados na Semana 2 do curso:

1. **Complexidade Condicional (Nested Conditionals):** Trecho com `if` dentro de `if`. 
2. **Cláusulas Else Desnecessárias:** Uso de `else` após comandos de `throw`.
3. **Falta de Clareza:** O fluxo principal de sucesso está oculto por validações aninhadas.

---

## Técnica de Refatoração Aplicada
- Replace Nested Conditional with Guard Clauses
- Aplicação do princípio fail-fast, tratando os casos inválidos logo no início do método
- Redução do aninhamento e maior clareza do fluxo principal


---

## Código Final (Depois da Refatoração)
- Após a refatoração, o método passou a utilizar cláusulas de guarda, tornando o fluxo principal mais simples, direto e legível.

```java
public void registraUsuario(String nome)
        throws UsuarioJaRegistradoException, UsuarioComNomeVazioException,
        UsuarioInexistenteException {
    
    if (nome == null) 
        throw new UsuarioInexistenteException("--->Não pode registrar usuario inexistente!");
    
    if (nome.isEmpty()) 
        throw new UsuarioComNomeVazioException("--->Não pode registrar usuario com nome vazio!");

    Usuario usuario = new Usuario(nome);
    
    if (_usuarios.contains(usuario)) 
        throw new UsuarioJaRegistradoException("--->Já existe usuário com o nome \"" + nome + "\"! Use outro nome!");
    
    _usuarios.add(usuario);
}
```
---

### Evidência de Execução

A imagem abaixo comprova a execução bem-sucedida (estado verde) do método
`registraUsuario(String)` após o ciclo de refatoração, em ambiente online
(JDoodle).


``
<img width="1908" height="962" alt="image" src="https://github.com/user-attachments/assets/26f3a83f-7f44-49c9-b2ff-7b6d56c8211d" />


``
<img width="1903" height="922" alt="image" src="https://github.com/user-attachments/assets/3f80d057-fee3-4099-a215-94477649b493" />




---
