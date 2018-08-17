---
title: 'Remover um pacote de idiomas de Unificação de mensagens: Exchange 2013 Help'
TOCTitle: Remover um pacote de idiomas de Unificação de mensagens
ms:assetid: a2bc2753-2c25-4ea0-a9d5-e3d42a699c6c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124004(v=EXCHG.150)
ms:contentKeyID: 50486286
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Remover um pacote de idiomas de Unificação de mensagens

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-14_

Você pode usar o EAC ou o Shell para gerenciar os idiomas de Unificação de mensagens (UM) em servidores de caixa de correio executando o serviço de Unificação de mensagens do Microsoft Exchange. No entanto, para remover um idioma da lista em um plano de discagem de UM, você deve remover o pacote de idiomas de Unificação de mensagens apropriado do servidor de caixa de correio usando o comando **Setup.exe /RemoveUmLanguagePack** . Depois de remover o pacote de idiomas de Unificação de mensagens do servidor de caixa de correio, o idioma não estará disponível quando você configura um plano de discagem ou um atendedor automático. Você pode exibir os pacotes de idiomas de Unificação de mensagens que estão instalados, exibindo as propriedades do servidor de caixa de correio ou usando o cmdlet **Get-UMService** .

Para tarefas adicionais relacionadas aos idiomas da UM, consulte [Procedimentos de idiomas, saudações e prompts de Unificação de mensagens](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Servidor de Caixa de Correio (serviço de UM)" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Verifique se um pacote de idiomas de Unificação de mensagens que não seja en-US é instalado.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Use Setup.exe para remover um pacote de idiomas de Unificação de mensagens

Em um prompt de comando, execute o seguinte comando.

    Setup.exe /RemoveUmLanguagePack:<UmLanguagePackName>

No comando anterior, *\<UmLanguagePackName\>* é o nome do pacote de idiomas de Unificação de mensagens, por exemplo, fr-FR.


> [!CAUTION]
> Você não pode usar o arquivo de Setup.exe que está localizado na pasta \Bin para remover um pacote de idiomas de Unificação de mensagens após ter instalado quaisquer atualizações. Você deve usar o arquivo de Setup.exe de Exchange 2013 DVD ou os arquivos de origem baixados. Se não fizer isso, você verá o seguinte erro: não há uma incompatibilidade de versões entre o aplicativo em execução e o aplicativo instalado.


