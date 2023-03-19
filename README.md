## Navegação e Orientação

Geralmente quem está iniciando com ambientes Unix (Linux, macOS, etc) e nunca teve
nenhum contato com a linha de comando, assim quando abre o terminal, fica preso, sem
saber para onde ir. Vamos se desprender.

Para começar, nada melhor do que saber quem é você e onde está!

### `whoami`

Com esse comando, você pode saber qual o nome do seu usuário.
Digite: `whoami`. Agora você saber quem você é :)

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

> ### Limpar a bagunça
> 
> Para limpar sua tela, digite o comando `clear` ou aperte `Ctrl` `l`.
> 
> ### Outras dicas
> 
> Você não acha chato ter que digitar todo o nome do diretório, arquivo ou qualquer outra coisa?
> Bem, quando estiver usando a linha de comando, lembre-se da tecla `Tab` (a tecla que fica
> acima do `CapsLock`). Por exemplo, digamos que você queira listar o que há em `Downloads`.
> Faça: `ls Dow` `Tab`. Veja que o `Tab` completou o resto para você! Essa é uma das coisas
> mais valiosas a se saber!
> 
> Além disso, para voltar em comandos anteriores, use a setinha para cima do seu teclado.
> Isso é muito útil quando queremos rodar novamente comandos já utilizados.

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

E se eu quiser voltar para um diretório anterior ao que eu estou agora?
Digamos que você esteja em `~/Documentos/filmes/`, e para voltar pra `Documentos`, como faz?

O bash tem atalhos para voltar um diretório acima: digite `cd ..`.

`..` significa "a localização do diretório pai". Enquanto isso, `.`, significa o diretório
atual. Então, se você quiser rodar algum comando no diretório atual, apenas use: `<comando> .`.

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

Até agora usamos nomes de arquivos/diretórios que não contêm espaços. Mas
e se eu quiser criar um que os tenha? Levianamente, alguém poderia criar
uma pasta chamada "curso linux" fazendo: `mkdir curso linux`. Qual o problema disso?

Aqui, o `mkdir` criaria *duas* pastas, uma com o nome de `curso` e outra com o nome de
`linux`. Isso acontece porque passamos dois argumentos para `mkdir` (mais sobre isso
mais pra frente). Assim, se quisermos criar essa pasta, basta colocar o nome da
pasta entre aspas simples: `mkdir 'curso linux'`.


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
>
> Esse comando faz o seguinte: cria o diretório *pai* Filmes e todos os seus
> *filhos* (`filme1` ... `filme7`), em que em cada um deles, há um diretório
> chamado `legenda`. A opção `-p` faz com que `mkdir` crie `Filmes` e todos os
> possíveis subdiretórios que ele possua.
> 
> Só mais esse:
> 
> ```bash
> mkdir -p ~/Documentos/{fmcc, p1, lp1, ic}
> ```
> 
> Esse comando simplesmente cria os diretórios `fmcc`, `p1`, `lp1` e `ic` dentro
> de sua pasta `Documentos`. O mesmo pode ser feito se você ir para `Documentos`
> e, lá, criar esses diretórios.
> 
> Porém, algumas vezes você não quer sair de onde está, e com esse comando você
> cria vários diretórios em uma pasta de uma vez só.
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

Digamos que você quer se lembrar de uma questão que fez há alguns dias.
`cat questão.py` te mostraria, no terminal, qual o conteúdo desse arquivo.

### `less`

Mas e quando o arquivo é muito grande e ainda sim apenas quero visualizá-lo,
sem precisar de um editor de texto para abrí-lo? Bem, outra ferramenta resolve
esse problema!

`less` é um paginador, o que significa que ele mostra o conteúdo em páginas
(você dá o scroll pelo conteúdo, e a área que preenche sua tela é uma página).

Abra o seu arquivo de configuração do bash com `less ~/.bashrc` (se você estiver na *home*
basta abrir com `less .bashrc`). Para sair, navegar para baixo aperte `j` ou a setinha
para baixo, e para navegar para cima, `k` ou a setinha para cima. Se quiser sair, aperte
`q`.

Com o `less` é possível pesquisar por palavras no texto também: `/<termo_de_pesquisa>`
se pesquisando de cima para baixo ou `?<termo_de_pesquisa>` se pesquisando de
baixo para cima. Para ir e voltar em cada termo achado use `n` ou `N`, respectivamente.

### `rm` & `rmdir`

Aprendemos a criar arquivos e diretórios com `touch` e `mkdir`, respectivamente.
Mas e pra apagá-los?

`rm` pode ser usado para ambos os casos, embora ele seja um comando perigoso.
Uma vez apagado, é difícil de ter um arquivo ou diretório de volta.

Por conta disso, `rmdir` foi criado, e ele apaga apenas diretórios vazios.
Crie um diretório com `mkdir foo`. Tente apagá-lo com `rm foo`.
Você verá que não é possível, pois `foo` é um diretório. Agora, tente com 
`rmdir foo`. Isso funciona, pois `foo` é um diretório vazio.

