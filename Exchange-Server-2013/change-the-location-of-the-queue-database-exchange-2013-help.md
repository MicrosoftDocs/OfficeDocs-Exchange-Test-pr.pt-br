---
title: 'Alterar o local do banco de dados de fila: Exchange 2013 Help'
TOCTitle: Alterar o local do banco de dados de fila
ms:assetid: f170cb0c-04a9-4fa7-b594-206e3a787e14
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb125177(v=EXCHG.150)
ms:contentKeyID: 51407933
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Alterar o local do banco de dados de fila

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

Um *queue* é um local de armazenamento temporário para mensagens que estão em espera para inserir o próximo estágio de processamento. Cada fila representa um conjunto de lógico de mensagens que processa de um servidor de transporte em uma ordem específica.

Como as versões anteriores do Exchange, o Microsoft Exchange Server 2013 usa um banco de dados do mecanismo de armazenamento extensível (ESE) para o armazenamento de mensagens da fila. Todas as filas diferentes são armazenadas em um único banco de dados ESE. Filas existem somente em servidores de caixa de correio ou em servidores de transporte de borda.

O local do banco de dados de fila e os logs de transações do banco de dados de fila é controlado por chaves no arquivo de configuração do aplicativo `%ExchangeInstallPath%Bin\EdgeTransport.exe.config` XML. Esse arquivo está associado ao serviço de transporte do Microsoft Exchange. A tabela a seguir explica cada chave em mais detalhes.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tecla</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>QueueDatabasePath</em></p></td>
<td><p>Esta chave especifica o local dos arquivos de banco de dados de fila. Os arquivos são:</p>
<ul>
<li><p>Mail.que</p></li>
<li><p>Trn.chk</p></li>
</ul>
<p>O local padrão é <code>%ExchangeInstallPath%TransportRoles\data\Queue</code>.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseLoggingPath</em></p></td>
<td><p>Esta chave especifica o local dos arquivos de log de transação fila banco de dados. Os arquivos são:</p>
<ul>
<li><p>Trn.log</p></li>
<li><p>Trntmp.log</p></li>
<li><p>Trn<em>nnn</em>.log</p></li>
<li><p>Trnres00001.jrs</p></li>
<li><p>Trnres00002.jrs</p></li>
<li><p>Temp.edb</p></li>
</ul>
<p>Observe que o TEMP é usado para verificar o esquema de banco de dados de fila quando inicia o serviço de transporte do Microsoft Exchange. Embora TEMP não for um arquivo de log de transações, ele é mantido no mesmo local em que os arquivos de log de transação.</p>
<p>O local padrão é <code>%ExchangeInstallPath%TransportRoles\data\Queue</code>.</p></td>
</tr>
</tbody>
</table>


## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 15 minutos.

  - Permissões do Exchange não se aplicam aos procedimentos neste tópico. Esses procedimentos são realizados no sistema operacional do Exchange Server.

  - Quando você parar ou reiniciar o serviço de transporte do Microsoft Exchange, o fluxo de emails no servidor é interrompido.

  - Quando você altera o local do banco de dados de fila ou os logs de transações, não foram movidos para as fila banco de dados e transações arquivos de log existentes. Um novo banco de dados de fila e novos logs de transação são criados no novo local. Os arquivos existentes são deixados no local antigo. No entanto, eles não são usados. Se você deseja reutilizar as fila banco de dados ou transações arquivos de log existentes no novo local, você deve mover os arquivos existentes para o novo local, depois que o serviço de transporte do Microsoft Exchange for interrompido, mas antes que o serviço foi iniciado.

  - Se a pasta de destino para os logs de transação ou de banco de dados da fila não existir, ele será criado para você se a pasta pai tem as seguintes permissões aplicadas a ele:
    
      - Serviço de Rede: Controle Total
    
      - Sistema: Controle Total
    
      - Administradores: Controle Total

  - Quaisquer configurações personalizadas em cada servidor feitas nos arquivos de configuração de aplicativo XML do Exchange, por exemplo, os arquivos web.config em servidores de acesso para cliente ou o arquivo EdgeTransport.exe.config em servidores de Caixa de Correio, são substituídos quando você instala uma Atualização Cumulativa do Exchange (CU). Não deixe de salvar essas informações para poder reconfigurar facilmente o servidor após a instalação. Você deve redefinir essas configurações depois de instalar uma Atualização Cumulativa.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## O que você deseja fazer?

## Usar o Prompt de comando para criar um novo banco de dados de fila e os logs de transações em um novo local

1.  Crie as pastas onde você deseja manter os logs de transações e de banco de dados de fila. Certifique-se de que as permissões corretas sejam aplicadas às pastas.

