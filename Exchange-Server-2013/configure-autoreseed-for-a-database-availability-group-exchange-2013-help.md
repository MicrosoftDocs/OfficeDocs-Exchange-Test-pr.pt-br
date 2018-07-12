---
title: 'Configurar o AutoReseed para um grupo de disponibilidade do banco de dados: Exchange 2013 Help'
TOCTitle: Configurar o AutoReseed para um grupo de disponibilidade do banco de dados
ms:assetid: 4a8bd779-b52a-40ed-8040-4d76eabeb41e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ619303(v=EXCHG.150)
ms:contentKeyID: 50485522
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o AutoReseed para um grupo de disponibilidade do banco de dados

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2013-04-15_

A nova propagação automática é um recurso para restaurar a redundância do banco de dados, após uma falha de disco. Se um disco falhar, as cópias de banco de dados armazenadas nesse disco são propagadas novamente, de maneira automática, para um disco sobressalente pré-configurado no servidor de Caixa de Correio. Você pode usar as instruções deste tópico para configurar a Nova Propagação Automática para um grupo de disponibilidade de banco de dados (DAG).


> [!WARNING]
> O recurso de Nova Propagação Automática não executa quaisquer tarefas de pré-requisitos de configuração para você. Instalar discos corretamente, adicionar discos sobressalentes ao sistema, trocar discos defeituosos e formatar novos discos são coisas que devem ser feitas manualmente pelo administrador.