Agora, crie um diretório chamado `bar` e, dentro dele, crie outro diretório chamado
`foobar`. Dentro de `foobar` crie um arquivo vazio chamado `arq.xt`.

Volte para sua *home* e tenta deletar o diretório `bar` com `rmdir`. Veja que não é possível,
pois `bar` não é um diretório vazio. Para apagá-lo, vamos precisar passar algumas *opções* para
o comando `rm`. Digite `rm -r bar`.

A opção `-r` remove ***r****ecursivamente* o que está em `bar`, ou seja, `foobar` e o arquivo
`arq.txt`.

> Tenha cuidado! Esse comando pode apagar um diretório inteiro, então use-o com moderação ;)

Para apagar um arquivo, usamos simplesmente `rm`. Por exemplo: `rm arquivo.txt`. Algumas vezes
temos arquivos protegidos. Para forçar a remoção, usamos a opção `-f`: `rm -f arq_protegido.txt`.
(Mais uma vez, cuidado! Essa opção também é perigosa.)

> ### Mais uma tangente!
> 
> Anteriormente citamos que o comando `rm` tem *opções*. Além disso, muitos comando têm também o que chamamos
> de *argumentos*. A estrutura de um comando é a seguinte:
> 
> ```
> <comando> OPÇÕES ARGUMENTOS
> ```
> 
> O número de opções e argumentos variam de comando para comando.
> Até agora estávamos usando vários comandos, passando opções e/ou argumentos (ou
> nenhum dos dois, como é o caso de `ls`).
> 
> Geralmente as opções tem duas formas: uma forma mais extensa e outra mais curta.
> Por exemplo:
> 
> `mkdir -p foo/bar` ou `mkdir --parents foor/bar`.
> 
> Aqui, `mkdir` é apresentado com uma opção, `-p` (a forma mais curta) ou `--parents` (a forma mais extensa, *verbosa*),
> e um argumento, `foo/bar`, o diretório `foo` e seu subdiretório `bar`. Já vimos o que essa opção faz: ela cria
> quaisquer diretórios e subdiretórios (diretórios pais e diretórios filhos, por isso `--parents`).
> 
> Esse tipo de formato segue para vários outros comandos, com a opção mais verbosa iniciando com `--` e a mais curta com
> `-`.
> 
> Uma coisa a se notar é que há vezes que um comando pode ter opção(ões) e/ou argumento(s) obrigatório(s) ou não.
> Para ilustrar isso, vamos recorrer a uma frequente ajuda nossa: as páginas `man` (de *man*ual).
> 
> #### `man`
> 
> Com `man` podemos ver o manual de uso de certo programa (geralmente um programa usado no terminal).
> As páginas `man` usam algum paginador, geralmente o `less`. Assim, tudo que aprendemos sobre `less` se
> aplica aqui.
> 
> Vejamos um exemplo: `man nano`.
> 
> `nano` é um simples editor de texto. Por enquanto não vamos focar no `nano`, mas sim em sua página
> `man`. Vejamos uma de sua sinopsis:
> 
> ```
> nano [options] [[+line[,column]] file]
> ```
> 
> Aqui, tudo que está entre colchetes é opcional. Primeiro, temos que as opções
> são opcionais (duh!). Depois, temos algo interessante: colchetes dentro de colchetes.
> 
> O que esse conjunto de colchetes quer dizer é: se quisermos utilizar o *argumento* `+line`
> (para abrir o `nano` numa linha específica), *obrigatoriamente*, precisamos passar como argumento
> o nome do arquivo (`file`). Ainda mais: se quisermos utilizar o argumento `column` (para
> abrir numa coluna específica), é *mandatório* utilizarmos o argumento `+line`.
> 
> > Veja como a sinopsis desse comando segue nossa estrutura básica, isto é
> o comando, seguido de opções e argumentos.
> 
> Ou seja (obs.: `#` são comentários):
> 
> ```bash
> nano +5 ~/.bashrc # válido
> 
> nano +5,2 ~/.bashrc # válido
> 
> nano +10 # inválido, pois não passamos um arquivo como argumento
> 
> nano 2 ~/.bashrc # inválido, por não passamos +line
> ```
> 
> As páginas `man` são muito úteis, e nos ajudarão muito em saber qual opção faz *tal* ou *qual* coisa.
> Logo, tente obter uma familiaridade com o comando `man`, pois, se você não tiver certeza o que certo comando
> faz, a página `man` dele com certeza te esclarecerá.

### `mv`

Até agora sabemos como criar e deletar diretórios e arquivos. No entanto ainda faltam
operações importantes, como mover e renomear arquivos. `mv` (*m*o*v*e) é uma faca de dois gumes,
uma vez que ela tanto pode mover quanto renomear arquivos e diretórios.

Para mover um arquivo/pasta, fazemos: `mv <arq_ou_pasta> <local>`. Ou seja, movemos `<arq_ou_pasta>` para
`<local>`. Digamos que baixamos uma prova em PDF, e queremos movê-la de `Downloads` para `Documentos`.
Para tal, podemos fazer: `mv Downloads/prova.pdf Documentos` (assumimos que você esteja na sua *home*).

