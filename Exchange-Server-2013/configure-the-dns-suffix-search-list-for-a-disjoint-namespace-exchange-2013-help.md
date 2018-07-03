---
title: 'Configurar a lista de pesquisa de sufixo DNS para um namespace separado: Exchange 2013 Help'
TOCTitle: Configurar a lista de pesquisa de sufixo DNS para um namespace separado
ms:assetid: cfa715ac-7b69-47c3-b206-933ec2cf677b
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb847901(v=EXCHG.150)
ms:contentKeyID: 50486692
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar a lista de pesquisa de sufixo DNS para um namespace separado

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Este tópico explica como usar o console de gerenciamento de diretiva de grupo (GPMC) para configurar a lista de pesquisa de sufixo do sistema de nome de domínio (DNS). Em alguns cenários de Exchange 2013 da Microsoft, se você tiver um namespace separado, você deve configurar a lista de pesquisa de sufixo DNS para incluir vários sufixos DNS.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 10 minutos

  - Para executar este procedimento, a conta utilizada deve ser delegada a associação ao grupo Administradores de domínio.

  - Confirme que você instalou .NET Framework 3.0 no computador no qual você instalará o GPMC.
    

    > [!TIP]
    > A versão atual do GPMC que podem ser baixados do Microsoft Download Center opera nas versões de 32 bits dos sistemas operacionais Windows Server 2003 e Windows XP e pode gerenciar remotamente os objetos de diretiva de grupo em controladores de domínio de 32 bits e 64 bits. Esta versão do GPMC não inclui uma versão de 64 bits e a versão de 32 bits não é executada em plataformas de 64 bits. A versão de 32 bits do Windows Server 2008 e a versão de 32 bits do Windows Vista ambas incluem uma versão de 32 bits do GPMC. A versão de 64 bits do Windows Server 2008 e a versão de 64 bits do Windows Vista ambas incluem uma versão de 64 bits do GPMC.



  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Use o GPMC para configurar a lista de pesquisa de sufixo DNS

1.  Em um computador de 32 bits em seu domínio, instale o GPMC com Service Pack 1 (SP1). Para obter informações de download, consulte o [Console de gerenciamento de diretiva de grupo com Service Pack 1](https://go.microsoft.com/fwlink/p/?linkid=100126).
    

    > [!TIP]
    > Se você tiver um computador no domínio executando Windows Server 2008 ou Windows Vista, você pode ignorar esta etapa.



2.  Clique em **Iniciar** \> **programas** \> **Ferramentas administrativas** \> **gerenciamento de diretiva de grupo**.

3.  Em **Gerenciamento de Política de Grupo**, expanda a floresta e o domínio em que se aplicará a Política de Grupo. Clique com o botão direito do mouse em **Objetos de Política de Grupo** e, em seguida, clique em **Novo**.

4.  Em **Novo GPO**, digite um nome para a política e clique em **OK**.

5.  Com o botão direito na nova política criada na etapa 4 e clique em **Editar**.

6.  No **Editor de gerenciamento de diretiva de grupo**, expanda **Configuração do computador**, expanda **diretivas**, expanda **Modelos administrativos**, expanda **rede** e clique em **Cliente DNS**.

7.  Clique com o botão **Lista de pesquisa de sufixo DNS**, clique em **All Tasks** e clique em **Editar**.

8.  Na página **Propriedades da Lista de Pesquisa de Sufixo DNS**, selecione **Habilitado**. Na caixa **Sufixos DNS**, digite o sufixo DNS principal do computador separado, o nome de domínio DNS e quaisquer espaços para nome adicionais de outros servidores com os quais o Exchange possa interoperar, como servidores de monitoramento ou servidores para aplicativos de terceiros. Clique em **OK**.

9.  Em **Gerenciamento de diretiva de grupo**, expanda **Objetos de diretiva de grupo** e, em seguida, selecione a política que você criou na etapa 4. Na guia **escopo**, o escopo a política para que ele se aplica somente aos computadores que estão separado.

## Como saber se funcionou?

Para verificar se você concluiu com êxito a migração, faça o seguinte:

  - Após instalar Exchange 2013, verifique se que você pode enviar mensagens de email dentro e fora da sua organização.

## Para saber mais

[Diretiva de grupo do Windows Server](https://go.microsoft.com/fwlink/p/?linkid=100128)

[Diretiva de grupo](https://go.microsoft.com/fwlink/?linkid=268043)

[Cenários de namespace separado](disjoint-namespace-scenarios-exchange-2013-help.md)

