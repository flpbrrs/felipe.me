---
tags:
  - dotNet
  - setup
data de criação: 2024-09-24
---
## Criando um projeto .NET

Através da IDE do Visual Studio podemos usar modelos que permitem uma criação facilitada de uma API .NET, nesse caso usamos o modelo: *API Web do ASP.NET Core.*

Nesse arquivos encontramos alguns arquivos:

- `program.cs`: Arquivo base da aplicação, semelhante ao main;
- `appsettings.json`: Arquivo de entrada da aplicação, aqui serão definidos algumas informações que serão carregadas na aplicação, como por exemplo conexões com o banco de dados
- `properties/launchSettings.json`: Arquivo que armazena os nossos profiles, podemos definir as variáveis de ambiente, propriedades de execução, endereço do host, etc;

## Exemplos de entidades no contexto .NET:

**Modelo**
```C#
namespace FilmeApi.Models;

public class Filme
{
    public string titulo { get; set; }
    public string genero {  get; set; }

    public int duracao { get; set; }
}
```

**Controller**
```C#
using FilmeApi.Models;
using Microsoft.AspNetCore.Mvc;

namespace FilmeApi.Controllers;

[ApiController]
[Route("[controller]")]
public class FilmeController : ControllerBase
{
    private static List<Filme> filmes = new List<Filme>();

    [HttpPost]
    public void registraFilme([FromBody] Filme filme) {
        filmes.Add(filme);
    }
}
```

>[!tip] Template string: $"{parâmetro} string";
>

## Validando parâmetros recebidos

O .NET usa o sistema de notações para marcar os parâmetros de uma classe e assim atribuir limitações aos parâmetros de uma classe. Algumas dessas tags podem receber parâmetros e atributos como mensagens de erros.

```C#
[Required(ErrorMessage = "Esse campo é obrigatório")]
public string name;
```

## Adicionando paginação a consultas

Para realizarmos consultas podemos usar os métodos de classes que implementam a interface `IEnumerable`, sendo eles: `Skip` e `Take`.

```C#
[HttpGet]
public IEnumerable<Filme> buscarTodosFilmes(
    [FromQuery] int skip = 0,
    [FromQuery] int take = 5
)
{
    return filmes
            .Skip(take * skip) // O skip sempre tem que vir antes
            .Take(take)
            .ToArray();
}
```

## Conectando com banco de dados

Podemos fazer uso de pacotes para conectar nossa aplicação a um banco de dados.

Para instalar um pacote devemos usar o `NuGet` no caminho: *Ferramentas > Gerenciar pacotes do NuGet > Gerenciar pacotes do Nuget  da solução*

Os pacotes para lidar com banco de dados são:
- `EntityFrameworkCore`
- `EntityFrameworkTools`

Agora, com os pacotes instalados, devemos começar a criar os nossos contextos relativos a nossa aplicação, que serão classes que farão a relação entre as classes C# e as entidades do banco.

Depois de feita a configuração, como no exemplo [[Conectando .NET ao SQL Server]], podemos usar o conceito de migrações para criar as tabelas no nosso bando de dados:

### Criando as migrações:

Devemos rodar um comando no terminal da aplicação, acessado via: `ferramentas > Gerenciador de pacotes do Nuget > Console do gerenciador de pacotes`

```shell
Add-Migration <nome-da-migration>
```

### Rodando as migrações:

No mesmo console, usamos o seguinte comando:

```shell
Update-Database
```

## Usando o banco de dados

Agora que temos nosso banco devemos alterar o nosso código para usar o banco.

Devemos atualizar nossa Controller para fazer uso do nosso contexto.

```C#
// Os nosso dados serão acessados via contexto
private FilmesContext _context;

// Que por usa vez será injetado no controlador
public FilmesController(FilmesContext context)
{
    _context = context;
}

[HttpPost]
public IActionResult RegistraFilme([FromBody] Filme filme)
{
	// Agora acessamos o nosso Enumerable via contexto
    _context.filmes.Add(filme);
    // Sendo necessário salvar sempre que alteramos algo...
    _context.SaveChanges();

    return CreatedAtAction(
        nameof(BuscarFilmePorId),
        new { filme.id },
        filme
     );
}
```

## Usando AutoMapper e DTOS

Não é um boa prática ficar transitando nossos objetos de negócio dentro da nossa aplicação, por isso uma boa prática é o uso de DTOs (*Data Transfer Objects*). Esses objetos serão usados para a única função de transitar dados, e dessa forma, não precisam ter um complexidade muito grande como os nossos objetos de valor. Deixando assim o uso direto dos nossas classes para os artefatos adequados.

