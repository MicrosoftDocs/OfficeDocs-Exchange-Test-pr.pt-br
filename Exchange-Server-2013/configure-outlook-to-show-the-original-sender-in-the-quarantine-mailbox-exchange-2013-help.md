---
title: 'Configurar o Outlook para mostrar o remetente original na caixa de correio de quarentena: Exchange 2013 Help'
TOCTitle: Configurar o Outlook para mostrar o remetente original na caixa de correio de quarentena
ms:assetid: 9249425d-1b06-48a0-ad95-c4eefb641ff4
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee861109(v=EXCHG.150)
ms:contentKeyID: 50486193
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o Outlook para mostrar o remetente original na caixa de correio de quarentena

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

A quarentena de spam é um recurso do agente de Filtro de Conteúdo que reduz o risco de perda de mensagens legítimas. A quarentena de spam fornece um local de repositório temporário para mensagens que estão identificadas como spam e que não devem ser entregues a uma caixa de correio de usuário dentro da organização.

Quando uma mensagem atinge o limite de quarentena de spam, ela é agrupada em uma notificação de falha de entrega e entregue à caixa de correio de quarentena de spam. Como as mensagens em quarentena são armazenadas como NDRs na caixa de correio de quarentena, o endereço do postmaster de sua organização será listado como o endereço De: de todas as mensagens. Entretanto, ter o endereço do remetente original, o endereço do destinatário original e o nível de confiança de spam (SCL) na lista de campos facilitará a localização da mensagem que deseja recuperar.

