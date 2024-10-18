---
tags:
  - dotNet
  - Banco-de-dados
data de criação: 2024-10-08
---
Usaremos o Entity Framework para criar as relações entre os nossos recursos do modelo, para isso precisamos definir muito bem a cardinalidade dessa relação.

# Relacionamento 1:1

No caso de relacionamento 1:1, como exemplo a relação entre endereço e um cinema.

Para explicitar a relação das nossas entidades, vamos adicionar a referência do id da na entidade dependente. Nesse caso, para que cinema exista deve previamente existir um endereço. 

```C#
public class Cinema
{
    ...
    public int EnderecoId { get; set; }
}
```

E além disso, devemos adicionar o parâmetro de virtualização em ambas as classes.

```C#
public class Cinema
{
	...
    public int EnderecoId { get; set; }
    public virtual Endereco Endereco { get; set; }
}

public class Endereco
{
    ...
    public virtual Cinema Cinema { get; set; }
}
```

Com o novo parâmetro, devemos adiciona-los as estruturas de código já existentes:

```C#
public class CreateCinemaDTO
{
    [Required(ErrorMessage = "O campo nome é obrigatório")]
    public string Nome { get; set; }

    public int EnderecoId { get; set; }
}

public class ReadCinemaDTO
{
    public int Id { get; set; }
    public string Nome { get; set; }

    public ReadEnderecoDTO endereco { get; set; }
}
```

Por fim, vamos consolidar as mudanças gerando uma nova migration:

> *Ferramentas > Gerenciador de pacotes do NuGet > Console do gerenciador de pacotes*

```bash
Add-Migration "Cinema e Endereco"

Update-Database
```

Agora temos que ajustar a virtualização da propriedade virtual no momento que buscamos essa instância, que seriam as `lazy properties`.

Inicialmente precisamos do pacote `proxies`, obtendo em:

> *Ferramentas > Gerenciador de pacotes do NuGet > Gerenciar pacotes para a solução...*

E fazendo a configuração no `program.cs`:

```C#
builder.Services.AddDbContext<FilmesContext>(
    opts => opts.UseLazyLoadingProxies().UseSqlServer(
	            builder
		            .Configuration
		            .GetConnectionString("FilmesConnection"
		    )
	)
);
```

O próximo passo é ajustar os nossos Profiles para conseguirmos realizar o mapeamento correto das entidades.

```C#
CreateMap<Entidade, ReadDTO>()
    .ForMember(
        readDTO => readDTO.campoMapeado,
        opt => opt.MapFrom(entidadeOrigem => entidadeOrigem.dadosParaMapear)
    );


// Exemplo
CreateMap<Cinema, ReadCinemaDTO>()
    .ForMember(
        cinemaDTO => cinemaDTO.endereco,
        opt => opt.MapFrom(cinema => cinema.Endereco) // Endereco é a entidade virtual
    );
```
