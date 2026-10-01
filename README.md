# Atividade — Tratamento de Erros e Exceções

## Introdução

O tratamento de erros e exceções é um recurso importante na programação porque permite que um sistema identifique situações inesperadas e tome uma atitude adequada. Em vez de deixar que um problema interrompa o programa de maneira inesperada, podemos tratar a situação, apresentar uma mensagem ao usuário ou realizar outra ação necessária.

Neste trabalho, serão apresentados os conceitos de erros, exceções, `try`, `catch`, `finally` e `throw`, utilizando exemplos em TypeScript.

---

# 1. Tratamento de erros e exceções

## O que é tratamento de erros?

Tratamento de erros é o conjunto de técnicas utilizadas para identificar e controlar problemas que podem acontecer durante a execução de um programa.

Um programa pode receber dados inválidos, tentar acessar algo que não existe ou realizar uma operação que não é permitida. O tratamento de erros permite que essas situações sejam controladas de forma adequada.

Por exemplo, em um sistema bancário, uma transferência com valor negativo deve ser recusada. Em vez de permitir que o programa continue com um valor inválido, podemos identificar o problema e informar o usuário.

## O que é uma exceção?

Uma exceção é uma situação anormal que acontece durante a execução de um programa e interrompe o fluxo normal daquela operação.

Em TypeScript, uma exceção pode ser lançada utilizando o comando `throw`. Ela pode ser capturada e tratada utilizando estruturas como `try` e `catch`.

Um exemplo seria tentar dividir um número por zero:

```typescript
function dividir(a: number, b: number): number {
    if (b === 0) {
        throw new Error("Não é possível dividir por zero.");
    }

    return a / b;
}
```

Nesse exemplo, quando `b` é igual a zero, o programa lança uma exceção porque a operação não é válida.

## Qual a diferença entre erro e exceção?

Erro é um problema que pode acontecer em um programa e impedir que ele funcione corretamente. Os erros podem ocorrer por diferentes motivos, como problemas de sintaxe, lógica ou durante a execução.

A exceção é uma ocorrência específica durante a execução que pode ser lançada e tratada pelo programa.

De maneira simples, podemos entender que **erro é o problema e exceção é uma forma de representar e comunicar determinados problemas durante a execução do programa, permitindo que sejam tratados**.

## Por que é importante tratar erros e exceções?

O tratamento de erros e exceções é importante porque:

* evita que o programa seja encerrado inesperadamente;
* permite apresentar mensagens claras ao usuário;
* impede que operações inválidas sejam realizadas;
* facilita a identificação de problemas;
* aumenta a confiabilidade do sistema;
* permite que o programa tome uma ação adequada diante de uma situação inesperada.

## Exemplo em TypeScript

```typescript
function dividir(a: number, b: number): number {
    if (b === 0) {
        throw new Error("Não é possível dividir por zero.");
    }

    return a / b;
}

try {
    const resultado = dividir(10, 0);
    console.log("Resultado:", resultado);
} catch (erro) {
    console.log("Erro:", (erro as Error).message);
}
```

Nesse código, a função `dividir` verifica se o segundo número é zero. Caso seja, o `throw` lança uma exceção.

A exceção é capturada pelo `catch`, que exibe a mensagem de erro.

---

# 2. Tratamento de exceções

O tratamento de exceções tem como finalidade controlar situações inesperadas que acontecem durante a execução de um programa.

Quando uma exceção ocorre, podemos impedir que ela cause uma interrupção inesperada do programa. Para isso, utilizamos estruturas como `try` e `catch`.

O `try` contém o código que pode gerar uma exceção. Caso uma exceção aconteça, a execução do `try` é interrompida e o `catch` é executado.

## Exemplo em TypeScript utilizando `try` e `catch`

```typescript
function verificarIdade(idade: number): void {
    if (idade < 18) {
        throw new Error("A pessoa deve ter 18 anos ou mais.");
    }

    console.log("Acesso permitido.");
}

try {
    verificarIdade(16);
} catch (erro) {
    console.log("Erro:", (erro as Error).message);
}
```

### Funcionamento

Primeiro, a função `verificarIdade` recebe o valor `16`.

