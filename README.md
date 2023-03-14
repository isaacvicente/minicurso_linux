## Navegação e Orientação

Geralmente quem está iniciando com ambientes Unix (Linux, macOS, etc) e nunca teve
nenhum contato com a linha de comando, assim quando abre o terminal, fica preso, sem
saber para onde ir. Vamos se desprender, então:

### `pwd`

Essa tela preta parece meio assustadora. Vamos nos informar de onde estamos então.
Digite `pwd`. Esse comando te mostra o diretório atual em que você está.

> `pwd` pode ser lembrado como ***p***rint ***w***orking ***d***irectory

### `ls`

Ok, mas o que está em nosso diretório? Vejamos: digite `ls` para *listar*
o que há no diretório em que você está.

Dentre os diretórios listados, muito provavelmente você verá:

- Downloads
- Documentos
- Vídeos
- etc...

Esses também são diretórios, como você pode perceber pela cor. Logo, você pode
pensar que nossa `home` é o diretório *pai* de Downloads, Documentos, etc.

### `cd`

Se Downloads é um diretório, podemos nos mover para dentro dele. Para tal,
digite o comando `cd Downloads` (***c***hange ***d***irectory). Quando damos um
`ls` podemos ver os arquivos ou pastas (diretórios) que possivelmente foram
baixados.

Para voltar onde estávamos (na `home`), temos várias maneira:

- `cd` - por padrão, `cd` já leva à *home* do usuário
- `cd ~` - `~` é um atalho pra *home*
- `cd $HOME` - o mesmo que o anterior
- `cd -` - este é interessante: ele te leva para o local onde você estava
anteriormente

`cd -` é um comando muito conveniente: vá de novo para `Downloads` e depois
digite: `cd ~/Documentos`. Agora você pode alternar entre os dois diretórios
apenas digitando `cd -`!

## Manipulação de arquivos e diretórios

### `touch`

Vamos criar alguns arquivos vazios com o comando `touch`. Imagine que você
apenas *toca* esses arquivos, sem inserir nada neles.

Digamos que você queira criar os arquivos `file1.txt`, `file2.txt` e
`file3.txt`. Para criá-los você faz:

```bash
touch file1.txt file2.txt file3.txt
```

### `mkdir`

E para criar diretórios? Fácil! `mkdir` (***m***ake ***dir***ectory) faz
justamente isso. Digamos que você queira criar o diretório `Fotos` na sua
*home*. Supondo que você já está na *home* (cheque com `pwd`), faça: `mkdir
Fotos`.

Agora, vamos criar o diretório `Filmes` dentro de `Downloads`, estando na
*home*: `mkdir Downloads/Filmes`. Você muito bem poderia se mover para
`Downloads` com `cd` e criar o diretório lá, mas isso é muito trabalho, né?


> ### Pequena pausa!
> 
> #### Expansão
> 
> Você percebeu o quão tedioso é criar arquivos do tipo:
> arq1.txt arq2.txt, etc? O Bash (e outros shells) têm uma coisa que
> se chama *expansão*:
> 
> Para ter o mesmo efeito do que vimos no exemplo do `touch` poderíamos
> fazer: `touch file{1..3}.txt`.
> 
> Por que "expansão"? Bem, aperte `Tab` e verá: essa nova *sintaxe* fez com que
> tivéssemos a mesma coisa que antes!
> 
> Outro exemplo interessante:
> ```bash
> mkdir -p Filmes/filme{1..7}/legenda
> ```
> Esse comando faz o seguinte: cria o diretório *pai* Filmes e todos os seus
> *filhos* (`filme1` ... `filme7`), em que em cada um deles, há um diretório
> chamado `legenda`. A opção `-p` faz com que `mkdir` crie `Filmes` e todos os
> possíveis subdiretórios que ele possua.
> 
> #### Caminhos
> 
> Você pôde perceber que para acessar um diretório dentro de outro, colocamos
> uma barra (`/`) entre eles.
> 
> Quando passamos algum arquivo ou diretório para algum comando, estamos dando
> a ele o *caminho* para esse arquivo ou diretório. Temos dois tipos de caminho
> (ou *path*):
> 
> - **Caminhos absolutos**: esses caminhos são apresentados desde a raiz do
>   sistema até onde queremos chegar. Por exemplo, o caminho absoluto de
>   `Downloads` é: `/home/<nome_do_usuario>/Downloads`. O comando `pwd`
>   printará justamente isso se você estiver em `Downloads`!
> 
> - **Caminhos relativos**: estávamos usando caminhos relativos até agora.
>   Quando você está na sua *home* e digita `cd Downloads`, o comando `cd` pega
>   o caminho ***relativo*** à *home*. Logo um caminho relativo é aquele que
>   segue de onde você está a diante.
> 
> Caminhos relativos são os mais usados e os mais úteis, embora você possa
> precisar usar algum caminho absoluto.
> 
> Por vezes um caminho absoluto pode ser "encurtado" e, assim, se parecer com
> um caminho relativo. Digamos que você está em `/etc/` e quer se movimentar
> para sua pasta de `Downloads`. Para isso, poderíamos fazer: `cd ~/Downloads`.
> Como sabemos, `~/` equivale a `/home/<nome_do_usuario>/`.
> 
> Assim, temos uma maneira bem mais confortável de acessar os diretórios e
> subdiretórios de *home*, por ser um local tão comum.

### `cat`

Muitas vezes queremos saber o que está dentro de um arquivo texto ou, para nós,
um arquivo que contém algum código fonte, em Python por exemplo. Nem sempre
vamos editar esse arquivo, então abrir um editor de texto gráfico só pra ler
esse arquivo e sair é muito tedioso, não?

O comando `cat` (con**cat**enate) faz o simples trabalho de mostrar o que há
dentro de um arquivo, imprimindo-o na tela. Isso é muito comum quando temos
arquivos pequenos, de poucas linhas, e apenas queremos seu conteúdo. 
