---
title: 'Criar certificados para Unificação de mensagens: Exchange 2013 Help'
TOCTitle: Criar certificados para Unificação de mensagens
ms:assetid: 66807ee7-3d3f-482d-a3ac-d4e9baca3271
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn205141(v=EXCHG.150)
ms:contentKeyID: 54651971
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar certificados para Unificação de mensagens

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-04-29_

Você pode usar o assistente de Novo Certificado do Exchange no EAC ou o Shell para criar certificados autoassinados ou solicitações de certificado para um certificado de infraestrutura de chave pública (PKI) interna. Para a Unificação de Mensagens (UM), você pode usar um destes certificados para o serviço de Unificação de Mensagens do Microsoft Exchange e para os serviços do Roteador de Chamadas da Unificação de Mensagens do Microsoft Exchange. Você pode usar o mesmo certificado para os dois serviços ou um certificado diferente para cada serviço. Você também pode adquirir e importar um certificado comercial de terceiros para os serviços de UM. Se você estiver usando um certificado autoassinado para UM, poderá precisar incluir o nome dos seus servidores de Acesso para Cliente e de Caixa de Correio no nome alternativo da entidade (SAN).

Por padrão, ao instalar o Exchange Server 2013, dois certificados autoassinados são criados: **Microsoft Exchange Server Auth Certificate** e **Microsoft Exchange**. O certificado autoassinado do **Microsoft Exchange** pode ser usado pela UM para criptografar dados, mas você deve atribuir o certificado aos serviços de Roteador de Chamada de UM e de UM. Após você atribuir o certificado aos serviços de Unificação de Mensagens, ele pode ser copiado e importado para os gateways VoIP, PBXs IP e PBXs habilitados para SIP. Entretanto, em vez de usar os certificados autoassinados padrão, você pode precisar criar outro especificamente para a Unificação de Mensagens.


> [!CAUTION]
> Os certificados autoassinados não podem ser usados quando você está fazendo integração da UM com o Microsoft Lync server.



Para conhecer tarefas de gerenciamento adicionais relacionadas ao gerenciamento de certificados para Unificação de Mensagens, consulte [Implantar certificados para os procedimentos de Unificação de mensagens](deploying-certificates-for-um-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Gerenciamento de certificado" no tópico [Permissões de infraestrutura do Exchange e do Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) e entrada "Serviço de UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md) . Você também deve fazer logon usando uma conta que seja membro do grupo Administradores local nesse computador.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para criar uma solicitação de certificado para UM

1.  No EAC, navegue até **Servidores** \> **Certificados** e depois clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

2.  Na página **Novo certificado do Exchange**, selecione **Criar uma solicitação para um certificado a partir de uma autoridade de certificação** e depois clique em **Avançar**.

3.  Insira um nome amigável para o certificado e depois clique em **Avançar**.

4.  Se você não precisa de um certificado curinga, clique em **Avançar**. Se você precisa de um certificado curinga, selecione **Solicitar um certificado curinga. Um certificado curinga pode ser usado para proteger todos os subdomínios sob o seu domínio raiz com um único certificado**, insira o nome do domínio raiz e clique em **Avançar**.

5.  Em **Armazenar solicitação de certificado neste servidor**, clique em **Procurar** para ir ao local onde você deseja armazenar o arquivo. Você também pode armazenar a solicitação de certificado em qualquer servidor de Caixa de Correio ou de Acesso para Cliente na sua organização do Exchange. Selecione o local, clique em **OK** e depois clique em **Avançar**.

6.  Se você solicitou um certificado curinga, pule para a etapa 9.

7.  Se você não solicitou um certificado curinga, precisará especificar os domínios que deseja incluir no seu certificado. Se você deseja editar um domínio, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição") e depois clique em **Avançar**.

8.  Em **Com base nas suas seleções, os seguintes domínios serão incluídos no seu certificado. Você pode adicionar mais domínios aqui ou fazer alterações**, você pode adicionar, editar, remover ou verificar o nome dos domínios que estão listados em **Domínio**. Depois clique em **Avançar**.

9.  Em **Especificar informações sobre a sua organização. Isso é exigido pela autoridade de certificação**, insira:
    
      - **Nome da organização**
    
      - **Nome do departamento**
    
      - **Cidade/Localidade**
    
      - **Estado/Província**
    
      - **Nome do País/Região**   Para esta opção, use a lista suspensa para selecionar o país ou região.

10. Em **Salvar a solicitação do certificado no seguinte arquivo**, insira o nome do arquivo do certificado e depois clique em **Concluir**.

## Use o Shell para criar uma solicitação de certificado para UM

Este exemplo cria uma nova solicitação de certificado do Exchange para um servidor de Caixa de Correio chamado `MyMailboxServer` com um nome amigável de `CertUM`.

    New-ExchangeCertificate -FriendlyName 'CertUM' -GenerateRequest -PrivateKeyExportable $true -KeySize '2048' -DomainName '*.northwindtraders.com' -SubjectName 'C=US,S=wa,L=redmond,O=northwindtraders,OU=servers,CN= northwindtraders.com' -Server 'MyMailboxServer'

## Use o EAC para criar um certificado autoassinado para UM

1.  No EAC, navegue até **Servidores** \> **Certificados** e depois clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

2.  Na página **Novo certificado do Exchange**, escolha **Criar um certificado autoassinado** e depois selecione **Avançar**.

3.  Insira um nome amigável para o certificado e depois selecione **Avançar**.

4.  Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") para escolher os servidores Exchange para os quais você deseja aplicar este certificado e depois selecione **Avançar**.

5.  Especifique os domínios que você deseja incluir no seu certificado e depois selecione **Avançar**. Se você deseja adicionar um domínio para um serviço, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

6.  Verifique se os domínios que você incluiu estão corretos e depois selecione **Finalizar**.


> [!IMPORTANT]
> Ao usar o EAC para criar um certificado autoassinado, não será solicitado que você habilite serviços para o certificado. Após o certificado ter sido criado, você pode usar o EAC ou o cmdlet <STRONG>Enable-ExchangeCertificate</STRONG> no Shell para habilitar os serviços do Exchange. Para mais informações sobre como atribuir um certificado aos serviços de UM, veja <A href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">Atribuir um certificado para os serviços de Unificação de mensagens e o roteador de chamada UM</A>.



## Usar o Shell para criar um certificado autoassinado para UM

Este exemplo cria um novo certificado autoassinado do Exchange para um servidor de Caixa de Correio chamado `MyMailboxServer` com um nome amigável de `UMCert`.

    New-ExchangeCertificate -Services 'UM, UMCallRouter' -DomainName '*.northwindtraders.com' -FriendlyName 'UMSelfSigned' -SubjectName 'C=US,S=WA,L=Redmond,O=Northwindtraders,OU=Servers,CN= Northwindtraders.com' -PrivateKeyExportable $true


> [!TIP]
> Ao especificar os serviços que você deseja habilitar usando o parâmetro <EM>Services</EM>, você deverá atribuir esses serviços. Neste exemplo, você deverá habilitar o certificado para os serviços de UM e de Roteador de Chamadas de UM. Para mais informações sobre como habilitar um certificado para serviços, veja <A href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">Atribuir um certificado para os serviços de Unificação de mensagens e o roteador de chamada UM</A>.


