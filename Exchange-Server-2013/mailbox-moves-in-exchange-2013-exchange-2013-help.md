---
title: 'Movimentações de caixa de correio no Exchange 2013: Exchange 2013 Help'
TOCTitle: Movimentações de caixa de correio no Exchange 2013
ms:assetid: 9c0a0bc9-2a39-4cf0-aa6e-6e5ef3fd38b5
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150543(v=EXCHG.150)
ms:contentKeyID: 50486255
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Movimentações de caixa de correio no Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-07_

Quando você mover uma caixa de correio, você está movê-lo de um *banco de dados de caixa de correio de origem* para um *banco de dados de caixa de correio de destino*. O banco de dados de caixa de correio de destino pode ser no mesmo servidor, em um servidor diferente, em um domínio diferente, em um site diferente Active Directory ou em outra floresta.

## Motivos para mover caixas de correio

Você pode precisar mover caixas de correio nos seguintes cenários:

  - **Atualizar**   Quando você atualiza de uma organização existente do Exchange Server 2007 ou Exchange Server 2010 Microsoft para Exchange Server 2013, mover caixas de correio dos servidores Exchange existente para um servidor de caixa de correio Exchange 2013.

  - **Realinhamento**   Você pode mover caixas de correio para fins de realinhamento. Por exemplo, convém mover uma caixa de correio de um banco de dados para um banco de dados que tem um limite de tamanho de caixa de correio maior.

  - **Investigar um problema**   Se você precisar investigar um problema com uma caixa de correio, você pode mover essa caixa de correio para um servidor diferente. Por exemplo, você pode mover todas as caixas de correio que tenham alta atividade para outro servidor.

  - **Caixas de correio corrompido**   Se você encontrar caixas de correio corrompidas, você pode mover as caixas de correio para um servidor diferente ou um banco de dados. As mensagens corrompidas não serão movidas.

  - **Alterações de local físico**   Você pode mover caixas de correio para um servidor em um site diferente Active Directory. Por exemplo, se um usuário é movido para outro local físico, você pode mover caixa de correio desse usuário para um servidor local mais próximo para o novo local.

  - **Separação das funções administrativas**   Convém separar a administração de Exchange de administração de conta de sistema operacional Windows. Para fazer isso, você pode mover caixas de correio de uma única floresta em um cenário de floresta de recursos. Neste cenário, as caixas de correio Exchange residem em uma floresta e suas contas de usuário associado Windows residem em uma floresta separada.

  - **Administração de email externo**   Convém terceirizar a administração do email e reter a administração de contas de usuário Windows. Para fazer isso, você pode mover caixas de correio de uma única floresta em um cenário de floresta de recursos.

  - **Administração de conta de email e usuário integra-se**   Convém alterar de um modelo de administração de email separados ou terceirizado para um modelo no qual as contas de usuário e de email podem ser gerenciadas do dentro da mesma floresta. Para fazer isso, você pode mover caixas de correio de um cenário de floresta de recursos a uma única floresta. Neste cenário, o Exchange caixas de correio e contas de usuário Windows residem na mesma floresta.

## Move do Exchange 2013

Microsoft Exchange Server 2013 introduz o conceito de *lote move* e *pontos de extremidade de migração*. Pontos de extremidade de migração são objetos de gerenciamento que descrevem o servidor remoto e as conexões que podem ser associadas um ou mais lotes. E, então, a nova arquitetura de movimentação de lote melhora no serviço de replicação de caixa de correio (MRS) movimentações com a capacidade de gerenciamento aprimoradas. Lote move arquitetura nos recursos Exchange 2013 os seguintes recursos:

  - Capacidade de mover várias caixas de correio em grandes lotes.

  - Notificação por email durante movimentação com emissão de relatórios.

  - Repetição automática e priorização automática de movimentações.

  - Caixas de correio de arquivo morto principais e pessoais podem ser movidas juntas ou separadamente.

  - Opção para finalização de solicitação de movimentação manual, que permite que você examine sua movimentação antes de concluí-la.

  - Sincronizações incrementais periódicas para atualizar alterações de migração.