Nesse contexto, surge a necessidade de mapear os nossos DTOs para as nossas classes de negócio. E, por isso, surge a necessidade do uso do AutoMapper, biblioteca para o mapeamento de entidades.

Para instala-lo podemos seguir o caminho padrão: `ferramentas > Gerenciador de pacotes do Nuget > Console do gerenciador de pacotes`

E para fazer uso seguimos os seguintes passos:

- Adicionar a referência do AutoMapper no `program.cs`:
```C#
builder.Services.AddAutoMapper(AppDomain.CurrentDomain.GetAssemblies());
```

- Criar o nosso arquivo de DTO `/DTOS`:
```C#
using System.ComponentModel.DataAnnotations;

namespace FilmesApi.DTOs
{
    public class CreateFilmeDTO
    {
        [Required(ErrorMessage = "O campo titulo é obrigatório")]
        public string titulo { get; set; }
        [Required(ErrorMessage = "O campo gênero é obrigatório")]
        [StringLength(50, ErrorMessage = "O tamando máximo é de 50 caracteres")]
        public string genero { get; set; }
        [Required(ErrorMessage = "O campo duração é obrigatório")]
        [Range(0, 200, ErrorMessage = "O tamanho deve ter entre 0 e 200")]
        public int duracao { get; set; }
    }
}
```

- Criar o profile de mapeamento do DTO `/Profiles`:
```C#
using AutoMapper;
using FilmesApi.DTOs;
using FilmesApi.Models;

namespace FilmesApi.Profiles;

public class FilmeProfile : Profile
{
    public FilmeProfile() {
	    /* Sempre que for criado um DTO que deve ser mapeado para filme outra linha de mapper deve ser adicionada */
        CreateMap<CreateFilmeDTO, Filme>();
    }
}
```

- Atualizar a nossa Controller para usar o Mapper e o DTO:
```C#
using AutoMapper;
using FilmesApi.Data;
using FilmesApi.DTOs;
using FilmesApi.Models;
using Microsoft.AspNetCore.Mvc;

namespace FilmesApi.Controllers
{
    [ApiController]
    [Route("[controller]")]
    public class FilmesController : ControllerBase
    {
        private FilmesContext _context;
	    
	    /* Adicionando o Mapper por injeção de dependência */
        private IMapper _mapper;

        public FilmesController(FilmesContext context, IMapper mapper)
        {
            _context = context;
            _mapper = mapper;
        }

        [HttpPost]
        public IActionResult RegistraFilme([FromBody] CreateFilmeDTO filmeDTO)
        {
	        /* Fazendo uso do Mpper */
            Filme filme = _mapper.Map<Filme>(filmeDTO);

            _context.filmes.Add(filme);
            _context.SaveChanges();

            return CreatedAtAction(
                nameof(BuscarFilmePorId),
                new { filme.id },
                filme
             );
        }
    }
}
```

## Usando o verbo Patch com o Newton JSON

Para fazer a criação de uma rota de patch podemos usar o Newton JSON, podemos instala-lo via: `ferramentas > Gerenciador de pacotes do Nuget > Console do gerenciador de pacotes`, instalando a versão da Microsoft.

- Devemos explicita-lo no `program.cs`:
```C#
builder.Services.AddControllers().AddNewtonsoftJson();
```

- Usa-lo na rota Patch:
```C#
[HttpPatch("{id}")]
public IActionResult atualizaParcialFilmePorId(
	int id,
	JsonPatchDocument<UpdateFilmeDTO> patch)
{
    var filmeBuscado = 
	    _context.filmes.FirstOrDefault((filme) => filme.id == id);

    if (filmeBuscado == null) return NotFound();

	/* 
		Essa conversão é de objeto para tipo,
		diferente da objeto para objeto usada anteriormente

		PS: Deve ser adicionado no profile a volta da conversão
	*/
    var filmeParaAtualizar = _mapper.Map<UpdateFilmeDTO>(filmeBuscado);

    patch.ApplyTo(filmeParaAtualizar, ModelState);

    if(!TryValidateModel(filmeParaAtualizar)) return ValidationProblem();

    _mapper.Map(filmeParaAtualizar, filmeBuscado);
    _context.SaveChanges();

    return NoContent();
}
```

- O body da requisição muda um pouco nesse caso:
```JSON
[
    { 
        "op": "replace",
        "path": "/duracao", // Nome do campo a ser atualizado
        "value": 120
    },
    // Aqui podem vir outros objetos relativos a outros campos...
]
```

