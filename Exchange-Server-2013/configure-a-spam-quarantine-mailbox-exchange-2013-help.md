---
title: 'Configurar uma caixa de correio de quarentena de spam: Exchange 2013 Help'
TOCTitle: Configurar uma caixa de correio de quarentena de spam
ms:assetid: 907d2f90-2a62-4d59-a4cf-945fef2e963f
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb123746(v=EXCHG.150)
ms:contentKeyID: 50486171
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar uma caixa de correio de quarentena de spam

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2013-02-19_

Mensagens consideradas como spam pelo agente de Filtro de Conteúdo podem ser direcionadas a uma caixa de correio de quarentena de spam. Se o limite de quarentena do nível de confiança de spam (SCL) estiver habilitado, todas as mensagens em quarentena serão classificadas como notificações de falha (NDR) e enviadas ao endereço SMTP especificado como a caixa de correio de quarentena de spam. Você pode examinar mensagens em quarentena e liberá-las para seus destinatários pretendidos usando o recurso Enviar Novamente no Microsoft Outlook.

## O que você precisa saber antes de começar?

  - Tempo estimado para a conclusão desta tarefa: 45 minutos.

  - Por padrão, os recursos antispam não estão habilitados no serviço de Transporte em um servidor de Caixa de Correio. Normalmente, você apenas habilita os recursos antispam em um servidor de Caixa de Correio se sua organização do Exchange não realiza nenhuma ação antes da filtragem antispam antes de aceitar mensagens de entrada. Para saber mais, confira [Habilitar a funcionalidade anti-spam em servidores de caixa de correio](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - A pessoa responsável pela caixa de correio de quarentena de spam pode exibir mensagens particulares e confidenciais em potencial e depois enviar emails em nome de qualquer pessoa na organização do Exchange.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Como fazer isso?

## Etapa 1: verificar se a filtragem de conteúdo está habilitada

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Recursos de antispam" no tópico [Permissões antispam e antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

1.  Execute o comando abaixo para verificar se o agente Filtro de Conteúdo está instalado e habilitado no servidor Exchange:
    
        Get-TransportAgent "Content Filter Agent"

2.  Execute o seguinte comando para verificar se a filtragem de conteúdo está habilitada:
    
        Get-ContentFilterConfig | Format-List Enabled

Para saber mais, confira [Gerenciar filtragem de conteúdo](manage-content-filtering-exchange-2013-help.md).

## Etapa 2: criar uma caixa de correio dedicada de quarentena de spam

Para criar uma caixa de correio de quarentena de spam dedicada, siga estas etapas:

  - **Criar um banco de dados dedicado do Exchange**   É recomendável que você crie um banco de dados dedicado para a caixa de correio de quarentena de spam. A caixa de correio de quarentena de spam deve ter um banco de dados grande, pois, se o limite de cota de armazenamento for atingido, mensagens serão perdidas. Para saber mais, confira [Gerenciar bancos de dados de caixa de correio no Exchange 2013](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md).

  - **Criar uma caixa de correio e uma conta de usuário dedicadas**   Recomendamos que você crie uma caixa de correio e uma conta de usuário do Active Directory dedicadas para a caixa de correio de quarentena de spam. Para saber mais, confira [Criar caixas de correio do usuário](create-user-mailboxes-exchange-2013-help.md).
    
    Você pode aplicar políticas de destinatário, como gerenciamento de registros de mensagens, cotas de caixa de correio e direitos de delegação, de acordo com as necessidades e as políticas de conformidade da organização. Para saber mais, confira [Gerenciamento de registros de mensagens](messaging-records-management-exchange-2013-help.md).
    

    > [!TIP]
    > Se uma mensagem em quarentena for rejeitada por causa de uma cota de armazenamento, a mensagem será perdida. O Exchange não gera NDRs para mensagens em quarentena porque as mensagens em quarentena são encapsuladas como NDRs.



  - **Configurar o Outlook**   Você precisa configurar as permissões de acesso delegado do Outlook de acordo com as necessidades de sua organização. Além disso, recomendamos que você configure o perfil do Outlook para mostrar os campos `Sender[#0x0069001E]`, `Recipient[#0x0E04001E]` e `Bcc[#0x0E02001E]` originais no modo de exibição **Mensagem**. Para saber mais, confira [Liberar mensagens em quarentena da caixa de correio de quarentena de spam](release-quarantined-messages-from-the-spam-quarantine-mailbox-exchange-2013-help.md).

## Etapa 3: especificar a caixa de correio de quarentena de spam

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Recursos de antispam" no tópico [Permissões antispam e antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

Execute o seguinte comando:

    Set-ContentFilterConfig -QuarantineMailbox <SmtpAddress>

Este exemplo envia todas as mensagens que excedem o limite de quarentena de spam para spamQ@contoso.com.

    Set-ContentFilterConfig -QuarantineMailbox spamQ@contoso.com

## Como saber se essa etapa funcionou?

Para verificar se a caixa de correio de quarentena de spam foi especificada com êxito, siga este procedimento:

1.  Execute o seguinte comando:
    
        Get-ContentFilterConfig | Format-List QuarantineMailbox

2.  Verifique se o valor apresentado é o valor que você configurou.

## Etapa 4: configurar o limite de quarentena de SCL

O limite de quarentena de SCL é o valor com o qual uma determinada mensagem identificada como possível spam será entregue na caixa de correio de quarentena de spam. Você pode definir o limite de quarentena de SCL como um valor de 0 a 9, onde 0 é a menor probabilidade de spam e 9 é a maior probabilidade de spam.

Para saber mais sobre como ajustar os limites de SCL de acordo com as necessidades da organização e sobre como ajustar os limites de SCL por destinatário, confira [Gerenciar filtragem de conteúdo](manage-content-filtering-exchange-2013-help.md).

## Etapa 5: gerenciar a caixa de correio de quarentena de spam

Ao gerenciar sua caixa de correio de quarentena de spam, siga estas diretrizes:

  - Libere os itens que foram enviados à caixa de correio de quarentena de spam usando o recurso Enviar Novamente no Outlook para reenviar a mensagem original.
    
    Para saber mais, confira [Liberar mensagens em quarentena da caixa de correio de quarentena de spam](release-quarantined-messages-from-the-spam-quarantine-mailbox-exchange-2013-help.md).

  - Monitore a caixa de correio de quarentena de spam para que seu tamanho permaneça em um intervalo aceitável. O volume das mensagens de email poderá mudar devido a um conjunto de destinatários maior, à tendência natural de mensagens cada vez maiores ou ao limite na ação de quarentena de SCL.

  - Monitore a caixa de correio de quarentena de spam para detectar falsos positivos. Se a sua caixa de correio de quarentena de spam incluir vários falsos positivos, ajuste o seu limite de quarentena de SCL. Para obter mais informações sobre como determinar por que falsos positivos estão sendo entregues na caixa de correio de quarentena de spam, confira [Carimbos anti-spam](anti-spam-stamps-exchange-2013-help.md).

  - Use o mesmo perfil do Outlook para recuperar mensagens em quarentena da caixa de correio de quarentena de spam. Não há suporte para a aplicação de permissões a um perfil do Outlook diferente para recuperar mensagens. Não é possível usar um perfil do Outlook diferente para recuperar ou liberar mensagens da caixa de correio de quarentena de spam.


> [!IMPORTANT]
> As NDRs identificadas como spam são excluídas, mesmo que sua classificação de SCL indique que elas devem permanecer em quarentena. As NDRs não são entregues na caixa de correio de quarentena de spam. Para controlar essas mensagens, use o log do agente ou o log de controle de mensagens. Para saber mais, confira <A href="anti-spam-agent-logging-exchange-2013-help.md">Log de agente de anti-spam</A>.



## Etapa 6: ajustar o limite de quarentena de SCL

Depois de configurar o limite de quarentena de SCL, monitore periodicamente as configurações e ajuste-as com base nas necessidades de sua organização. Por exemplo, se muitos falsos positivos forem filtrados para a caixa de correio de quarentena de spam, eleve o limite de quarentena de SCL. Para saber mais sobre como ajustar o limite de quarentena de SCL, confira [Limite do Nível de Confiança de Spam](spam-confidence-level-threshold-exchange-2013-help.md).

