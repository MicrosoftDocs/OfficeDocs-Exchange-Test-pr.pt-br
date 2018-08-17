---
title: 'Configurar o serviço de disponibilidade para topologias entre florestas'
TOCTitle: Configurar o serviço de disponibilidade para topologias entre florestas
ms:assetid: f1e7d407-f0d3-47a7-8cc3-03c5980445d5
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb125182(v=EXCHG.150)
ms:contentKeyID: 52058891
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o serviço de disponibilidade para topologias entre florestas

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-10-22_

O serviço de Disponibilidade melhora as informações de livre/ocupado dos funcionários ao proporcionar dados seguros, consistentes e atualizados de livre/ocupado a clientes que executam o MicrosoftOutlook. Por padrão, esse serviço é instalado com o Exchange Server 2013. Em topologias entre florestas, em que todos os clientes se conectando executam o Outlook, o serviço de Disponibilidade é o único método de recuperação de informações de disponibilidade. Você pode usar o Shell para configurar o serviço de Disponibilidade para topologias entre florestas.


> [!NOTE]
> Você não pode usar o EAC para configurar o serviço de Disponibilidade entre florestas.



## Usar o serviço de Disponibilidade em florestas confiáveis e não confiáveis

O serviço de Disponibilidade pode ser usado em topologias entre florestas confiáveis e não confiáveis. O tipo de informação de disponibilidade que está disponível depende da utilização de uma floresta confiável ou não confiável.

**Florestas Confiáveis**   Nesse tipo de floresta, você pode configurar o serviço de Disponibilidade para recuperar as informações de livre/ocupado de cada usuário. Quando o serviço de Disponibilidade estiver configurado para recuperar informações de disponibilidade por usuário, pode fazer solicitações entre florestas em nome de um usuário particular. Isso permite que um usuário em uma floresta remota recupere informações detalhadas de disponibilidade de alguém que não esteja na mesma floresta.

**Florestas Não Confiáveis**   Nesse tipo de floresta, você só pode configurar o serviço de Disponibilidade para recuperar as informações de livre/ocupado na organização. Quando o serviço de Disponibilidade fizer solicitações de disponibilidade entre florestas no nível organizacional, as informações são retornadas para cada usuário da organização. Em florestas não confiáveis, não é possível controlar o nível das informações de disponibilidade retornadas por usuário.

## Configurar o Windows para topologias entre florestas

Por padrão, uma lista de endereços global (GAL) contém destinatários de email de uma única floresta. Se você tiver um ambiente entre florestas, recomendamos usar o Microsoft Identity Lifecycle Manager (ILM) 2007 Feature Pack 1 (FP1) para assegurar que a GAL, em qualquer floresta, tenha destinatários de email de outras florestas. O ILM 2007 FP1 cria usuários de email que representam destinatários de outras florestas, permitindo assim que os usuários os exibam na GAL e enviem email. Por exemplo, os usuários na Floresta A aparecem como usuário de email na Floresta B e vice-versa. Os usuários na floresta de destino podem selecionar o objeto de usuário de email que representa um destinatário em outra floresta para enviar email.

Para habilitar a sincronização da GAL, crie agentes de gerenciamento que importam usuários, contatos e grupos habilitados para email de serviços designados do Active Directory em um metadiretório centralizado. No metadiretório, os objetos habilitados para email são representados como usuários de email. Os grupos são representados como contatos sem nenhum membro associado. Em seguida, os agentes de gerenciamento exportam esses usuários de email para uma unidade organizacional na floresta de destino especificada.

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Permissões de Serviço de Disponibilidade" no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o Shell para configurar informações de disponibilidade por usuário em uma topologia entre florestas confiável

Este exemplo configura o serviço de Disponibilidade para recuperar informações de disponibilidade, por usuário, em um servidor de caixas de correio na floresta de destino.

    Get-MailboxServer | Add-ADPermission -Accessrights Extendedright -Extendedrights "ms-Exch-
    EPI-Token-Serialization" -User "<Remote Forest Domain>\Exchange servers"

Este exemplo define o método de acesso de disponibilidade usado pelo serviço de Disponibilidade no servidor de caixas de correio na floresta de origem. O servidor local de caixas de correio está configurado para acessar informações de disponibilidade na floresta ContosoForest.com, por usuário. Este exemplo usa a conta de serviço para recuperar informações de disponibilidade.

    Add-AvailabilityAddressSpace -Forestname ContosoForest.com -AccessMethod PerUserFB -UseServiceAccount:$true


> [!NOTE]
> Para configurar a disponibilidade bidirecional entre florestas, repita essas etapas na floresta de destino.



Se optar por configurar a disponibilidade entre florestas com confiabilidade, e por usar uma conta de serviço (ao invés de especificar credenciais para toda a empresa ou por usuário), você deve estender as permissões, conforme mostrado no exemplo da seção "Usar o Shell para configurar a disponibilidade entre florestas confiáveis com uma conta de serviço". A execução desse procedimento na floresta de destino dá aos servidores de caixas de correio da floresta de origem a permissão para serializar o contexto original do usuário.

## Usar o Shell para configurar a disponibilidade entre florestas confiáveis com uma conta de serviço

Este exemplo configura a disponibilidade entre florestas confiáveis com uma conta de serviço.

    Get-MailboxServer | Add-ADPermission -Accessrights Extendedright -Extendedright "ms-Exch-EPI-Token-Serialization" -User "<Remote Forest Domain>\Exchange servers"

Para obter informações detalhadas sobre sintaxe e parâmetros, consulte os seguintes tópicos:

  - [Get-MailboxServer](https://technet.microsoft.com/pt-br/library/bb123539\(v=exchg.150\))

  - [Add-ADPermission](https://technet.microsoft.com/pt-br/library/bb124403\(v=exchg.150\))

  - [Add-AvailabilityAddressSpace](https://technet.microsoft.com/pt-br/library/bb124122\(v=exchg.150\))

  - [Set-AvailabilityConfig](https://technet.microsoft.com/pt-br/library/bb124103\(v=exchg.150\))

## Usar o Shell para configurar informações de disponibilidade para toda a empresa em uma topologia entre florestas não confiável

Este exemplo define a conta de toda a organização no objeto de configuração da disponibilidade para configurar o nível de acesso para informações de disponibilidade na floresta de destino.

    Set-AvailabilityConfig -OrgWideAccount "Contoso.com\User"

Este exemplo adiciona o objeto de configuração de espaço de endereçamento de Disponibilidade para a floresta de origem.

    $a = Get-Credential (Enter the credentials for organization-wide user in Contoso.com domain)
    Add-AvailabilityAddressspace -Forestname Contoso.com -Accessmethod OrgWideFB -Credential:$a

