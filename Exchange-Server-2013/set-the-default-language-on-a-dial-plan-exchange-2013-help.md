---
title: 'Definir o idioma padrão em um plano de discagem: Exchange 2013 Help'
TOCTitle: Definir o idioma padrão em um plano de discagem
ms:assetid: 7a1d2e7e-4053-40af-9ec1-ec714df12ad4
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998914(v=EXCHG.150)
ms:contentKeyID: 50556233
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Definir o idioma padrão em um plano de discagem

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2016-12-09_

Você pode definir o idioma padrão para um plano de discagem de Unificação de mensagens (UM). Cada plano de discagem que você cria inicialmente usará inglês (en-US) como o idioma padrão. O pacote de idioma inglês (en-US) é instalado em todas as versões do MicrosoftExchange Server 2013 e não pode ser removido.

Se você deseja selecionar outro idioma como o idioma padrão, por exemplo, alemão (de-DE), você deve primeiro baixar o alemão UM pacote .exe arquivo de idioma do [Exchange Server 2013 UM pacotes de idiomas](https://go.microsoft.com/fwlink/p/?linkid=266542) e instalar esse pacote de idiomas no servidor de caixa de correio usando o arquivo de instalação UMLanguagePack.de-de.exe. Após ter instalado o pacote de idiomas, você pode definir o idioma padrão para um idioma diferente do inglês (en-US) em seus planos de discagem de Unificação de MENSAGENS.

Para tarefas adicionais relacionadas aos idiomas da UM, consulte [Procedimentos de idiomas, saudações e prompts de Unificação de mensagens](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Planos de discagem de UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para definir o idioma padrão em um plano de discagem de UM

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**.

2.  Na exibição de lista, selecione o plano de discagem de Unificação de MENSAGENS que você deseja modificar e, na barra de ferramentas, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Plano de discagem de UM**, clique em **Configurar**.

4.  Na página **configurações**, em **idioma de áudio**, selecione o idioma que você deseja definir na lista suspensa.

5.  Clique em **Salvar** para aceitar suas alterações.

## Usar o Shell para definir o idioma padrão em um plano de discagem de UM

Este exemplo define o idioma padrão em um plano de discagem de UM chamado `MyUMDialPlan` alemão como.

    Set-UMDialPlan -Identity MyUMDialPlan -DefaultLanguage de-DE

Este exemplo define o idioma padrão em um plano de discagem UM chamado `MyUMDialPlan` como o japonês.

    Set-UMDialPlan -Identity MyUMDialPlan -DefaultLanguage ja-JP

Este exemplo define o idioma padrão em um plano de discagem UM chamado `MyUMDialPlan` como inglês australiano.

    Set-UMDialPlan -Identity MyUMDialPlan -DefaultLanguage en-AU