Para tarefas de gerenciamento adicionais relacionadas a DAGs, consulte [Gerenciando grupos de disponibilidade de banco de dados](managing-database-availability-groups-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para a conclusão da tarefa: 10 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Grupos de Disponibilidade do Banco de Dados" no tópico [Permissões de resiliência de site e disponibilidade altas](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Uma partição de disco lógica única por disco físico deve ser criada.

  - A estrutura específica do banco de dados e da pasta de log descrita nas etapas abaixo deverá ser usada.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Como fazer isso?

## Etapa 1: Configurar os caminhos raiz de bancos de dados e volumes

A primeira etapa envolve configurar os diretórios raiz para os bancos de dados (*AutoDagDatabasesRootFolderPath*) e volumes (*AutoDagVolumesRootFolderPath*) usados pelo DAG. Os padrões são C:\\ExchangeDatabases e C:\\ExchangeVolumes, respectivamente. Se você estiver usando os caminhos padrão, pode pular essa etapa.

Este exemplo ilustra como configurar o caminho raiz para os bancos de dados.

    Set-DatabaseAvailabilityGroup DAG1 -AutoDagDatabasesRootFolderPath "C:\ExchDbs"

Este exemplo ilustra como configurar o caminho raiz para os volumes de armazenamento.

    Set-DatabaseAvailabilityGroup DAG1 -AutoDagVolumesRootFolderPath "C:\ExchVols"

## Como saber se essa etapa funcionou?

Para verificar se você configurou com êxito os caminhos raiz para bancos de dados e volumes, execute este comando:

    Get-DatabaseAvailabilityGroup DAG1 | Format-List *auto*

A saída para *AutoDagDatabasesRootFolderPath* e *AutoDagVolumesRootFolderPath* deve refletir os caminhos configurados.

## Etapa 2: Configurar o número de bancos de dados por volume

Em seguida, configure o número de bancos de dados por volume (*AutoDagDatabaseCopiesPerVolume*) para o DAG.

Este exemplo ilustra como definir essa configuração de Nova Propagação Automática para um DAG configurado com 4 bancos de dados por volume.

    Set-DatabaseAvailabilityGroup DAG1 -AutoDagDatabaseCopiesPerVolume 4

## Como saber se essa etapa funcionou?

Para verificar se você configurou com êxito o número de bancos de dados por volume, execute este comando.

    Get-DatabaseAvailabilityGroup DAG1 | Format-List *auto*

A saída para *AutoDagDatabaseCopiesPerVolume* deve refletir o valor configurado.

## Etapa 3: Criar os diretórios raiz para bancos de dados e volumes

Primeiro, crie os diretórios que correspondem aos diretórios raiz configurados na Etapa 1. O exemplo a seguir mostra como criar os diretórios padrão usando o prompt de comando.

``` 
    md C:\ExchangeDatabases
``` 
``` 
    md C:\ExchangeVolumes
``` 

## Como saber se essa etapa funcionou?

Para verificar se você configurou com êxito os diretórios raiz para bancos de dados e volumes, execute este comando:

    Dir C:\

Os diretórios criados devem aparecer na lista de saída.

## Etapa 4: Montar as pastas de volume

Para cada volume que será usado para os bancos de dados (incluindo volumes sobressalentes), use o aplicativo Gerenciamento de Disco do Windows (diskmgmt.msc) para montar cada volume em uma pasta montada em C:\\ExchangeVolumes\\. Por exemplo, se houver 2 volumes com bancos de dados e 1 volume sobressalente, monte os volumes para as seguintes pastas montadas:

  - C:\\ExchangeVolumes\\Volume1

  - C:\\ExchangeVolumes\\Volume2

  - C:\\ExchangeVolumes\\Volume3

Os nomes das pastas montadas podem ser qualquer nome de pasta, desde que as pastas sejam montadas sob o caminho do volume raiz.

## Como saber se essa etapa funcionou?

Para verificar se você montou com êxito as pastas de volume, execute este comando:

    Dir C:\

Os volumes montados devem aparecer na lista de saída.

## Etapa 5: Criar as pastas de banco de dados

Em seguida, crie os diretórios de banco de dados no caminho de raiz C:\\ExchangeDatabases. Este exemplo ilustra como criar diretórios para uma configuração de armazenamento de 4 bancos de dados em cada volume.

``` 
    md c:\ExchangeDatabases\db001
``` 
``` 
    md c:\ExchangeDatabases\db002
``` 
``` 
    md c:\ExchangeDatabases\db003
``` 

``` 
    md c:\ExchangeDatabases\db004
``` 

## Como saber se essa etapa funcionou?

Para verificar se você montou com êxito as pastas de banco de dados, execute este comando:

    Dir C:\ExchangeDatabases

Os diretórios criados devem aparecer na lista de saída.

## Etapa 6: Criar pontos de montagem para os bancos de dados

Crie os pontos de montagem para cada banco de dados e vincule o ponto de montagem ao volume correto. Por exemplo, a pasta montada para db001 deve ser em C:\\ExchangeDatabases\\db001. Você pode usar diskmgmt.msc ou mountvol.exe para fazer isso. Este exemplo ilustra como montar db001 para C:\\ExchangeDatabases\\db001 usando mountvol.exe.

    Mountvol.exe c:\ExchangeDatabases\db001 \\?\Volume (GUID)

## Como saber se essa etapa funcionou?

Para verificar se você criou com êxito os pontos de montagem dos bancos de dados, execute este comando.

    Mountvol.exe C:\ExchangeDatabases\db001 /L

O volume montado deve aparecer na lista de pontos de montagem.

## Etapa 7: Criar a estrutura do diretório de banco de dados

Depois, crie dois diretórios dentro das pastas que você criou na Etapa 5, um para cada banco de dados e um para cada fluxo de log de banco de dados que será armazenado no mesmo volume. Você deve usar o seguinte formato para sua estrutura de diretório:

C:\\\< *NomeDaPastaDoBancoDeDados*\>\\*NomeDoBancoDeDados*\\\<*NomeDoBancoDeDados*\>.db

C:\\\< *NomeDaPastaDoBancoDeDados*\>\\*NomeDoBancoDeDados*\\\<*NomeDoBancoDeDados*\>.log

Este exemplo ilustra como criar diretórios para 4 bancos de dados que serão armazenados no Volume 1:

``` 
    md c:\ExchangeDatabases\db001\db001.db
``` 
``` 
    md c:\ExchangeDatabases\db001\db001.log
``` 
``` 
    md c:\ExchangeDatabases\db002\db002.db
``` 
``` 
    md c:\ExchangeDatabases\db002\db002.log
``` 
``` 
    md c:\ExchangeDatabases\db003\db003.db
``` 
``` 
    md c:\ExchangeDatabases\db003\db003.log
``` 
``` 
    md c:\ExchangeDatabases\db004\db004.db
``` 
``` 
    md c:\ExchangeDatabases\db004\db004.log
``` 
Repita os comandos acima para bancos de dados em cada volume.

## Como saber se essa etapa funcionou?

Para verificar se você criou com êxito a estrutura de diretório de bancos de dados, execute este comando.

    Dir C:\ExchangeDatabases /s

Os diretórios criados devem aparecer na lista de saída.

## Etapa 8: Criar bancos de dados

Crie bancos de dados com caminhos de log e de banco de dados configurados com as pastas apropriadas. Este exemplo ilustra como criar um banco de dados que é armazenado no diretório e na estrutura de ponto de montagem recém-criados.

    New-MailboxDatabase -Name db001 -Server MBX1 -LogFolderPath C:\ExchangeDatabases\db001\db001.log -EdbFilePath C:\ExchangeDatabases\db001\db001.db\db001.edb

## Como saber se essa etapa funcionou?

Para verificar se você criou com êxito os banco de dados na pasta a adequada, execute este comando:

    Get-MailboxDatabase db001 | Format List *path*

As propriedades de banco de dados que são retornadas devem indicar que o arquivo de banco de dados e os arquivos de log estão sendo armazenados nas pastas acima.

## Como saber se essa tarefa funcionou?

Para verificar se você configurou a Nova Propagação Automática para um DAG, faça o seguinte:

1.  Execute o seguinte comando para verificar se o DAG está configurado corretamente.
    
        Get-DatabaseAvailabilityGroup DAG1 | Format-List *auto*

2.  Execute o comando a seguir para verificar se a estrutura de diretório está configurada corretamente (abaixo, estão os caminhos padrão; se necessário, substitua os caminhos pelos caminhos que você está usando).
    
``` 
        Dir c:\ExchangeDatabases /s
``` 
```     
        Dir c:\ExchangeVolumes /s
``` 
