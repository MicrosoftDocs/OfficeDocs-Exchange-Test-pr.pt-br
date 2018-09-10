---
title: 'Gerenciar dicas de política: Exchange 2013 Help'
TOCTitle: Gerenciar dicas de política
ms:assetid: cec50a35-1d00-47b3-b72f-ac1bb0fd630e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ619307(v=EXCHG.150)
ms:contentKeyID: 50484804
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar dicas de política

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Dicas de política são informativos avisos que são exibidos para remetentes de email enquanto eles compõem uma mensagem. A finalidade da dica de política é instruir os usuários que podem ser violam as práticas de negócios ou políticas que você estiver aplicando com as políticas de prevention (DLP) de perda de dados que você tiver estabelecido. Os procedimentos a seguir ajudarão você a começar a usar as dicas de política. Assista a este vídeo para saber mais.

> [!VIDEO https://www.microsoft.com/pt-br/videoplayer/embed/dd629bb7-063d-49f3-b7e1-8f2e0aa4de13]

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 30 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada \&quot;Prevenção de perda de dados (DLP)\&quot; no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - As Dicas de Política serão exibidas apenas para remetentes de email apenas quando as seguintes condições forem atendidas:
    
    1.  O programa cliente de mensagens do remetente é o Microsoft Outlook 2013. Se a sua organização tiver implantado o Exchange 2013 SP1 ou estiver usando o Exchange Online, as Dicas de Política também aparecerão no Outlook Web App e no OWA para dispositivos.
    
    2.  Existe uma regra de transporte que invoca as notificações de Dica de Política. Você pode criar uma regra de transporte configurando uma política de DLP que inclui a ação **Notificar o remetente com uma Dica de Política**.
    
    3.  O conteúdo de um cabeçalho da mensagem, corpo da mensagem ou anexo de mensagem verificado pelo seu agente de transporte atende às condições estabelecidas nas políticas ou regras de DLP que também incluem as regras de notificação de Dica de Política. Colocada de outra forma, a Dica de Política será exibida aos usuários finais apenas se eles fizerem algo que faça a regra associada agir.

  - O texto de notificação padrão da Dica de Política integrado ao sistema será exibido se você não usar o recurso de configurações de Dica de Política para personalizar seu texto de Dica de Política. Para saber mais sobre o texto padrão, consulte [Dicas de política](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/data-loss-prevention/policy-tips).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Criar ou modificar uma Dica de Política somente de notificação

Esse procedimento resulta em uma Dica de Política informativa sendo mostrada a um remetente de email quando as condições de uma regra específica são atendidas. No Microsoft Outlook, o remetente pode impedir que esse tipo de dica seja exibido usando uma caixa de diálogo de opções de Dicas de Política. Para configurar o texto da Dica de Política personalizada, consulte Create custom Policy Tip notification text.

## Usar o EAC para configurar Dicas de Política somente de notificação

1.  No EAC, navegue até **Gerenciamento de conformidade** \> **Prevenção de perda de dados**.

2.  Clique duas vezes em uma das políticas que aparecem na sua lista de políticas ou realce um item e selecione **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Editar política de DLP**, clique em **Regras**.

4.  Para adicionar Dicas de Política a uma regra existente, realce a regra e selecione **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").
    
    Para adicionar uma nova regra em branco que você possa personalizar completamente, selecione **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") e depois selecione **Criar uma nova regra** .

5.  Em **Aplicar esta regra se**, selecione **A mensagem contém informações confidenciais**. Essa condição é obrigatória.

6.  Selecione ![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"), selecione os tipos de informações confidenciais, selecione **Adicionar**, depois **OK** e outra vez **OK**.

7.  Na caixa **Faça o seguinte**, selecione **Notificar o remetente com uma Dica de Política** e selecione uma opção na lista suspensa **Escolha se a mensagem é bloqueada ou se pode ser enviada**; por fim, selecione **OK**.

8.  Se quiser adicionar condições ou ações, na parte inferior da janela, selecione **Mais opções**.
    

    > [!TIP]
    > Somente as seguintes condições podem ser usadas: 
    > <UL>
    > <LI>
    > <P><STRONG>SentTo (o destinatário é)</STRONG></P>
    > <LI>
    > <P><STRONG>SentToScope (o destinatário está localizado)</STRONG></P>
    > <LI>
    > <P><STRONG>De (o remetente é)</STRONG></P>
    > <LI>
    > <P><STRONG>FromMemberOf (o remetente é um membro de)</STRONG></P>
    > <LI>
    > <P><STRONG>FromScope (o remetente está localizado)</STRONG></P></LI></UL>As seguintes ações não podem ser usadas: 
    > <UL>
    > <LI>
    > <P><STRONG>RejectMessageReasonText (rejeitar a mensagem e incluir uma explicação)</STRONG></P>
    > <LI>
    > <P><STRONG>RejectMessageEnhancedStatusCode (rejeitar a mensagem com o código de status avançado)</STRONG></P>
    > <LI>
    > <P><STRONG>DeletedMessage (excluir a mensagem sem notificar ninguém)</STRONG></P></LI></UL>



9.  Na lista **Escolha um modo para essa regra**, selecione se deseja que a regra seja imposta. Recomendamos testar a regra primeiro.

10. Selecione **Salvar** para finalizar as modificações da regra e salvar as alterações.

## Como saber se funcionou?

Para verificar se você criou com êxito uma Dica de Política que apenas notificará um remetente, faça o seguinte:

1.  No EAC, navegue até **Gerenciamento de conformidade** \> **Prevenção de perda de dados**.

2.  Selecione a política que você espera que contenha uma mensagem de notificação.

3.  Selecione **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição") e depois selecione **Regras**.

4.  Selecione a regra específica que você espera que contenha uma mensagem de notificação.

5.  Confirme se sua ação **Notificar o remetente** aparece na parte inferior do resumo de regra.

## Criar ou modificar uma Dica de Política de mensagem de bloqueio

Esse procedimento resulta em uma Dica de Política sendo mostrada a um remetente de email que indica que uma mensagem é rejeitada e não será entregue até a condição problemática não estar mais presente. O remetente recebe a opção de indicar que sua mensagem de e-mail não inclui a condição problemática. Isso também é conhecido como uma sobreposição de falso positivo. Se o remetente indicar isso, a mensagem poderá deixar a caixa de saída para que o relatório do usuário seja auditado. No entanto, o Exchange bloqueará o envio da mensagem. Para configurar o texto da Dica de Política personalizada, consulte Create custom Policy Tip notification text.

## Usar o EAC para configurar Dicas de Política de mensagem de bloqueio

1.  No EAC, navegue até **Gerenciamento de conformidade** \> **Prevenção de perda de dados**.

2.  Clique duas vezes em uma das políticas que aparecem na sua lista de políticas ou realce um item e selecione **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Editar política de DLP**, clique em **Regras**.

4.  Para adicionar Dicas de Política a uma regra existente, realce a regra e selecione **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

5.  Para adicionar uma nova regra em branco, que você possa personalizar completamente, selecione **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

6.  Para adicionar uma ação que revelará uma Dica de Política, selecione **Mais opções…** e depois selecione o botão **Adicionar ação**.

7.  Na lista suspensa, selecione **Notificar o remetente com uma Dica de Política** e selecione **Bloquear a mensagem**.

8.  Selecione **OK** e **Salvar** para finalizar a modificação da regra e salvar suas alterações.

## Como saber se funcionou?

Para verificar se você criou com êxito uma Dica de Política de mensagem de rejeição, faça o seguinte:

1.  No EAC, navegue até **Gerenciamento de conformidade** \> **Prevenção de perda de dados**.

2.  Selecione uma vez para realçar a política que você espera que contenha uma mensagem de notificação.

3.  Selecione **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição") e depois selecione **Regras**.

4.  Selecione uma vez para realçar a regra específica que você espera que contenha uma mensagem de notificação.

5.  Confirme se sua ação **Avise o remetente que a mensagem não pode ser enviada** aparece na parte inferior do resumo de regra.

## Criar ou modificar uma Dica de Política de substituição exceto bloquear

Há quatro opções de Dicas de Política que pode rejeitar mensagens ou impedir que mensagens saiam da caixa de saída do remetente. Para saber mais sobre essas opções, consulte [Dicas de política](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/data-loss-prevention/policy-tips).

## Usar o EAC para configurar Dicas de Política de substituição exceto bloquear

1.  No EAC, navegue até **Gerenciamento de conformidade** \> **Prevenção de perda de dados**.

2.  Selecione duas vezes uma das políticas que aparecem na sua lista de políticas ou realce um item e selecione **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Editar política de DLP**, selecione **Regras**.

4.  Para adicionar Dicas de Política a uma regra existente, realce a regra e selecione **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").
    
    Para adicionar uma nova regra em branco que você possa personalizar completamente, selecione **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") e depois **Mais opções…**

5.  Para adicionar a ação que revelará uma Dica de Política, selecione o botão **Adicionar ação**.

6.  Na lista suspensa, selecione **Notificar o remetente com uma Dica de Política** e selecione **Bloquear a mensagem, mas permitir que o remetente sobreponha e envie**.

7.  Selecione **OK** e **Salvar** para finalizar a modificação da regra e salvar suas alterações.

## Como saber se funcionou?

Para verificar se você criou com êxito uma Dica de Política de substituição exceto rejeitar, faça o seguinte:

1.  No EAC, navegue até **Gerenciamento de conformidade** \> **Prevenção de perda de dados**.

2.  Selecione uma vez para realçar a política que você espera que contenha uma mensagem de notificação.

3.  Selecione **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição") e depois selecione **Regras**.

4.  Selecione uma vez para realçar a regra específica que você espera que contenha uma mensagem de notificação.

5.  Confirme se sua ação **Bloquear a mensagem, mas permitir que o remetente sobreponha e envie** aparece na parte inferior do resumo de regra.

## Criar texto de notificação da Dica de Política personalizada

Este procedimento opcional o ajudará a personalizar o texto de notificação da Dica de Política que os remetentes de email visualizam em seus programas de email. Se você fizer isso, tenha em mente que o texto da notificação da Dica de Política personalizada não será exibido, a não ser que você também configure uma regra de política de DLP com uma ação que faça com que a notificação apareça. Tenha em mente que há notificações de Dica de Política de sistema padrão que poderão ser mostradas se você não personalizar seu texto de notificação de Dica de Política. Para saber mais sobre o texto padrão, consulte [Dicas de política](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/data-loss-prevention/policy-tips).

## Usar o EAC para criar e gerenciar texto de notificação da Dica de Política personalizada

1.  No EAC, navegue até **Gerenciamento de conformidade** \> **Prevenção de perda de dados**.

2.  Selecione **Configurações de Dica de Política**![Configurações das dicas de políticas](images/JJ619307.54d1813d-3289-4765-a9a3-a7303a5ab3c7(EXCHG.150).gif "Configurações das dicas de políticas").

3.  Para adicionar uma nova Dica de Política com sua própria mensagem personalizada, selecione **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Para obter mais informações sobre as opções de ação disponíveis, consulte [Dicas de política](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/data-loss-prevention/policy-tips).
    
    Para modificar uma Dica de Política existente, realce a dica e selecione **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").
    
    Para excluir uma Dica de Política existente, realce-a e selecione **Excluir**![Excluir ícone](images/JJ673559.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Excluir ícone") e então confirme a ação.

4.  Selecione **Salvar** para finalizar a modificação da Dica de Política e salvar suas alterações.

5.  Selecione **Fechar** para finalizar o gerenciamento das suas Dicas de Política e salvar suas alterações.

## Usar o Shell para criar texto de notificação da Dica de Política personalizada

O seguinte exemplo cria uma nova Dica de Política no idioma inglês que impedirá o envio de uma mensagem. O texto desta Dica de Política personalizada é alterado para o seguinte valor: "Esta mensagem parece conter conteúdo restrito e não será entregue."

    New-PolicyTipConfig -Name en\Reject -Value "This message appears to contain restricted content and will not be delivered."

Para obter mais informações sobre cmdlets de DLP, consulte [Cmdlets de política e conformidade](https://technet.microsoft.com/pt-br/library/dd298082\(v=exchg.150\)).

## Usar o Shell para modificar texto de notificação da Dica de Política personalizada

O exemplo a seguir modifica uma Dica de Política somente de notificação e no idioma inglês existente. O texto dessa Dica de Política personalizada é alterado para "O envio de números de conta bancária não é recomendado."

    Set-PolicyTipConfig en\NotifyOnly "Sending bank account numbers in email is not recommended."

Para obter mais informações sobre cmdlets de DLP, consulte [Cmdlets de política e conformidade](https://technet.microsoft.com/pt-br/library/dd298082\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você criou com êxito o texto da Dica de Política personalizada, faça o seguinte:

1.  No EAC, navegue até **Gerenciamento de conformidade** \> **Prevenção de perda de dados**.

2.  Selecione **Configurações de Dica de Política**![Configurações das dicas de políticas](images/JJ619307.54d1813d-3289-4765-a9a3-a7303a5ab3c7(EXCHG.150).gif "Configurações das dicas de políticas").

3.  Selecione **Atualizar**![Ícone Atualizar](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "Ícone Atualizar").

4.  Confirme se a ação, a localidade e o texto dessa localidade aparecem na lista.

## Para obter mais informações

[Prevenção de perda de dados](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Dicas de política](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/data-loss-prevention/policy-tips)

[Regras de fluxo de emails ou de transporte](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) Exchange 2013

[Regras de fluxo de emails (regras de transporte) no Exchange Online](https://technet.microsoft.com/pt-br/library/jj919238\(v=exchg.150\)) Exchange Online

[Dicas de email do Exchange 2010](https://go.microsoft.com/fwlink/?linkid=265179)

