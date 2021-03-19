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

---

### Tuplas

Sintaticamente, as tuplas são estruturas de dados muito parecidas com as listas. Ao invés de colchetes `[]`, usa-se chaves `{}`.

A diferença principal é que a tupla é armazenada em endereço contiguamente na memória, ou seja, em endereços de memória um após o outro, seguintes. O que torna possível ter agora o acesso direto aos elementos.

```elixir
{1, 2, 3}
#=> {1, 2, 3}

x = {1, 2, 3, 4, 5, 6, 7, 8}
#=> {1, 2, 3, 4, 5, 6, 7, 8}
elem(x, 4)
#=> 5
```

É possível modificar os elementos. Na tupla `x`, quero colocar `"abacaxi"` na posição `4`:

```elixir
put_elem(x, 4, "abacaxi")
#=> {1, 2, 3, 4, "abacaxi", 6, 7, 8}
```

Como temos endereços contíguos, não podemos ir acrescentando elementos.

```elixir
put_elem(x, 8, "abacaxi")
#=>  ** (ArgumentError) argument error
#        :erlang.setelement(9, {1, 2, 3, 4, 5, 6, 7, 8}, "abacaxi")
```

Como a tupla tem tamanho contíguo, e não é um tamanho dinâmico, não podemos acrescentar um elemento no final.

Toda vez que modificamos uma tupla, criamos uma tupla nova inteira na memória e reservo esse espaço novo na memória.

Por isso, sempre que tivermos um volume de dados muito grande que vai aumentando de tamanho, e tenho que iterar sobre esses dados, usamos a lista ao invés da tupla.

Então, para que utilizamos a tupla?

Vamos criar um arquivo pelo terminal:

```bash
echo 'meu arquivo de texto' > text.txt
```

E vamos usar o `iex` para ler esse arquivo:

```elixir
File.read("text.txt")
#=> {:ok, "meu arquivo de texto\n"}
```

A maior aplicação na tupla são agrupamentos de dados que tem sentido entre si, ou seja, a tupla diz duas informações: a primeira informação `:ok` é que o meu arquivo foi aberto com sucesso e a segunda informação `"meu arquivo de texto\n"` é o conteúdo do arquivo em si.

Ao tentar ler um arquivo inexistente, retornamos uma tupla contendo um `atom` de `:error` e o segundo elemento é um `atom` que simboliza o resultado da operação, ou seja, qual foi o erro que ocorreu. Nesse caso, é o código de arquivo inexistente:

```elixir
File.read("banana.txt")
#=> {:error, :enoent}
```

Usamos muito as tuplas com `:ok` e `:error` para controlar o fluxo de execução das nossas aplicações e também para ser retorno de funções.

O módulo `File` contém a função `read` com e sem exclamação:

```elixir
File.read
#=> read!/1         read/1          read_link!/1    read_link/1
```

Ao chamar a função com exclamação num arquivo inexistente, recebemos uma exceção ao invés de uma tupla:

```elixir
File.read!("banana.txt")
#=> ** (File.Error) could not read file "banana.txt": no such file or directory
#       (elixir 1.11.4) lib/file.ex:355: File.read!/1
```

Quando não temos garantia de sucesso de uma operação, vamos usar as funções sem exclamação, assim, temos a tupla de `:ok` ou `:error` como retorno das funções.
