# Refatoração: Guard Clauses no método `registraUsuario`

## Contexto
Este repositório contém o exercício de refatoração do método `registraUsuario` da classe `Biblioteca`.

## Antes (código original)
> Cole aqui o código original do método `registraUsuario` (antes da refatoração).

## Mau Cheiro (Code Smell)
- Complexidade Condicional
- Código em Escada (excesso de if/else aninhados)

## Técnica aplicada
- Replace Nested Conditional with Guard Clauses (fail-fast)

## Depois (código refatorado)
```java
public void registraUsuario(String nome)
        throws UsuarioJaRegistradoException, UsuarioComNomeVazioException,
        UsuarioInexistenteException {
    
    // 1. Validação de nulidade (Guarda)
    if (nome == null) {
        throw new UsuarioInexistenteException("--->Não pode registrar usuario inexistente!");
    }

    // 2. Validação de nome vazio (Guarda)
    if (nome.isEmpty()) {
        throw new UsuarioComNomeVazioException("--->Não pode registrar usuario com nome vazio!");
    }

    Usuario usuario = new Usuario(nome);
    
    // 3. Validação de duplicidade (Guarda)
    if (_usuarios.contains(usuario)) {
        throw new UsuarioJaRegistradoException("--->Já existe usuário com o nome \"" 
                + nome + "\"! Use outro nome!");
    }

    // 4. Fluxo principal limpo
    _usuarios.add(usuario);
}# SAB-Refatoracao-TDD
SAB-Refatoracao-TDD