Dentro da função, existe uma verificação:

```typescript
if (idade < 18)
```

Como `16` é menor que `18`, o programa executa:

```typescript
throw new Error("A pessoa deve ter 18 anos ou mais.");
```

O `throw` lança uma exceção. Como a função foi chamada dentro de um bloco `try`, a exceção é capturada pelo `catch`.

O `catch` então apresenta a mensagem:

```text
Erro: A pessoa deve ter 18 anos ou mais.
```

Assim, o erro é tratado de maneira controlada.

---

# 3. `try`, `catch` e `finally`

As estruturas `try`, `catch` e `finally` são utilizadas em conjunto para controlar exceções.

## `try`

O `try` contém o código que pode gerar uma exceção.

```typescript
try {
    // código que pode gerar uma exceção
}
```

Quando uma exceção acontece dentro do `try`, sua execução é interrompida e o controle passa para o `catch`.

## `catch`

O `catch` é responsável por capturar e tratar a exceção gerada dentro do `try`.

```typescript
catch (erro) {
    // tratamento do erro
}
```

Ele pode, por exemplo, mostrar uma mensagem informando o problema.

## `finally`

O `finally` contém código que será executado ao final do processo, independentemente de uma exceção ter acontecido ou não.

Ele pode ser utilizado para realizar alguma ação que deve ocorrer no final de uma operação.

## Exemplo utilizando as três estruturas

```typescript
function dividir(a: number, b: number): number {
    if (b === 0) {
        throw new Error("O divisor não pode ser zero.");
    }

    return a / b;
}

try {
    const resultado = dividir(20, 0);
    console.log("Resultado:", resultado);
} catch (erro) {
    console.log("Erro:", (erro as Error).message);
} finally {
    console.log("Operação finalizada.");
}
```

### Funcionamento

O programa começa executando o bloco `try`.

A função `dividir` recebe `20` e `0`. Como o divisor é zero, a função executa o `throw` e lança uma exceção.

A execução do `try` é interrompida e o `catch` captura a exceção.

Depois disso, o `finally` é executado e mostra:

```text
Operação finalizada.
```

A saída será semelhante a:

```text
Erro: O divisor não pode ser zero.
Operação finalizada.
```

Portanto:

* `try` tenta executar uma operação;
* `catch` trata uma exceção;
* `finally` executa uma ação ao final do processo.

---

# 4. `throw`

O comando `throw` é utilizado para **lançar uma exceção manualmente**.

Ele é útil quando o programa identifica uma situação que não deve continuar.

Por exemplo, podemos verificar se uma idade é válida. Caso seja negativa, podemos lançar uma exceção.

## Exemplo em TypeScript

```typescript
function cadastrarPessoa(nome: string, idade: number): void {
    if (idade < 0) {
        throw new Error("A idade não pode ser negativa.");
    }

    console.log(`Pessoa ${nome} cadastrada com sucesso.`);
}

try {
    cadastrarPessoa("João", -5);
} catch (erro) {
    console.log("Erro ao cadastrar:", (erro as Error).message);
}
```

### Funcionamento

A função `cadastrarPessoa` recebe o nome `"João"` e a idade `-5`.

O programa verifica:

```typescript
if (idade < 0)
```

Como a idade é negativa, o programa executa:

```typescript
throw new Error("A idade não pode ser negativa.");
```

Nesse momento, uma exceção é lançada.

Como a chamada da função está dentro de um `try`, o `catch` captura a exceção e apresenta a mensagem:

```text
Erro ao cadastrar: A idade não pode ser negativa.
```

Portanto, o `throw` permite que o próprio programa identifique uma situação inválida e informe que uma exceção aconteceu.

---

# 5. Aplicação prática — Transferência bancária

Agora será criada uma função para realizar uma transferência bancária.

A função deverá:

* rejeitar valores menores ou iguais a zero;
* rejeitar valores maiores que o saldo disponível;
* lançar uma exceção quando a operação for inválida;
* tratar as exceções utilizando `try` e `catch`.

## Código em TypeScript

