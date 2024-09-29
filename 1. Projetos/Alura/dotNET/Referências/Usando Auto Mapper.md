O AutoMapper é uma biblioteca muito utilizada para mapeamento de objetos no .NET, facilitando a conversão de modelos de domínio para DTOs (Data Transfer Objects) e vice-versa, de forma automática. Usar DTOs é uma prática comum quando se quer expor ou transferir apenas um subconjunto de dados, melhorando o desempenho e garantindo segurança.

Vou te mostrar como configurar e utilizar o **AutoMapper 13** para mapear entidades para DTOs em uma API .NET.

### Passo a Passo para usar AutoMapper com DTOs:

#### 1. **Instalar o AutoMapper:**
Primeiro, você precisa instalar o pacote do AutoMapper e sua integração com o ASP.NET Core.

Use o seguinte comando no **NuGet Package Manager**:
```bash
Install-Package AutoMapper.Extensions.Microsoft.DependencyInjection
```

Ou com o **.NET CLI**:
```bash
dotnet add package AutoMapper.Extensions.Microsoft.DependencyInjection
```

#### 2. **Criar os Modelos e DTOs:**

Suponha que você tenha uma entidade chamada `Produto` e você queira expor um `ProdutoDTO` que tenha apenas algumas propriedades do modelo de domínio.

##### Exemplo do modelo `Produto`:
```csharp
public class Produto
{
    public int Id { get; set; }
    public string Nome { get; set; }
    public decimal Preco { get; set; }
    public string Descricao { get; set; }
    public DateTime DataCriacao { get; set; }
}
```

##### Exemplo do DTO `ProdutoDTO`:
```csharp
public class ProdutoDTO
{
    public int Id { get; set; }
    public string Nome { get; set; }
    public decimal Preco { get; set; }
}
```

#### 3. **Configurar o Mapeamento com AutoMapper:**

Você precisará criar uma classe de perfil para definir como os mapeamentos de uma entidade para um DTO devem ocorrer.

##### Criando o `ProdutoProfile`:
```csharp
using AutoMapper;

public class ProdutoProfile : Profile
{
    public ProdutoProfile()
    {
        // Mapeando Produto para ProdutoDTO
        CreateMap<Produto, ProdutoDTO>();

        // Mapeamento reverso, se você precisar
        CreateMap<ProdutoDTO, Produto>();
    }
}
```

Essa classe usa a classe `Profile` do AutoMapper para definir o mapeamento entre `Produto` e `ProdutoDTO`. O mapeamento inverso também pode ser configurado, caso você precise converter de volta do DTO para o modelo de domínio.

#### 4. **Registrar o AutoMapper no Projeto:**

No arquivo `Program.cs` ou `Startup.cs`, você precisa registrar o AutoMapper nos serviços da sua aplicação.

##### No `Program.cs` (para .NET 6 ou superior):
```csharp
var builder = WebApplication.CreateBuilder(args);

// Registrar o AutoMapper
builder.Services.AddAutoMapper(typeof(Program));

// Outros serviços
var app = builder.Build();
```

##### No `Startup.cs` (para versões anteriores ao .NET 6):
```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Registrar o AutoMapper
    services.AddAutoMapper(typeof(Startup));

    // Outros serviços
}
```

#### 5. **Usar o AutoMapper no seu Controller ou Serviço:**

Agora que o AutoMapper está configurado, você pode utilizá-lo dentro de seus controladores ou serviços para mapear objetos de `Produto` para `ProdutoDTO`.

##### Exemplo de uso no Controller:
```csharp
using AutoMapper;
using Microsoft.AspNetCore.Mvc;

[ApiController]
[Route("api/[controller]")]
public class ProdutosController : ControllerBase
{
    private readonly IMapper _mapper;

    public ProdutosController(IMapper mapper)
    {
        _mapper = mapper;
    }

    [HttpGet("{id}")]
    public IActionResult GetProduto(int id)
    {
        // Simulando busca no banco de dados
        var produto = new Produto
        {
            Id = id,
            Nome = "Produto Teste",
            Preco = 99.99M,
            Descricao = "Descrição do produto",
            DataCriacao = DateTime.Now
        };

        // Usando o AutoMapper para converter Produto em ProdutoDTO
        var produtoDTO = _mapper.Map<ProdutoDTO>(produto);

        return Ok(produtoDTO);
    }
}
```

Aqui, o AutoMapper transforma a entidade `Produto` no DTO `ProdutoDTO`, e o retorno da API será apenas com os campos mapeados.

#### 6. **Mapeamento Personalizado (opcional):**

Caso você precise mapear propriedades específicas ou fazer transformações no mapeamento, pode configurar um mapeamento mais detalhado.

##### Exemplo de Mapeamento Personalizado:
```csharp
public class ProdutoProfile : Profile
{
    public ProdutoProfile()
    {
        CreateMap<Produto, ProdutoDTO>()
            .ForMember(dest => dest.Nome, opt => opt.MapFrom(src => src.Nome.ToUpper())) // Nome será em maiúsculo no DTO
            .ForMember(dest => dest.Preco, opt => opt.MapFrom(src => Math.Round(src.Preco, 2))); // Arredondar preço no DTO
    }
}
```

### Resumo:
- O **AutoMapper** facilita a conversão entre entidades e DTOs, especialmente quando você tem muitos campos que precisam ser mapeados.
- Basta definir perfis de mapeamento, configurar o AutoMapper no `Program.cs` ou `Startup.cs`, e usá-lo injetando o serviço `IMapper` nos controladores ou serviços.
- Você pode personalizar o mapeamento, aplicando transformações durante o processo.

Isso te ajudará a manter o código mais limpo e modular, facilitando o uso de DTOs em projetos de APIs ASP.NET Core.