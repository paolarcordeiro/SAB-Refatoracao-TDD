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

## Identificação de Maus Cheiros
- Mau cheiro: Condicionais Aninhadas (Nested Conditionals)
- Tipo: Complexidade de código e baixa legibilidade
- Impacto: Dificuldade de entendimento, manutenção e evolução do código


## Técnica de Refatoração Aplicada
- Replace Nested Conditional with Guard Clauses
- Aplicação do princípio fail-fast, tratando os casos inválidos logo no início do método
- Redução do aninhamento e maior clareza do fluxo principal


## Código Final (Depois da Refatoração)
- Após a refatoração, o método passou a utilizar cláusulas de guarda, tornando o fluxo principal mais simples, direto e legível.

public void registraUsuario(String nome)
        throws UsuarioJaRegistradoException, UsuarioComNomeVazioException,
        UsuarioInexistenteException {
    
    if (nome == null) 
        throw new UsuarioInexistenteException("--->Não pode registrar usuario inexistente!");
    
    if (nome.isEmpty()) 
        throw new UsuarioComNomeVazioException("--->Não pode registrar usuario com nome vazio!");

    Usuario usuario = new Usuario(nome);
    
    if (_usuarios.contains(usuario)) 
        throw new UsuarioJaRegistradoException(
            "--->Já existe usuário com o nome \"" + nome + "\"! Use outro nome!"
        );
    
    _usuarios.add(usuario);
}
