# Ignite Elixir - Rocketseat 🚀

## Por que estudar funcional e Elixir?

### Por que Funcional?

- [x] Temos somente funções, e isso é bom!

  Como um chão de fábrica, temos um pipeline com funções que pegam o dado e modelam o dado

- [x] Imutabilidade

  O dado gravado na memória não vai modificar ela. Modificamos a cópia dela. Garantia da integridade do dado. Menos efeito colateral mesmo com vários núcleos acessando os dados ao mesmo tempo.

  - Redução de efeitos colaterais
  - Concorrência e paralelismo

- [x] Mais fácil de testar e crescer a codebase com qualidade
- [x] Vai te tornar um dev melhor!

---

### Por que Elixir?

- [x] Elixir é funcional
- [x] Código simples, explícito e legível

  Além de ser código de alto nível, é forçado a seguir uma guia de estilo muito específica.

- [x] Erlang VM (BEAM)

  Uma linguagem compilada. O código é todo lido, compilado para gerar um binário, então já é possível saber os erros de antemão. É compilado para Erlang, linguagem criada pela Ericsson com alto foco em disponibilidade, escalabilidade e principalmente para atender demandas de telecomunicações.

  - Alta disponibilidade e escalabilidade
  - Em 2018, rodava 90% de todo o tráfego da Internet

- [x] Pode usar todo poder computacional disponível

### Qual é a aplicação?

- [x] Sistemas WEB, backend, frontend ou monolitos
- [x] Nossa trilha terá o foco em backend

---

### iex

Após [instalação](https://elixir-lang.org/install.html), podemos usar o Elixir interativo [iex](https://elixir-lang.org/getting-started/introduction.html#interactive-mode). Basta digitar no terminal:

```bash
$ iex

# Erlang/OTP 23 [erts-11.1.8] [source] [64-bit] [smp:4:4] [ds:4:4:10] [async-threads:1] [hipe] [dtrace]

# Interactive Elixir (1.11.4) - press Ctrl+C to exit (type h() ENTER for help)
#=> iex(1)>
```

Sempre usar aspas duplas para strings. E para interpolação, usamos:

```elixir
x = "fumi"
"cintia #{x}"
#=> "cintia fumi"
```

---

### Modules

Em funcional, não temos classes e objetos. Temos módulos, que são namespaces contendo várias funções.

Ex: o módulo [String](https://hexdocs.pm/elixir/String.html) possui a função [length/1](https://hexdocs.pm/elixir/String.html#length/1). Esse `/1` é a [aridade da função](https://elixir-lang.org/getting-started/modules-and-functions.html#function-capturing), ou seja, quantos argumentos a função recebe. Chamamos a função de um módulo para fazer a operação sobre essa string e não usamos a própria string invocando um método de objeto.

```elixir
String.length("cintia")
#=> 6
```

Podemos consultar a documentação das funções do módulo ao digitar, por exemplo:

```elixir
h String.slice
```

A reatribuição de valor numa variável, o valor novo é gravado em outro endereço de memória.

```elixir
x = "CiNtIa"
x = String.downcase(x)
#=> "cintia"
```

---

### Atoms

[Atoms](https://hexdocs.pm/elixir/Atom.html) são constantes onde o valor da constante é o próprio nome dela. Atoms comuns são `:ok` e `:error`.

Funções como `is_atom(:banana)` ou `div(6, 2)` não estão em módulo, pois são funções do módulo kernel que já estão disponíveis de prontidão para serem utilizadas na biblioteca padrão da linguagem, sem precisar importar.

```elixir
is_atom(:banana)
#=> true

div(6, 2)
#=> 3
```

---

### Listas

[Listas](https://hexdocs.pm/elixir/List.html) são diferentes que arrays convencionais. Listas encadeadas no Elixir. Então o primeiro elemento da lista aponta para o segundo, que aponta para o terceiro. Então, só temos acesso ao primeiro elemento da lista. Por isso, não é possível acessar diretamente `x[0]` em uma lista encadeada como fazemos em arrays.

Usamos uma lista encadeada quando tenho uma coleção de dados e quero percorrer por toda ela. Ela sempre vai ter tempo de acesso linear, e ela tem tamanho de dado dinâmico bastando o último elemento apontar para o próximo. Assim a lista pode crescer indefinidamente.

Lista pode ter dados variados:

```elixir
[1, 2, 4.5, "string"]
#=> [1, 2, 4.5, "string"]
```

Pode ser somada:

```elixir
[1, 2, 3] ++ [4, 5, 6]
#=> [1, 2, 3, 4, 5, 6]
```

Pode ser subtraída:

```elixir
[1, 2, 3] -- [1, 3]
#=> [2]
```

Acessando o primero elemento [hd](https://hexdocs.pm/elixir/Kernel.html#hd/1) de head:

```elixir
hd([1, 2, 3])
#=> 1
```

Acessando o restante dos elementos [tl](https://hexdocs.pm/elixir/Kernel.html#tl/1) de tail:

```elixir
tl([1, 2, 3])
#=> [2, 3]
```

Internamente, o mapeamento ocorre da seguinte forma. Temos uma lista `[1, 2, 3]`, que o final dessa lista aponta para a lista `[4]`, que resulta na lista x que é `[1, 2, 3, 4]`

```elixir
[1, 2, 3] ++ [4]
#=> [1, 2, 3, 4]
```