2.  Em uma janela de prompt de comando, abra o arquivo EdgeTransport.exe.config no bloco de notas executando o seguinte comando:
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

3.  Modifique as chaves a seguintes na seção `<appSettings>` .
    
        <add key="QueueDatabasePath" value="<LocalPath>" />
        <add key="QueueDatabaseLoggingPath" value="<LocalPath>" />
    
    Por exemplo, para criar um novo banco de dados de fila em D:\\Queue\\QueueDB e novos logs de transação D:\\Queue\\QueueLogs, use os seguintes valores:
    
        <add key="QueueDatabasePath" value="D:\Queue\QueueDB" />
        <add key="QueueDatabaseLoggingPath" value="D:\Queue\QueueLogs" />

4.  Quando terminar, salve e feche o arquivo EdgeTransport.exe.config.

5.  Reinicie o serviço de Transporte do Microsoft Exchange executando o seguinte comando:
    
        net stop MSExchangeTransport && net start MSExchangeTransport

## Como saber se funcionou?

Para verificar se você criado com êxito um novo banco de dados de fila e novos logs de transações em um novo local, faça o seguinte:

1.  Verifique se os novos arquivos de banco de dados Mail.que e Trn.chk existir no novo local.

2.  Verifique se os arquivos de log de transação novos arquivos Trn.log, Trntmp.log, Trnres00001.jrs, Trnres00002.jrs e TEMP existirem no novo local.

3.  Se você pode excluir a fila banco de dados e transações arquivos de log antigos do local antigo depois que o serviço de transporte do Microsoft Exchange foi iniciado, esses arquivos não estão sendo usados.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Voltar ao início

## Usar o Prompt de comando para mover os logs de transações e de banco de dados de fila existentes para um novo local

Apenas os cenários de recuperação de desastre onde o serviço de transporte do Microsoft Exchange não foi desligado corretamente ou uma falha de disco rígido exigiria que você deseja restaurar e realocar um banco de dados de fila existente e seus logs de transação existente.

Sob circunstâncias comuns, você não deve ter que reutilizar os logs de transação existente. Um desligamento normal do serviço de transporte do Microsoft Exchange grava todas as entradas de log de transações não confirmadas no banco de dados de fila. E, então, o log circular é usado, portanto logs de transações que contêm alterações confirmadas anteriormente do banco de dados não são preservados.

Use o procedimento a seguir para mover os logs de transações e de banco de dados de fila existentes em um novo local:

1.  Crie as pastas onde você deseja manter os logs de transações e de banco de dados de fila. Certifique-se de que as permissões corretas sejam aplicadas às pastas.

2.  Em uma janela de prompt de comando, abra o arquivo EdgeTransport.exe.config no bloco de notas executando o seguinte comando:
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

3.  Modifique as chaves a seguir na seção `<appSettings>` :
    
        <add key="QueueDatabasePath" value="<LocalPath>" />
        <add key="QueueDatabaseLoggingPath" value="<LocalPath>" />
    
    Por exemplo, para alterar o local do banco de dados de fila para D:\\Queue\\QueueDB e os logs de transação para D:\\Queue\\QueueLogs, use os seguintes valores:
    
        <add key="QueueDatabasePath" value="D:\Queue\QueueDB" />
        <add key="QueueDatabaseLoggingPath" value="D:\Queue\QueueLogs" />

4.  Quando terminar, salve e feche o arquivo EdgeTransport.exe.config.

5.  Pare o serviço de transporte do Microsoft Exchange executando o seguinte comando:
    
        net stop MSExchangeTransport

6.  Mova os arquivos de banco de dados existente Mail.que e Trn.chk do local original para o novo local.

7.  Move o log de transação existente arquivos Trn.log, Trntmp.log,*nnnnn*log Trn, Trnres00001.jrs, Trnres00002.jrs e TEMP do local antigo para o novo local.

8.  Inicie o serviço de transporte do Microsoft Exchange executando o seguinte comando:
    
        net start MSExchangeTransport

## Como saber se funcionou?

Para verificar que você moveu com êxito os logs de transações e de banco de dados de fila existentes para o novo local, faça o seguinte:

1.  Verifique se os arquivos de banco de dados de fila Mail.que e Trn.chk existir no novo local.

2.  Verifique se os arquivos de log de transação arquivos Trn.log, Trntmp.log, Trnres00001.jrs, Trnres00002.jrs e TEMP existirem no novo local.

3.  Verifique não se que há nenhuma fila de arquivos de log de transação ou de banco de dados no local original.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Voltar ao início