Em Exchange 2013, você deve mover caixas de correio entre o Exchange 2007 e Exchange 2010 e Exchange 2013 do Centro de administração do Exchange 2013 (EAC) e o Shell de gerenciamento do Exchange.


> [!TIP]
> Você ainda pode executar as movimentações de caixa de correio única em Exchange 2013 semelhante ao Exchange Server 2010 usando o EAC ou os cmdlets do lote solicitar ou migração de movimentação.




> [!TIP]
> Você não pode mover caixas de correio no local de Exchange Server 2003 para Exchange 2013.



Para obter mais informações sobre como gerenciar move novas e existentes, consulte [Gerenciar movimentações de local](manage-on-premises-moves-exchange-2013-help.md).

## Pontos de extremidade de migração

Pontos de extremidade de migração capturam as informações de servidor remoto e as credenciais necessárias para migrar os dados e a fonte de configurações de limitação de persistência. Você pode usar os pontos de extremidade de migração para definir configurações para remoto e move entre florestas. Movimentações locais não exigem o uso de um ponto de extremidade. (Movimentações locais são movimentações que mover caixas de correio entre dois bancos de dados diferentes locais Exchange.)

A lista a seguir mostra os tipos de mudanças que oferecem suporte a pontos de extremidade de migração:

  - **Mover entre florestas**   Mova caixas de correio entre duas florestas de Exchange locais diferentes. Movimentações entre florestas exigem o uso de um ponto de extremidade de RemoteMove Exchange.

  - **Movimentação remota**   Em uma implantação híbrida, uma movimentação remota envolve as migrações de *inclusão* ou de *exclusão* . Movimentações remotas exigem o uso de um ponto de extremidade de RemoteMove. Inclusão Move caixas de correio de uma organização local do Exchange para Exchange on-line no Microsoft Office 365 e usa um ponto de extremidade RemoteMove como o ponto de extremidade de origem do lote de migração. Exclusão Move caixas de correio de Exchange Online em Office 365 para uma organização de Exchange local e usa um ponto de extremidade de RemoteMove Exchange como o ponto de extremidade de destino do lote de migração.

A tabela a seguir mostra os tipos de ponto de extremidade de migração e os valores que podem ser gerenciadas no Exchange 2013.

### Valores de tipos de ponto de extremidade de migração

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>RemoteMove do Exchange</th>
<th>LocalMove do Exchange</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MaxConcurrentMigrations</p></td>
<td><p>MaxConcurrentMigrations</p></td>
</tr>
<tr class="even">
<td><p>RemoteServer</p></td>
<td><p>Site</p></td>
</tr>
<tr class="odd">
<td><p>ArchiveDomain</p></td>
<td><p>Banco de Dados</p></td>
</tr>
<tr class="even">
<td><p>BadItemLimit</p></td>
<td><p>ArchiveDatabase</p></td>
</tr>
<tr class="odd">
<td><p>LargeItemLimit</p></td>
<td><p>BadItemLimit</p></td>
</tr>
<tr class="even">
<td><p>Bancos de dados</p></td>
<td><p>LargeItemLimit</p></td>
</tr>
<tr class="odd">
<td><p>TargetDeliveryDomain</p></td>
<td><p>PrimaryOnly</p></td>
</tr>
<tr class="even">
<td><p>PrimaryOnly</p></td>
<td><p>ArchiveDatabase</p></td>
</tr>
<tr class="odd">
<td><p>ArchiveDatabase</p></td>
<td><p>DAG</p></td>
</tr>
<tr class="even">
<td><p>ArchiveOnly</p></td>
<td><p>Floresta</p></td>
</tr>
</tbody>
</table>


Para obter mais informações sobre pontos de extremidade de migração, consulte a interface do usuário de **migração** no EAC e [New-MigrationEndpoint](https://technet.microsoft.com/pt-br/library/jj218611\(v=exchg.150\)).

Para obter mais informações sobre como gerenciar move novas e existentes, consulte [Gerenciar movimentações de local](manage-on-premises-moves-exchange-2013-help.md).