Não pode parecer, mas `mv` pode ser um pouco perigoso também. Quer dizer, e se movermos um arquivo
`arq.txt` que está na pasta `foo` para uma pasta `bar`, sendo que na pasta `bar` já existe um arquivo com
o mesmo nome (`arq.txt`)? O comando `mv foo/arq.txt bar/` sobrescreveria `arq.txt` de `bar` de lugar do
`arq.txt` de `foo`.

Vamos testar isso: crie os diretórios `foo` e `bar` como descrito. Além disso, crie
arquivos vazios com mesmo nome `arq.txt` dentro de `foo` e `bar`. Agora, de dentro
da sua *home*, faça:

```bash
echo "conteúdo de foo" > foo/arq.txt
echo "conteúdo de bar" > bar/arq.txt

mv bar/arq.txt foo/
```

Cheque o que está em foo/arq.txt agora:
`cat foo/arq.txt`

O "conteúdo de foo" foi sobrescrito!

OK, mas como eu posso renomear um arquivo com um comando que move coisas?
Simples! Para renomear, basta fazer:
```bash
mv <nome_atual> <novo_nome>
```
, em que `<nome_atual>` e `<novo_nome>` referecem-se tanto a diretórios quanto arquivos.

O que estamos fazendo aqui, afinal? Bem, estamos *movendo* um arquivo/diretório existente para outro
arquivo/diretório inexistente. Ou seja, estamos sobrescrevendo um arquivo/diretório vazio!

### `cp`

Outra coisa muito comum que fazemos é copiar arquivos ou pastas.
Para fazer isso da linha de comando, usamos o comando `cp` (*c*o*p*y).

Supondo que você queira copiar um arquivo como `questoes.pdf` da *home* para
`Documentos`, basta fazer: `cp questoes.pdf Documentos/`

E para diretórios? Como um diretório pode ter vários outros subdiretórios e/ou arquivos nele,
precisamos copiar esse diretório *recursivamente*. Para isso usamos a opção `-r`, `-R` ou
`--recursive`: `cp -r Downloads/provas/ Documentos`.

Isso faria com que o diretório `Documentos` *também* tenha uma pasta chamada `provas`.

Assim como `mv` pode sobrescrever um arquivo, `cp` também pode (lembre-se da situação que
ilustramos anteriormente), então cuidado!

> Para ter um resumo das opções de um certo comando, utilize a opção `--help`.
> Muitos comandos têm essa opção para uma rápida olhada em suas principais opções.

## Edição de código/texto

O assunto de editores de texto é cabeludo, já que muitas pessoas defendem
seus respectivos editores com unhas e dentes.

Na matéria de LP1 vocês precisarão usar Vim! Apesar dessa obrigação, não tomem isso como
algo chato, mas sim divertido, pois Vim é muito divertido. Eu mesmo sou suspeito a falar,
pois gosto muito de Vim.

Hoje, vamos aprender o básico sobre o uso de Vim.

No Vim temos uma ideia muito incomum entre outros editores de texto: os modos.
Vim é um editor modal, o que significa que ele tem vários modos dependendo do *estado* em
que você está.

- ****Modo normal**** - `NORMAL`: É nesse modo que você *deve* permanecer quando não estiver usandos os
outros modos. No modo *normal* você consegue navegar pelo seu texto e fazer pequenas alterações.
De fato, quando estamos "*codando*" o que fazemos na maior parte do tempo é analisando o código,
fazendo pequenas mudanças para resolução de problemas, testes, etc. Para ir de qualquer
modo ao modo *normal* você aperta a tecla `Esc`.

- ****Modo inserção**** - `INSERT`: No modo *insert* você começa a escrever propriamente.
Para acessar esse comando você pode apertar `i` no teclado. Para entrar em modo *insert*
e ir para o final da linha, aperte `A`, para o começo da linha, `I`.

- ****Modo de  comando**** -  `COMMAND`: Por ser um editor extremamente flexível e customizável
(muito embora não pareça muito), Vim tem seus comandos próprios, que podem ser acessados da seguinte
forma (certifique-se que você esteja no modo *normal*): `:<comando>`. Um dos comandos mais importantes
é aquele para sair do Vim: aperte `:q` (ou `:quit`) se seu arquivo está salvo ou `:q!` (ou `:quit!`) para sair sem salvar.
E como faço para salvar um arquivo? Da mesma forma, podemos fazer: `:w` (ou `:write`).
Para salvar *e* sair você pode combinar dois comandos: `:wq` ou então apenas `:x`.

Agora vamos de fato aprender a como usar o Vim!! Como não quero reinventar a roda, vamos usar
um conteúdo que o próprio Vim apresenta para seus novos usuários, ensinando-os os comandos básicos.

De seu terminal, digite: `vimtutor`. Leia **atenciosamente** a tudo, e faça o que for pedido.
Tente completar todas as lições, do começo ao fim.