```typescript
function transferir(saldo: number, valor: number): number {
    if (valor <= 0) {
        throw new Error(
            "O valor da transferência deve ser maior que zero."
        );
    }

    if (valor > saldo) {
        throw new Error(
            "Saldo insuficiente para realizar a transferência."
        );
    }

    return saldo - valor;
}
```

A função recebe dois valores:

* `saldo`: representa o saldo disponível na conta;
* `valor`: representa o valor que será transferido.

Primeiro, o programa verifica se o valor é menor ou igual a zero:

```typescript
if (valor <= 0)
```

Se for, uma exceção é lançada:

```typescript
throw new Error(
    "O valor da transferência deve ser maior que zero."
);
```

Depois, o programa verifica se o valor da transferência é maior que o saldo:

```typescript
if (valor > saldo)
```

Caso seja, outra exceção é lançada:

```typescript
throw new Error(
    "Saldo insuficiente para realizar a transferência."
);
```

Se nenhuma dessas situações acontecer, a transferência é considerada válida e a função retorna o novo saldo:

```typescript
return saldo - valor;
```

## Situação de erro 1 — Valor menor que zero

```typescript
let saldo = 1000;

try {
    saldo = transferir(saldo, -100);
    console.log("Transferência realizada com sucesso.");
} catch (erro) {
    console.log("Erro:", (erro as Error).message);
}
```

Nesse caso, o saldo é `1000` e o valor da transferência é `-100`.

Como o valor é menor que zero, a condição:

```typescript
if (valor <= 0)
```

é verdadeira.

A função lança uma exceção e o `catch` captura o problema.

A saída será:

```text
Erro: O valor da transferência deve ser maior que zero.
```

O saldo continua sendo `1000`.

---

## Situação de erro 2 — Valor maior que o saldo

```typescript
try {
    saldo = transferir(saldo, 1500);
    console.log("Transferência realizada com sucesso.");
} catch (erro) {
    console.log("Erro:", (erro as Error).message);
}
```

Nesse caso, o saldo é `1000`, mas a transferência é de `1500`.

A condição:

```typescript
if (valor > saldo)
```

é verdadeira.

Por isso, o programa lança a exceção:

```typescript
throw new Error(
    "Saldo insuficiente para realizar a transferência."
);
```

O `catch` captura a exceção e apresenta:

```text
Erro: Saldo insuficiente para realizar a transferência.
```

O saldo continua sendo `1000`.

---

## Situação válida

Também podemos testar uma transferência válida:

```typescript
try {
    saldo = transferir(saldo, 300);
    console.log("Transferência realizada com sucesso.");
    console.log("Novo saldo:", saldo);
} catch (erro) {
    console.log("Erro:", (erro as Error).message);
}
```

Como o saldo é `1000` e a transferência é de `300`, a operação é permitida.

A função retorna:

```text
700
```

A saída será:

```text
Transferência realizada com sucesso.
Novo saldo: 700
```

## Funcionamento geral

O funcionamento da transferência pode ser resumido da seguinte maneira:

1. A função recebe o saldo e o valor da transferência.
2. Verifica se o valor é menor ou igual a zero.
3. Se for, lança uma exceção com `throw`.
4. Caso contrário, verifica se o valor é maior que o saldo.
5. Se for, lança outra exceção.
6. Se nenhuma condição inválida acontecer, calcula o novo saldo.
7. O código que chama a função utiliza `try` para tentar realizar a operação.
8. O `catch` captura qualquer exceção lançada pela função.
9. O usuário recebe uma mensagem explicando o motivo pelo qual a operação não pôde ser realizada.

---

# Conclusão

O tratamento de erros e exceções é importante para desenvolver programas mais seguros, previsíveis e confiáveis. Durante a atividade, foi possível observar que o `throw` pode ser utilizado para lançar uma exceção quando uma situação inválida é identificada.

O `try` é utilizado para executar um código que pode gerar uma exceção, enquanto o `catch` permite capturar e tratar essa exceção. Já o `finally` permite executar uma ação ao final do processo, independentemente de ter ocorrido uma exceção.

No exemplo da transferência bancária, esses recursos foram utilizados para impedir transferências com valores inválidos ou maiores que o saldo disponível. Dessa forma, o programa consegue identificar o problema, interromper a operação inválida e informar ao usuário o motivo do erro.
