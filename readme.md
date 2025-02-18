<h1 align="center">
  <br />
  <img
    src="./_docs/assets/icon.png"
    alt="Mega Man Robots API"
    width="150"
  />
  <br />
  <b>Mega Man Robots API</b>
  <br />
  <sub
    ><sup><b>(MEGA-MAN-ROBOTS)</b></sup></sub
  >
  <br />
  <a
    href="https://github.com/felipeAguiarCode/MegaApiDotnetCore/actions/workflows/build.yml"
  >
    <img
      src="https://github.com/felipeAguiarCode/MegaApiDotnetCore/actions/workflows/build.yml/badge.svg"
      alt=""
    />
  </a>
  <a href="https://github.com/felipeAguiarCode/MegaApiDotnetCore/releases/latest">
    <img
      src="https://img.shields.io/github/v/release/felipeAguiarCode/MegaApiDotnetCore"
      alt="Latest Release"
    />
  </a>
</h1>
## Descrição

Megaman API é um projeto desenvolvido em **.NET Core 3.1** que fornece informações sobre os chefes (*bosses*) do jogo Megaman. O objetivo é disponibilizar um backend que fornece JSONs com informações detalhadas sobre os personagens.

Exemplo de resposta da API:

json
{
  "Id": 1,
  "Code": "DLN/DRN-003",
  "Name": "Cutman",
  "HP": 150,
  "Picture": "https://vignette.wikia.nocookie.net/megaman/images/2/22/Cutman.png"
}


## Tecnologias Utilizadas
- **[ASP.NET Core 3.1](https://dotnet.microsoft.com/en-us/download/dotnet/3.1)** - Framework para desenvolvimento da API.
- **[Entity Framework Core](https://docs.microsoft.com/en-us/ef/core/)** - ORM para interação com o banco de dados.
- **[SQL Server](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)** - Banco de dados utilizado.
- **[Newtonsoft.Json](https://www.newtonsoft.com/json)** - Biblioteca para manipulação de JSON.

## Dependências

| Dependência | Versão | Descrição |
|--------------|---------|-------------|
| [Microsoft.EntityFrameworkCore](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore/3.1.8) | 3.1.8 | ORM para manipulação do banco de dados. |
| [Microsoft.EntityFrameworkCore.Design](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Design/3.1.8) | 3.1.8 | Ferramentas de design do Entity Framework Core. |
| [Microsoft.EntityFrameworkCore.SqlServer](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.SqlServer/3.1.8) | 3.1.8 | Provedor do Entity Framework Core para SQL Server. |
| [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/12.0.2) | 12.0.2 | Biblioteca para serialização e desserialização de JSON. |

## Estrutura do Projeto


.vs
.vscode
bin
Controllers
Database
middlewares
Models
obj
Properties
Services
appsettings.Development.json
appsettings.json  
global.json
MegamanApi.csproj  
MegamanApi.sln
Program.cs
Startup.cs


### Diretórios e Arquivos

- **Controllers/**: Contém os controladores da API.
- **Database/**: Responsável pela interação com o banco de dados.
- **middlewares/**: Middleware para tratamento de requisições e respostas.
- **Models/**: Modelos que representam os dados da API.
- **Services/**: Lógica de negócio e serviços auxiliares.
- **appsettings.json**: Arquivo de configuração da aplicação.
- **Program.cs**: Ponto de entrada da aplicação.
- **Startup.cs**: Configurações iniciais da API.

## Técnicas Utilizadas

- **Arquitetura RESTful** - Organização da API seguindo os princípios do REST.
- **Injeção de Dependência** - Utilização do conceito de *Dependency Injection* para melhorar a modularidade do código.
- **Entity Framework Core** - ORM para comunicação eficiente com o banco de dados.
- **Tratamento de Exceções** - Uso de *middlewares* para manipulação de erros e respostas padronizadas.
- **Versionamento de API** - A API é estruturada na versão `v1`, facilitando futuras atualizações.

## Endpoints

csharp
using System.Collections.Generic;
using Megaman.Dtos;
using Megaman.Services;
using Microsoft.AspNetCore.Mvc;


```namespace Megaman.Controllers
{
    //api/v1/robots
    [ApiController]
    [Route("api/v1/robots")]
    public class RobotsController : ControllerBase
    {
        private readonly IRobotServices _services;
        public RobotsController(IRobotServices services)
        {
           _services = services;
        }

        //GET api/v1/robots
        [HttpGet] 
        public ActionResult<IEnumerable<RobotReadDTO>> GetAllRobots()
        {
            var robotItems = _services.SearchAll();
            return Ok(robotItems);
        }

        //GET api/v1/robots/{id}
        [HttpGet]
        [Route("{id:int}")]
        public object GetCommandById([FromRoute]int id)
        {   
            var robot = _services.SearchById(id);

            if(robot != null)
                return Ok(robot);
            
                return NotFound( 
                        new { message = "Nenhum robo encontrado" }
                );
        }

        //POST api/v1/robots
        [HttpPost]
        public ActionResult RobotSend(){
            return Ok();
        }
    }
}
```

## Como Executar o Projeto

1. Clone o repositório:
   sh
   git clone https://github.com/Cristiano1980-ti/MegamanApi.git
   
2. Navegue até a pasta do projeto:
   sh
   cd MegamanApi
   
3. Restaure as dependências:
   sh
   dotnet restore
   
4. Execute a aplicação:
   sh
   dotnet run
   
5. A API estará disponível em `http://localhost:5000/api/v1/robots`.

## Contribuição

Para contribuir com este projeto:
1. Faça um fork do repositório.
2. Crie uma nova branch:
   sh
   git checkout -b minha-feature
   
3. Faça suas modificações e commit:
   sh
   git commit -m "Minha nova feature"
   
4. Envie para o repositório remoto:
   sh
   git push origin minha-feature
   
5. Abra um Pull Request para revisão.

## Licença

Este projeto está licenciado sob a [MIT License](LICENSE).


Desenvolvido com ❤️ por [Cristiano Xavier](https://github.com/Cristiano1980-ti)