Por padrão, você não poderá selecionar esses campos no Microsoft Outlook. Para que possa adicionar esses campos na exibição de mensagem, você deverá primeiro criar um formulário do Outlook que adiciona o remetente original, o destinatário original e o SCL original como campos opcionais que podem ser selecionados. Depois de criar este formulário personalizado, você poderá configurar o Outlook para exibir esses campos no modo de exibição de mensagens.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão do procedimento: 15 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Acesso à caixa de correio" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Este procedimento exige que você tenha configurado a caixa de correio de quarentena do antispam. Para obter mais informações, consulte [Configurar uma caixa de correio de quarentena de spam](configure-a-spam-quarantine-mailbox-exchange-2013-help.md) (página em inglês).

  - Para acessar a caixa de correio de quarentena, você precisará configurar um perfil do Outlook para essa caixa de correio e, em seguida, abra a caixa de correio usando o Outlook. Para obter mais informações sobre como configurar e usar vários perfis do Outlook, consulte [Visão geral do Outlook perfis de email](https://go.microsoft.com/fwlink/p/?linkid=178975).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Etapa 1: use o bloco de notas para criar um formulário personalizado do Outlook

1.  Abra o bloco de notas e copie o seguinte código no documento.
    
        [Description]
        MessageClass=IPM.Note
        CLSID={00020D31-0000-0000-C000-000000000046}
        DisplayName=Quarantine Extension Form
        Category=Standard
        Subcategory=Form
        Comment=This form allows the Original Sender (ReceivedRepresentingEmailAddress), Original Recipient (To), and Original SCL (OriginalScl) values to be viewed as columns.
        LargeIcon=IPML.ico
        SmallIcon=IPMS.ico
        Version=3.0
        Locale=enu
        Hidden=1
        Owner=Microsoft Corporation
        Contact=Your Name
        
        [Platforms]
        Platform1=Win16
        Platform2=NTx86
        Platform9=Win95
        
        [Platform.Win16]
        CPU=ix86
        OSVersion=Win3.1
        
        [Platform.NTx86]
        CPU=ix86
        OSVersion=WinNT3.5
        
        [Platform.Win95]
        CPU=ix86
        OSVersion=Win95
        
        [Properties]
        Property01=ReceivedRepresentingEmailAddress
        Property02=DisplayTo
        Property03=OriginalScl
        
        [Property.ReceivedRepresentingEmailAddress]
        Type=31
        NmidInteger=0x0078
        DisplayName=ReceivedRepresentingEmailAddress
        
        [Property.DisplayTo]
        Type=31
        NmidInteger=0x0E04
        DisplayName=DisplayTo
        
        [Property.OriginalScl]
        Type=3
        NmidPropset={41F28F13-83F4-4114-A584-EEDB5A6B0BFF}
        NmidString=OriginalScl
        DisplayName=OriginalScl
        
        [Verbs]
        Verb1=1
        
        [Verb.1]
        DisplayName=&Open
        Code=0
        Flags=0
        Attribs=2
        
        [Extensions]
        Extensions1=1
        
        [Extension.1]
        Type=31
        NmidPropset={00020D0C-0000-0000-C000-000000000046}
        NmidInteger=1
        Value=1000000000000000

2.  Salve o arquivo na pasta Office Forms usando os seguintes valores:
    
      - **Caminho** *\<Caminho de Instalação do Office\>*\\\<*OfficeVersion\>*\\Forms\\*\<LCID\>*
        
          - *\<Caminho de Instalação do Office\>*   Para versões de 32 bits do Office em versões de 32 bits do Microsoft Windows ou versões de 64 bits do Office em versões de 64 bits do Windows, o caminho padrão é `C:\Program Files\Microsoft Office`. Para versões de 32 bits do Office em versões de 64 bits do Windows, o caminho padrão é `C:\Program Files (x86)\Microsoft Office`.
        
          - *\<OfficeVersion\>*   Para o Outlook 2007, o valor é `Office12`. Para o Outlook 2010, o valor é `Office14`. Para o Outlook 2013, o valor é `Office15`.
        
          - *\<LCID\>*   Este é o valor de sua identificação de localidade (LCID). Por exemplo, a LCID para inglês dos EUA é 1033. Para obter mais informações, consulte [KB221435: Lista de identificadores de localidade com suporte no Word](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=221435).
    
      - **Nome**   Para o restante desse procedimento, consideremos que o arquivo tenha o nome `QTNE.cfg`. O nome do arquivo não é importante, mas certifique-se de colocar o valor entre aspas para que o arquivo seja salvo como QTNE.cfg e não como QTNE.cfg.txt.
    
    Por exemplo, para uma versão em inglês dos EUA de 32 bits do Outlook 2013 instalada em uma versão de 64 bits do Windows, salve o arquivo como:
    
        "C:\Program Files (x86)\Microsoft Office\Office15\Forms\1033\QTNE.cfg"
    

    > [!TIP]
    > Se o controle de acesso do usuário do Windows (UAC) impedir que você salve o arquivo no local correto, salve-o primeiro em um local temporário e, em seguida, copie-o.



## Etapa 2: configurar o Outlook para usar o formulário personalizado do Outlook

Use um dos seguintes procedimentos com base na versão do Outlook instalada no seu computador.

## Configurar o Outlook 2010 ou Outlook 2013

1.  No Outlook 2010 ou no Outlook 2013, clique em **Arquivo** \> **Opções** \> **Avançadas**.

2.  Na seção **Desenvolvedores**, clique em **Formulários Personalizados**.

3.  Na caixa de diálogo **Opções**, clique em **Gerenciar Formulários**.

4.  Na caixa de diálogo **Gerenciador de Formulários**, clique em **Instalar**. Navegue até o local do arquivo `QTNE.cfg`, selecione-o e clique em **Abrir**. Na caixa de diálogo **Propriedades do Formulário**, verifique as informações e clique em **OK** para instalar o Formulário de Extensão de Quarentena em sua biblioteca de Formulários Particulares.

5.  Na caixa de diálogo **Gerenciador de Formulários**, clique em **Fechar**. Clique em **OK** duas vezes para fechar as caixas de diálogo restantes e retornar à interface principal do Outlook.

6.  Na guia **Página Inicial**, no modo de exibição de **Email** da caixa de entrada, clique com o botão direito no título da coluna (talvez você precise expandir a largura da lista de mensagens para ver as colunas) e selecione **Configurações de Exibição**.

7.  Na caixa de diálogo **Configurações de Exibição Avançadas**, clique em **Colunas**.

8.  Na caixa de diálogo **Mostrar Colunas**, na lista suspensa **Selecionar colunas disponíveis em**, role até o final da lista e selecione **Formulários**.

9.  Na caixa de diálogo **Selecionar formulários da Empresa para esta pasta**, no campo **Formulários Selecionados**, selecione **Mensagem** e clique em **Remover**. No campo **Formulários Pessoais**, selecione **Formulário de Extensão de Quarentena** e clique em **Adicionar**. Quando terminar, clique em **Fechar**.

10. Na caixa de diálogo **Mostrar Colunas**, na seção **Colunas Disponíveis**, selecione um ou mais dos seguintes campos e clique em **Adicionar** após cada campo selecionado.
    
      - **ReceivedRepresentingEmailAddress**   Remetente original
    
      - **DisplayTo**   Destinatário Original (observe que isso aparece como **Para** após você adicioná-lo)
    
      - **OriginalScl**   SCL original
    
    Use os botões **Mover para Cima** ou **Mover para Baixo** para posicionar as colunas no modo de exibição. Para obter melhores resultados, posicione os três novos campos após o campo **Anexo** e antes do campo **De**. Quando você terminar, clique em **OK** duas vezes para retornar à interface principal do Outlook.

## Configurar o Outlook 2007

1.  Em Outlook 2007, clique em **Ferramentas** \> **Opções**.

2.  Na caixa de diálogo **Opções**, clique na guia **Outro** e, em **Geral**, clique em **Opções Avançadas**.

3.  Na caixa de diálogo **Opções Avançadas**, clique em **Formulários Personalizados** e, na caixa de diálogo **Formulários Personalizados**, clique em **Gerenciar Formulários**.

4.  Na caixa de diálogo **Gerenciador de Formulários**, clique em **Instalar**. Navegue até o local do arquivo `QTNE.cfg`, selecione-o e clique em **Abrir**. Na caixa de diálogo **Propriedades do Formulário**, verifique as informações e clique em **OK** para instalar o Formulário de Extensão de Quarentena em sua biblioteca de Formulários Particulares.

5.  Feche a caixa de diálogo **Gerenciador de Formulários**, clique em **OK** três vezes para fechar as caixas de diálogo restantes e retorne à interface principal do Outlook 2007.

6.  No modo de exibição **Email** da caixa de entrada, clique com o botão direito no título da coluna (talvez você precise expandir a largura da lista de mensagens para ver as colunas) e selecione **Personalizar Modo de Exibição Atual**.

7.  Na caixa de diálogo **Personalizar Exibição: Caixa de diálogo** Mensagens, clique em **Mostrar Campos**.

8.  Na caixa de diálogo **Mostrar Campos**, na lista suspensa **Selecionar campos disponíveis em**, role até o final da lista e selecione **Formulários**.

9.  Na caixa de diálogo **Selecionar formulários da Empresa para esta pasta**, no campo **Formulários Selecionados**, selecione **Mensagem** e clique em **Remover**. No campo **Formulários Pessoais**, selecione **Formulário de Extensão de Quarentena** e clique em **Adicionar**. Quando terminar, clique em **Fechar**.

10. Na caixa de diálogo **Mostrar Campos**, na seção **Campos Disponíveis**, selecione um ou mais dos seguintes campos e clique em **Adicionar** após cada campo selecionado.
    
      - **ReceivedRepresentingEmailAddress**   Remetente original
    
      - **DisplayTo**   Destinatário Original (observe que isso aparece como **Para** após você adicioná-lo)
    
      - **OriginalScl**   SCL original
    
    Use os botões **Mover para Cima** ou **Mover para Baixo** para posicionar as colunas no modo de exibição. Para obter melhores resultados, posicione os três novos campos após o campo **Anexo** e antes do campo **De**. Quando você terminar, clique em **OK** duas vezes para retornar à interface principal do Outlook 2007.

## Como saber se funcionou?

Você saberá se esse procedimento funcionou se conseguir ver o remetente original, o destinatário original ou os valores do SCL original para mensagens em quarentena na caixa de correio de quarentena de spam usando o Outlook.

