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
