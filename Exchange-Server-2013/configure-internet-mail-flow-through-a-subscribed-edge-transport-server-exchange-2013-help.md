---
title: 'Configurar fluxo de emails por um servidor de Transporte de Borda inscrito'
TOCTitle: Configurar o fluxo de mensagens da Internet por meio de um servidor de Transporte de Borda inscrito
ms:assetid: d12ea770-99ce-4ab4-a373-96f2554641fa
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb738158(v=EXCHG.150)
ms:contentKeyID: 61183359
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o fluxo de mensagens da Internet por meio de um servidor de Transporte de Borda inscrito

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-08_

Para estabelecer as mensagens da Internet por meio de um servidor de Transporte de Borda, inscreva o servidor de Transporte de Borda em um site do Active Directory. Isso cria automaticamente os dois conectores de Envio exigidos para o fluxo de mensagens da Internet:

  - Um conector de Envio configurado para enviar emails de saída a todos os domínios da Internet.

  - Um conector de Envio configurado para enviar emails de entrada do servidor de Transporte de Borda ao servidor de Caixa de Correio do Exchange 2013.

Se você não quiser inscrever o servidor de Transporte de Borda em um site do Active Directory, poderá criar manualmente os conectores de Envio necessários para estabelecer o fluxo de mensagens entre o servidor de Caixa de Correio e o servidor de Transporte de Borda. Para obter mais informações, consulte [Configurar o fluxo de emails da Internet através de um servidor de transporte de borda sem usar o EdgeSync](configure-internet-mail-flow-through-an-edge-transport-server-without-using-edgesync-exchange-2013-help.md). No entanto, recomendamos a inscrição do servidor de Transporte de Borda no site do Active Directory sempre que possível.

## Antes de você começar

  - Tempo estimado para conclusão: 20 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "EdgeSync" e "Servidores de Transporte de Borda" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Antes de inscrever um servidor de Transporte de Borda para sua organização, será necessário configurar os domínios autoritativos e as políticas de endereço de email para sua organização do Exchange.

  - Habilite a porta LDAP segura 50636/TCP no firewall separando sua rede de perímetro da organização do Exchange. O servidor de Transporte de Borda precisa ser capaz de se comunicar com todos os servidores de Caixa de Correio do Exchange 2013 no site do Active Directory inscrito.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Configurar o fluxo de mensagens da Internet por meio de um servidor de Transporte de Borda inscrito

1.  No servidor de Transporte de Borda, crie o arquivo de Inscrição de Borda usando a seguinte sintaxe.
    
        New-EdgeSubscription -FileName <FileName>.xml [-Force]
    
    O exemplo a seguir cria um arquivo de Inscrição de Borda chamado EdgeSubscriptionInfo.xml na pasta C:\\Meus Documentos. O parâmetro *Force* suprime os prompts que confirmam os comandos que serão desabilitados e os avisos de que os dados de configuração serão substituídos no servidor de Transporte de Borda.
    
    ```powershell
New-EdgeSubscription -FileName "C:\My Documents\EdgeSubscriptionInfo.xml" -Force
```

2.  Copie o arquivo de Inscrição de Borda resultante em um servidor de Caixa de Correio no site do Active Directory em que você está inscrevendo o servidor de Transporte de Borda.

3.  No servidor de Caixa de Correio, para importar o arquivo de Inscrição de Borda, use a seguinte sintaxe.
    
        New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "<FileName>.xml" -Encoding Byte -ReadCount 0)) -Site <SiteName>
    
    Este exemplo importa o arquivo de Inscrição de Borda chamado EdgeSubscriptionInfo.xml da pasta D:\\Data e inscreve o servidor de Transporte de Borda no site do Active Directory chamado "Default-First-Site-Name".
    
        New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "D:\Data\EdgeSubscriptionInfo.xml" -Encoding Byte -ReadCount 0)) -Site "Default-First-Site-Name"
    

    > [!NOTE]
    > Você pode usar os parâmetros <EM>CreateInternetSendConnector</EM> ou <EM>CreateInboundSendConnector</EM> para impedir a criação automática de um ou ambos os Conectores de envio exigidos. Para obter mais informações, consulte <A href="edge-subscriptions-exchange-2013-help.md">Inscrições de Borda</A>.



4.  No servidor de Caixa de Correio, execute o seguinte comando para iniciar a primeira sincronização do EdgeSync.
    
    ```powershell
Start-EdgeSynchronization
```

5.  Depois de concluir, recomendamos a exclusão do arquivo de Inscrição de Borda do servidor de Transporte de Borda e do servidor de Caixa de Correio. O arquivo de Inscrição de Borda contém informações sobre credenciais usadas durante o processo de comunicação LDAP.

