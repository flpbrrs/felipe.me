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

