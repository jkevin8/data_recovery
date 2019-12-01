# Recuperacao de dados

Aula sobre recuperação de dados

Edite o texto a para organizar pesquise por  Markdown (Linguagem de marcação de texto )

## Introdução

**Qual é o componente mais valioso de um computador?**

Você pode sugerir, num primeiro momento, que seria o processador. Em geral, o processador é o componente mais caro de um computador. A não ser que você queira investir numa placa de vídeo de ponta, ou numa placa-mãe cheia de novidades. Todas essas alternativas estão considerando valor econômico das partes do computador, mas será mesmo que valioso é aquilo que tem um preço alto?

Há quem diga que o que é realmente valioso é aquilo que é difícil de ser substituído. Por isso preços mais altos são naturalmente relacionados a itens mais valiosos. Então eu pergunto, quanto custa os seus dados?
Faltando um dia para a entrega do seu trabalho de fim de curso, por acidente, você deleta o arquivo. Você perdeu tudo. E agora? Quanto você pagaria para tê-lo novamente? Os dados do usuário são a coisa mais importante num computador. Todo o resto é substituível, mas tem um preço. E é impossível precificar aquela foto especial que estava armazenada no disco rígido do computador que foi roubado, por exemplo.

Por isso, nessa aula pretende-se mostrar várias estratégias de manutenção corretiva e preventiva relacionadas ao armazenamento de dados.

Os slides usados na aula podem ser encontrados [aqui](https://jp-guimaraes.github.io/data_recovery). Eles vão sendo atualizados aos poucos. Se quiser contribuir para essa aula, o código pode ser encontrado [aqui](https://github.com/jp-guimaraes/data_recovery). Comentários, críticas e dúvidas também são sempre bem-vindas, basta enviar um e-mail para <joao.guimaraes@ifrn.edu.br>.

## Técnicas de recuperação de dados

* Manutenção Corretiva
* Manutenção Preventiva

Recuperar, mas por quê?

* Dados inacessíveis
* Sistema Operacional?
* Foram deletados?
* Lixeira
* Nuvem

## Estratégias de Backup

* Importância

O backup (cópia  de segurança) é a única forma de recuperar informações em caso de pane (tanto por parte do hardware quanto dos softwares). Arquivos de dados, como: fotos, imagens, planilhas, textos, etc. Computadores e programas podem parar de uma hora para outra, impedindo acesso às informações. Você nunca sabe quando isso irá acontecer, portanto é importante manter o backup sempre atualizado.

* Tipos de backup

Backup Completo: este tipo de backup faz uma cópia de todos os dados para outro local. Sem nenhum tipo de segmentação.

 * Backup Incremental 
 
 Resultará na cópia apenas dos dados que foram alterados desde a última operação de backup de qualquer tipo.
 
 * Backup Diferencial 
 
 É semelhante a um incremental na primeira vez em que é executada, pois copiará todos os dados alterados do backup anterior. No entanto, cada vez que for executado posteriormente, ele continuará copiando todos os dados alterados desde o backup completo anterior.

 * Backup Espelhado
 
 Quando um arquivo na origem é excluído, ele também é excluído no backup de espelhamento. Por isso, os backups espelhados devem ser usados com cautela, pois, um arquivo excluído acidentalmente ou por vírus, também pode fazer com que os backups espelhados sejam excluídos.

 * Backup Local
 
  Qualquer tipo de backup em que o meio de armazenamento é mantido à mão, em dispositivo físico. Backups locais protegem o conteúdo digital de falhas no disco rígido e ataques de vírus. 

 * Backup Externo 
 
 Quando o armazenamento de mídia de backup é mantido em um local geográfico diferente da origem, isso é conhecido como backup externo.

 * Backup Online ou na Nuvem 
 
 Estes são backups feitos continuamente, sempre conectado à origem que está sendo armazenada em backup. Normalmente, o meio de armazenamento em nuvem está localizado fora do local e conectado à fonte de backup por uma rede ou conexão com a Internet.

 * Backup Remoto
 
 É uma forma de backup externo, com a diferença de que você pode acessar, restaurar ou administrar os backups enquanto está localizado em seu local de origem ou outro local.

 * Backup FTP
 
 É um tipo de backup onde o processo é feito através da Internet para um servidor FTP. Normalmente, o servidor FTP está localizado em um data center comercial, longe dos dados de origem que estão sendo armazenados em backup.


* RAID

* Sistema Operacional
  * Linux
    Script
  * Windows
    Tasker
* Nuvem

## RAID

## Gerenciador de janelas do ubuntu

```shell
nautilus
```

## Gerenciador de janelas do lubuntu

```shell
pcmanfm
```

## Montagem

```shell
sudo mount -t tipo arquivo_particao diretorio_destino
```

O arquivo da partição vai ser algo do tipo `/dev/sda1`

## Recuperação de dados em partições e discos formatados

Para recuperar dados em partições e discos formatados/deletados é recomendado o procedimento de clonagem.

## Clonagem de discos

Aqui temos um breve resumo sobre clonagem de discos e partições usando o software dd. Existe um repositório mais completo sobre clonagem que pode ser encontrado [aqui](https://github.com/jp-guimaraes/clonagem). Lá pode ser encontrado uma revisão de alguns comandos básicos de terminal do linux para depois aprensentar o `dd`, ferramenta usada para clonagem.

### O comando dd

Em geral o `dd` é usado da seguinte forma:

```shell
dd if=/dev/sda1 of=/dev/sdb2
```

`if=/dev/sda1` é a primeira partição do disco a que será clonada para a segunda partição do disco b, `/dev/sdb2`

### Como fazer data wipe num disco rígido

Uso:

```shell
dd if=/dev/urandom of=/dev/sdX bs=4k
```

### O programa `foremost`

O [foremost](https://github.com/korczis/foremost) é um software livre que busca por cabeçalhos de arquivos com o objetivo de recuperar arquivos em partições e discos. Por essa característica de buscar cabeçalhos, pode-se usar esse software para recuperar inclusive arquivos deletados ou de partições/discos formatados.

Para usar o foremost para recuperar arquivos basta passar os tipos de arquivos que se deseja buscar pelos cabeçalhos, o arquivo ou partição de entrada e um diretório de saída onde os arquivos recuperados serão armazenados. Usa-se `-t all` para buscar por todas as extensões de arquivos possíveis.

```shell
foremost -t all -i arquivo_de_entrada -o diretorio_de_saida
```

### Roteiro de recuperação

1. Clonar partição alvo e gerar aquivo iso equivalente

```shell
dd if=/dev/particao_alvo of=/localizacao_do_arquivo
```

1. Criar diretório para receber arquivos recuperados

```shell
mkdir dir_arquivos_recuperados
```

1. Rodar foremost buscando por todos os cabeçalhos de arquivos possíveis na imagem criada

```shell
foremost -t all -i localizacao_do_arquivo -o dir_arquivos_recuperados
```

Ao final do processamento, um arquivo .txt é gerado com o resumo do procedimento.
