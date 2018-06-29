---
title: 'Usar o Backup do Windows Server para fazer backup e restaurar dados do Exchange: Exchange 2013 Help'
TOCTitle: Usar o Backup do Windows Server para fazer backup e restaurar dados do Exchange
ms:assetid: 0fac891a-5713-42b6-afd5-c91b2b88f966
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd876851(v=EXCHG.150)
ms:contentKeyID: 50484949
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Usar o Backup do Windows Server para fazer backup e restaurar dados do Exchange

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2016-12-09_

[Preferencial arquitetura](https://blogs.technet.com/b/exchange/archive/2014/04/21/the-preferred-architecture.aspx) para Exchange Server 2013 da Microsoft aproveita um conceito conhecido como Exchange Native Data Protection. Exchange Proteção de dados nativa depende de recursos nativos Exchange para proteger os dados de caixa de correio, sem o uso de backups tradicionais. Mas, se você quiser criar backups, Exchange inclui um plug-in para Windows Server Backup (WSB) que permite que você crie sensível ao Exchange backups baseados em VSS do serviço de cópias de sombra de Volume de dados Exchange. Para aproveitar os backups sensível ao Exchange, você deve ter o recurso WSB instalado.

O plugin, WSBExchange.exe, funciona como um serviço denominado Extensão do Servidor do Microsoft Exchange para Backup do Windows Server (o nome curto para esse serviço é WSBExchange). Esse serviço é instalado e configurado automaticamente para inicialização manual em todos os servidores de Caixa de Correio. O plugin permite que o WSB crie backups de VSS com suporte ao Exchange.

Antes de usar o WSB para fazer backup dos dados do Exchange, recomendamos que você se familiarize com os seguintes recursos e opções para o plugin:

  - Os backups feitos com o WSB ocorrem no nível de volume e a única maneira de realizar um backup ou uma restauração no nível do aplicativo é selecionando um volume inteiro. Para fazer backup de um banco de dados e de seu fluxo de logs, é preciso fazer backup de todo o volume que contém o banco de dados e os logs, não apenas das pastas individuais. Não é possível fazer backup de dados sem fazer o backup do volume inteiro que contém os dados.

  - O backup deve ser executado localmente no servidor que fará parte do backup, e não é possível usar o plug-in para fazer backups VSS remotos. Não há administração remota do WSB ou do plugin. No entanto, você pode usar os Serviços de Área de Trabalho Remota ou os Serviços de Terminal para gerenciar backups remotamente.

  - O backup pode ser criado em uma unidade de disco rígido local ou em um compartimento de rede remoto.

  - Somente backups completos devem ser realizados. O truncamento do log ocorrerá após a conclusão bem-sucedida de um backup completo de VSS de um volume ou de pastas contendo um banco de dados do Exchange.

  - Ao restaurar os dados, é possível restaurar somente os dados do Exchange. Esses dados podem ser restaurados para seu local original ou para um local alternativo. Se você restaurar os dados para o local original, o WSB e o plugin controlarão automaticamente o processo de recuperação, incluindo a desmontagem de qualquer banco de dados existente e a repetição de logs no banco de dados recuperado.

  - O processo de restauração não é compatível com a Recuperação de banco de dados do Exchange (RDB). Se quiser usar uma RDB, é preciso restaurar os dados em um local alternativo e, então, copiar ou mover manualmente os dados restaurados a partir deste local para a estrutura de pastas RDB.

  - Ao restaurar dados do Exchange, o backup de todos os bancos de dados deve ser restaurado junto. Não é possível restaurar apenas um banco de dados.

  - Restaurações de bare metal são compatíveis ao usar o WSB. No entanto, a abordagem de recuperação recomendada para servidores Exchange é recuperar o servidor Exchange e, em seguida, restaurar os dados. Se você estiver usando um aplicativo de backup de terceiros (por exemplo, que não seja da Microsoft), o suporte para restaurações de bare metal talvez seja disponibilizado pelo fornecedor do aplicativo de backup.

A tabela a seguir descreve a capacidade de suporte das opções de backup e recuperação disponíveis para o Exchange 2013 com WSB.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Se você...</th>
<th>Então...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Fizer backup do servidor completo...</p></td>
<td><p>Será realizada uma cópia de backup do VSS e os logs de transação para os bancos de dados no servidor não serão truncados.</p></td>
</tr>
<tr class="even">
<td><p>Executar um backup personalizado e selecionar um ou mais volumes para fazer backup...</p></td>
<td><p>Um backup de VSS completo pode ser selecionado, permitindo que os logs de transação dos bancos de dados nos volumes selecionados sejam truncados na conclusão bem-sucedida de um backup.</p></td>
</tr>
<tr class="odd">
<td><p>Executar um backup personalizado e selecionar uma ou mais pastas para fazer backup...</p></td>
<td><p>Um backup de VSS completo pode ser selecionado e os arquivos de log serão truncados. No entanto, a restauração do backup estará limitada à restauração de arquivo, já que a restauração no nível de aplicativo não estará disponível.</p></td>
</tr>
</tbody>
</table>


Para obter etapas detalhadas sobre como fazer backup do Exchange usando o WSB, consulte [Usar o Backup do Windows Server para fazer o backup do Exchange](use-windows-server-backup-to-back-up-exchange-exchange-2013-help.md).

Para obter etapas detalhadas sobre como restaurar dados de um backup feito com o WSB, consulte [Usar o Backup do Windows Server para restaurar um backup do Exchange](use-windows-server-backup-to-restore-a-backup-of-exchange-exchange-2013-help.md).

