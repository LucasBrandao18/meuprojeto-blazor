# meuprojeto-blazor
pratica-sala-de-aula

# Prática de Blazor — Aula 01

Implementação da parte prática de **Aula01 - Introducao ao Blazor no .NET 10.pdf**,
a partir da **página 15 do arquivo**.

**Aluno:** Lucas Brandão Viana — Ciência da Computação.

O PDF tem 35 páginas físicas, mas os slides numerados vão de 01/24 a 24/24:
há capturas de tela entre eles. Este projeto considera também essas capturas,
incluindo a alteração de `Home.razor` com as variáveis `Nome` e `Idade`.

## O que foi solicitado e implementado

| Página física / slide | Atividade | Implementação |
| --- | --- | --- |
| 15–20 / slide 15 | Criar `MeuPrimeiroBlazor` pelo template Blazor e abrir no VS Code. | Projeto `MeuPrimeiroBlazor.csproj` na raiz, preservando a estrutura e o layout do template. |
| 21–24 / slide 16 | Executar com `dotnet watch run`. | Perfil HTTP local em `http://localhost:5070`, com suporte a Hot Reload. |
| 25 / slide 17 | Entender `@page`, interpolação e `@code`. | `Components/Pages/Exemplo.razor`, rota `/exemplo`, com `valor = 0`. |
| 26 / slide 18 | Criar `Contador.razor`, com evento de clique e incremento. | Rota `/contador`, variável `contador = 0` e método `Incrementar`. |
| 27–30 / slide 19 e capturas | Editar um componente e observar a atualização automática. | `Home.razor` mostra `Nome` e `Idade`, como na captura, e recebeu uma alteração validada com Hot Reload. |
| 31–32 / slides 20–21 | Verificar o SDK, criar `Exercicio01`, rodar com Hot Reload e mudar um texto de `Home.razor`. | Segundo projeto independente em `Exercicio01/`, com página inicial personalizada e atualização automática testada. |
| 33 / slide 22 | Conhecer soluções para erros de ambiente. | Orientações na seção de problemas comuns deste README. |
| 34–35 / slides 23–24 | Revisar os próximos passos e o ambiente. | SDK e extensões conferidos; projetos preparados para estudo local. O roteiro de aulas futuras não é uma solicitação para implementar formulários ou outros exercícios agora. |

## Organização dos projetos

Há **duas aplicações independentes**, pois a aula usa um projeto para a
demonstração e pede a criação de outro para o exercício:

- **MeuPrimeiroBlazor:** arquivos diretamente na raiz `pratica-blazor`, conforme
  o caminho solicitado. Contém todos os exemplos desenvolvidos na aula.
- **Exercicio01:** subpasta com seu próprio `.csproj`, componentes e arquivos
  estáticos. Contém o exercício final de alteração de texto.

O projeto principal exclui `Exercicio01/**` dos itens de compilação e da
observação de arquivos. Isso impede que os componentes, os arquivos gerados
e o `Program.cs` de uma aplicação sejam compilados pela outra.

```text
pratica-blazor/
├── MeuPrimeiroBlazor.csproj
├── Program.cs
├── README.md
├── .gitignore
├── .vscode/
│   ├── extensions.json
│   ├── launch.json
│   └── tasks.json
├── Properties/launchSettings.json
├── Components/
│   ├── App.razor
│   ├── Routes.razor
│   ├── _Imports.razor
│   ├── Layout/                  # Layout, menu e reconexão do template
│   └── Pages/
│       ├── Home.razor            # Nome e idade do exemplo da aula
│       ├── Exemplo.razor         # @page, @valor e @code
│       ├── Contador.razor        # Contador implementado conforme a aula
│       ├── Counter.razor         # Contador original do template
│       ├── Weather.razor         # Dados fictícios do template
│       ├── Error.razor
│       └── NotFound.razor
├── wwwroot/                     # Bootstrap local, CSS e favicon
├── appsettings.json
├── appsettings.Development.json
└── Exercicio01/
    ├── Exercicio01.csproj
    ├── Program.cs
    ├── Components/Pages/Home.razor
    ├── Components/              # Demais componentes do template
    ├── Properties/launchSettings.json
    ├── wwwroot/
    └── appsettings*.json
```

`Counter` e `Weather` foram mantidos para preservar o template usado nas
capturas do professor. A previsão de `Weather` é simulada, não consulta uma
API meteorológica.

## Ambiente

- **SDK .NET 10**: versão encontrada na verificação, `10.0.400`.
- **VS Code** instalado e acessível pelo comando `code`.
- Extensões **C# Dev Kit**, **C#** e **.NET Install Tool** encontradas na lista
  de extensões instaladas. Há recomendações em `.vscode/extensions.json`.

Para conferir novamente:

```powershell
dotnet --version
code --list-extensions
```

Não há dependências NuGet de terceiros, banco de dados ou APIs externas.
O Bootstrap está incluído em `wwwroot`, sem depender de CDN.

## Como abrir e executar

### Demonstração: MeuPrimeiroBlazor

No PowerShell:

```powershell
Set-Location 'C:\Users\lucas\OneDrive\Documentos\vs code uni\pratica-blazor'
code .
dotnet watch run
```

Deixe o terminal aberto. Acesse **http://localhost:5070**. O perfil do projeto
permite abertura automática do navegador; se ele não abrir, use esse endereço
manualmente.

| Rota | Conteúdo |
| --- | --- |
| `/` | Exemplo de interpolação de nome e idade. |
| `/exemplo` | Valor inicial da variável `valor`. |
| `/contador` | Contador criado na aula. |
| `/counter` | Contador original do template. |
| `/weather` | Tabela com dados simulados do template. |

