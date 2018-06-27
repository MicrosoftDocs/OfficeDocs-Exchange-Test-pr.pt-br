---
title: 'Selecione o idioma para um atendedor automático: Exchange 2013 Help'
TOCTitle: Selecione o idioma para um atendedor automático
ms:assetid: 3a1c1ec0-c726-41fb-a294-59faab205609
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997306(v=EXCHG.150)
ms:contentKeyID: 50556165
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Selecione o idioma para um atendedor automático

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2016-12-09_

Você pode configurar a definição de idioma de prompt padrão em um atendedor automático de UM (Unificação de Mensagens). A definição de idioma disponível em um atendedor automático da UM permite configurar o idioma de prompt padrão no atendedor automático. Ao usar os prompts padrão do sistema para o atendedor automático, esse é o idioma que o chamador ouvirá sempre que o atendedor automático responder à chamada de entrada. Essa definição de idioma afeta apenas os prompts do sistema padrão que são fornecidos depois que você instalou o servidor de Caixa de Correio que executa o serviço de Unificação de Mensagens do Microsoft Exchange. Essa configuração não terá efeito sobre os prompts personalizados configurados em um atendedor automático. Os idiomas disponíveis baseiam-se nos pacotes de idiomas da Unificação de Mensagens instalados no servidor de Caixa de Correio.

Cada atendedor automático que você cria inicialmente usará inglês (en-US) como o idioma padrão. O pacote de idiomas inglês (en-US) é instalado por padrão em todas as versões do Microsoft Exchange 2013 e não pode ser removido. Se você deseja selecionar outro idioma, por exemplo, alemão (de-DE), você deve primeiro baixar o alemão UM idioma .exe arquivo pack do [Exchange Server 2013 UM pacotes de idiomas](https://go.microsoft.com/fwlink/?linkid=266542) e instalar o pacote de idiomas de Unificação de MENSAGENS no servidor de caixa de correio usando o arquivo de instalação UMLanguagePack.de-de.exe. Após ter instalado o pacote de idioma de Unificação de MENSAGENS, você pode definir o idioma padrão para um idioma diferente do inglês (en-US) em atendedores automáticos.

Para tarefas adicionais relacionadas aos idiomas da UM, consulte [Procedimentos de idiomas, saudações e prompts de Unificação de mensagens](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Atendedores automáticos da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem de UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se um plano de discagem de UM foi criado. Para obter etapas detalhadas, consulte [Criar um Atendedor Automático da UM](create-a-um-auto-attendant-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para definir a configuração de idioma padrão

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**.

2.  Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e, na barra de ferramentas, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **plano de discagem de UM**, em **Atendedores Automáticos da UM**, selecione o atendedor automático da UM que deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

4.  Na página **Geral**, em **Idioma para interface de voz automática**, selecione o idioma necessário na lista suspensa.

5.  Clique em **Salvar** para aceitar suas alterações.

## Usar o Shell para definir a configuração de idioma padrão

Este exemplo define o inglês da Grã-Bretanha como idioma padrão no atendedor automático da UM `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -Language en-GB

Este exemplo define o inglês da Grã-Bretanha como idioma padrão no atendedor automático da UM `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -Language de-DE

