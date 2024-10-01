De início, precisamos colocar nossas informações acerca do método `AdicionaFilme()` em nossa classe `FilmeController` como comentário seguindo o padrão XML:

```csharp
/// <summary>
    /// Adiciona um filme ao banco de dados
    /// </summary>
    /// <param name="filmeDto">Objeto com os campos necessários para criação de um filme</param>
    /// <returns>IActionResult</returns>
    /// <response code="201">Caso inserção seja feita com sucesso</response>
    [HttpPost]
    [ProducesResponseType(StatusCodes.Status201Created)]
    public IActionResult AdicionaFilme(
        [FromBody] CreateFilmeDto filmeDto)
    {
    //código omitido
```

Em seguida, precisamos alterar a nossa chamada do método `AddSwagger()` em nossa classe `Program.cs`:

```csharp
builder.Services.AddSwaggerGen(c =>
{
    c.SwaggerDoc("v1", new OpenApiInfo { Title = "FilmesAPI", Version = "v1" });
    var xmlFile = $"{Assembly.GetExecutingAssembly().GetName().Name}.xml";
    var xmlPath = Path.Combine(AppContext.BaseDirectory, xmlFile);
    c.IncludeXmlComments(xmlPath);
});
```

Por fim, altere seu `<PropertyGroup>` no arquivo `FilmesApi.csproj`:

```xml
  <PropertyGroup>
    <TargetFramework>net6.0</TargetFramework>
    <Nullable>enable</Nullable>
    <ImplicitUsings>enable</ImplicitUsings>
    <GenerateDocumentationFile>true</GenerateDocumentationFile>
  </PropertyGroup>
```

Com isso, nosso método `AdicionaFilme()` estará devidamente documentado, informando os parâmetros recebidos, tipo de resposta e padrões implementados. Como desafio, faça sua própria documentação para os métodos de leitura, atualização e escrita!