### Exercício prático 1: Exercicio01

Em outro terminal, a partir da mesma raiz:

```powershell
dotnet watch --project .\Exercicio01\Exercicio01.csproj run
```

Acesse **http://localhost:5071**. Também é possível entrar na subpasta e
executar os comandos exatamente como no exercício:

```powershell
cd Exercicio01
code .
dotnet watch run
```

As portas diferentes permitem executar os dois projetos ao mesmo tempo.
Para parar qualquer execução, use `Ctrl+C` no respectivo terminal.

### Compilar e executar sem Hot Reload

Na raiz:

```powershell
dotnet build MeuPrimeiroBlazor.csproj
dotnet build .\Exercicio01\Exercicio01.csproj
```

Para executar uma das aplicações sem observar alterações:

```powershell
dotnet run --project MeuPrimeiroBlazor.csproj
```

Ou:

```powershell
dotnet run --project .\Exercicio01\Exercicio01.csproj
```

No VS Code, com a raiz aberta, o F5 oferece as configurações **Demonstração -
MeuPrimeiroBlazor** e **Exercício 01**. Cada uma compila e executa a DLL do
projeto correspondente. Para reproduzir o fluxo de edição da aula, prefira
`dotnet watch run` no terminal.

## Como os códigos funcionam

### Inicialização e estrutura

`Program.cs` registra os componentes Razor e o suporte a **Interactive Server**,
configura arquivos estáticos e mapeia o componente `App` como raiz da aplicação.

`App.razor` define o HTML, carrega o Bootstrap e os estilos locais e inclui o
script `_framework/blazor.web.js`. `Routes.razor` encontra os componentes
marcados com `@page` e os exibe dentro de `MainLayout`. `NavMenu` fornece os
links de navegação.

### Exemplo.razor

```razor
@page "/exemplo"

<h3>Exemplo</h3>
<p>Valor atual: @valor</p>

@code {
    private int valor = 0;
}
```

`@page` define o endereço; `@valor` insere o valor da variável no HTML;
`@code` reúne a lógica C#. Esse exemplo não tem botão: ele mostra o valor zero.

### Contador.razor

O componente declara `private int contador = 0`. O botão usa
`@onclick="Incrementar"`, e o método `Incrementar` executa `contador++`.
O Blazor atualiza o parágrafo `Valor atual: @contador` após o evento.
O atributo `role="status"` permite anunciar a atualização a leitores de tela.

Foi acrescentado **`@rendermode InteractiveServer`**, necessário porque o
template usa interatividade por página. Sem isso, copiar somente o trecho do
slide poderia produzir um botão sem ação em uma página renderizada estaticamente.
O botão aguarda a conexão interativa antes de ser habilitado.

O contador é um estado em memória do componente. Ele volta a zero ao
recarregar a página ou criar uma nova instância do componente.

### Home.razor da demonstração

Reproduz os valores didáticos da captura da página 28:

```csharp
private string Nome = "Epaminondas";
private int Idade = 30;
```

O texto usa `<strong>@Nome</strong>` e `<strong>@Idade</strong>` para mostrar
os valores. Esses dados pertencem ao exemplo do professor e **não representam
o nome nem a idade do aluno**.

### Home.razor do Exercicio01

O template começa com `Hello, world!` e `Welcome to your new app.`.
Com o projeto aberto no navegador e o watcher ativo, esses textos foram
alterados para a apresentação do exercício, incluindo:

> Olá, Lucas! Meu primeiro exercício com Blazor.

> Texto atualizado com Hot Reload no .NET 10.

Isso atende ao exercício de modificar um texto e observar a mudança sem
parar o servidor. O nome completo e o curso foram preenchidos com os dados
informados pelo aluno.

## Como repetir a prática de Hot Reload

1. Inicie `Exercicio01` com `dotnet watch` e abra a página na porta 5071.
2. Abra `Exercicio01/Components/Pages/Home.razor`.
3. Mude apenas o texto de um parágrafo e salve com `Ctrl+S`.
4. Observe o terminal registrar `File updated` e `C# and Razor changes applied`.
5. Confira o novo texto no navegador sem clicar em atualizar.

O mesmo procedimento funciona no `Components/Pages/Home.razor` da demonstração.
Mudanças de texto Razor normalmente são aplicadas diretamente; alterações
estruturais podem exigir reinicialização. Nesse caso, siga o aviso do watcher
ou use `Ctrl+R`. `dotnet run` sozinho não observa os arquivos.

## Ajustes para execução neste computador

- **`UseAppHost=false`** nos dois `.csproj`: executa a aplicação pelo runtime
  `dotnet` instalado, sem depender do `.exe` nativo bloqueado anteriormente
  pelo controle de aplicativos do Windows. Nenhuma política de segurança é alterada.
- **HTTP local em 5070 e 5071**: a aula aceita porta semelhante e suas capturas
  já mostram HTTP. Os projetos foram criados com `--no-https`; por isso não
  precisam configurar certificados nem apresentam o aviso de redirecionamento
  HTTPS mostrado no material. Essa é uma configuração para estudo local.
- **Exclusão do projeto filho**: `DefaultItemExcludes` impede a compilação e
  observação recursiva do `Exercicio01` pelo projeto principal.


## Verificações realizadas

- SDK .NET 10 e instalação das extensões conferidos.
- Compilação dos dois projetos sem erros nem avisos.
- Páginas iniciais abertas no navegador.
- `Exemplo.razor` exibindo `Valor atual: 0`.
- `Contador.razor` iniciando em zero e chegando a três após três cliques.
- Edição real de `Home.razor` nos dois projetos, com aplicação das alterações
  pelo watcher e atualização observada no navegador sem recarregamento manual.
