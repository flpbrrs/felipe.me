O código que você forneceu é um método para atualizar um filme em um banco de dados usando ASP.NET Core. Vamos analisar passo a passo o que está acontecendo e por que ele funciona.

### 1. Método `HttpPut` e Rota
```csharp
[HttpPut("{id}")]
public IActionResult atualizaFilmePorId(int id, [FromBody] UpdateFilmeDTO filmeDTO)
```
- O atributo `[HttpPut("{id}")]` define que este método responderá a requisições HTTP do tipo PUT, que são geralmente usadas para atualizar recursos no servidor.
- `"{id}"` indica que um parâmetro da URL será usado, que é o `id` do filme que você quer atualizar.
- O parâmetro `id` é o identificador do filme, e `filmeDTO` é um objeto do tipo `UpdateFilmeDTO` que contém as informações para a atualização. O `[FromBody]` indica que os dados do filme serão passados no corpo da requisição.

### 2. Busca do Filme no Banco
```csharp
var filmeBuscado = _context.filmes.FirstOrDefault((filme) => filme.id == id);
```
- Aqui, `_context.filmes` faz parte do contexto de dados (provavelmente uma instância do `DbContext` do Entity Framework).
- A função `FirstOrDefault` busca o primeiro filme na lista de filmes cujo `id` seja igual ao que foi passado na URL. Se não encontrar nenhum filme com aquele `id`, `filmeBuscado` será `null`.

### 3. Verificação de Existência
```csharp
if (filmeBuscado == null) return NotFound();
```
- Caso nenhum filme tenha sido encontrado, o método retorna um `NotFound()`, que corresponde a um código de status HTTP 404, indicando que o recurso (filme) não foi encontrado.

### 4. Atualização do Filme
```csharp
var filmeAtualizado = _mapper.Map(filmeDTO, filmeBuscado);
```
- Aqui, você está usando um `mapper` (provavelmente AutoMapper) para mapear os dados do `UpdateFilmeDTO` para o objeto `filmeBuscado`.
- O método `Map` substitui as propriedades do `filmeBuscado` com os valores correspondentes do `filmeDTO`, sem criar um novo objeto. Isso é importante porque o `filmeBuscado` ainda está sendo rastreado pelo Entity Framework.

### 5. Salvando as Alterações
```csharp
_context.SaveChanges();
```
- O Entity Framework rastreia mudanças nos objetos carregados do banco de dados (como `filmeBuscado`), e quando você chama `SaveChanges`, ele gera e executa as consultas SQL necessárias para salvar as alterações no banco.

### 6. Retorno
```csharp
return NoContent();
```
- Após salvar as alterações, o método retorna um `NoContent()`, que corresponde ao código HTTP 204, indicando que a atualização foi bem-sucedida, mas não há nenhum conteúdo a ser retornado.

### Por que funciona assim?
1. **Rastreamento do Entity Framework:** Ao buscar o filme, o Entity Framework começa a rastrear as mudanças no objeto. Quando as propriedades do filme são atualizadas com o `Mapper`, ele detecta essas alterações.
2. **Eficiência:** A atualização é feita diretamente no objeto recuperado. Você não precisa buscar o filme novamente ou criar um novo objeto.
3. **Mapeamento simplificado:** O AutoMapper permite que você evite fazer atribuições manuais de propriedades, tornando o código mais limpo e fácil de manter.

Essa abordagem funciona bem porque o EF Core é capaz de detectar as mudanças nos objetos rastreados e gerar as consultas SQL adequadas para atualizar os registros no banco de dados.