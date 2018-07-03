---
title: 'Preparar a caixas de correio para movimentações entre florestas usando código de exemplo: Exchange 2013 Help'
TOCTitle: Preparar a caixas de correio para movimentações entre florestas usando código de exemplo
ms:assetid: f35ac7a5-bb84-4653-b6d0-65906e93627b
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee861124(v=EXCHG.150)
ms:contentKeyID: 50486990
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Preparar a caixas de correio para movimentações entre florestas usando código de exemplo

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Microsoft Exchange 2013 oferece suporte a movimentações de caixa de correio e migrações usando os cmdlets **New-MoveRequest** e **New-MigrationBatch** . Você também pode mover a caixa de correio por meio do Centro de administração do Exchange (EAC). Você pode mover uma caixa de correio de uma floresta de Exchange de fonte para uma floresta de Exchange 2010 de destino.

Para executar **New-MoveRequest**, um usuário de email deve existir na floresta de destino de Exchange e o usuário de email deve ter um conjunto mínimo de atributos necessários Active Directory. Você pode criar um usuário de email necessários na floresta de destino de Exchange Personalizando a implantação do Microsoft Identity Lifecycle Manager (ILM) 2007. O código de amostra de extensão de regras baseadas em ILM descrito neste tópico demonstra como personalizar sua implantação atual do ILM para criar usuários habilitados para email necessários na floresta de Exchange 2013 de destino.

Para obter mais informações sobre como preparar para movimentações entre florestas, incluindo descrições dos atributos necessários Active Directory, consulte [Preparar a caixas de correio para solicitações de movimentação entre florestas](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Baixe o código de amostra da página [preparar para mover de caixa de correio Online](https://go.microsoft.com/fwlink/p/?linkid=177882) no Microsoft Download Center.

  - Para executar o código de exemplo, você precisa ILM 2007 Feature Pack 1 Service Pack 1 (SP1). Para baixar o feature pack, consulte o artigo da Base de Conhecimento Microsoft 977791, [que Service Pack 1 (compilação 3.3.1139.2) está disponível para Identity Lifecycle Manager 2007 Feature Pack 1](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=977791).

  - Você também precisará dos seguintes itens:
    
      - Uma floresta de origem que esteja executando o Exchange 2013, em que a caixa de correio reside atualmente.
    
      - Uma floresta de destino com o Exchange 2013 instalado, para onde a caixa de correio será movida.

  - Para conectar a floresta de destino Exchange 2013, você deve ter a permissão apropriada para chamar o cmdlet **UpdateRecipient** . Para ver quais permissões você precisa, consulte a seção "Permissões de provisionamento do destinatário" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md) .

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Como fazer isso?

## Etapa 1: Instalar o código de amostra do ILM

1.  No Microsoft Visual Studio 2008, abra Microsoft.Exchange.Sample.OneWayGALSync.sln para exibir o código de exemplo. O código de exemplo inclui o seguinte:
    
      - Microsoft.MetadirectoryServicesEx.dll é o arquivo binário que é fornecido com o ILM 2007 FP1 SP1 em "\\Program Files\\Microsoft Identity Integration Server\\Bin\\Assemblies?. Ele é referenciado pelo código de exemplo.
    
      - OneWaySync.xml é referenciado pelo código de exemplo.
    
      - A pasta de ILMServerConfig contém os arquivos de configuração de ILM para o agente de gerenciamento de fonte (MA), o destino MA e o metaverso do ILM (MV).
    
      - Microsoft.Exchange.Sample.OneWayGALSync.MARules.dll e Microsoft.Exchange.Sample.OneWayGALSync.MVRules.dll (construída a partir de código de exemplo) estão sob "\\obj\\Debug?

2.  No servidor ILM, copie o seguinte \\Program Files\\Microsoft Identity Integration server\\extensions.:
    
      - OneWaySync.xml
    
      - Microsoft.Exchange.Sample.OneWayGALSync.MARules.dll
    
      - Microsoft.Exchange.Sample.OneWayGALSync.MVRules.dll

3.  Edite o arquivo OneWaySync.xml que você copiou na pasta Extensões de ILM na etapa 1 para especificar o distinguishedName (DN) do contêiner TargetOU na floresta de Exchange de destino no qual você deseja criar os usuários de email. Você pode usar LDP.exe ou ADSIEdit.exe para procurar o contêiner TargetOU se você não souber qual é o seu nome.
    

    > [!TIP]
    > Se você estiver usando esta amostra junto com o ILM 2007 do GalSync exclua esse contêiner da lista de contêineres gerenciados por GalSync2007.



4.  No Console do Gerenciador de identidades do ILM, vá para o **arquivo** \> **Importar a configuração do servidor** para importar a configuração do servidor ILM da pasta ILMServerConfig. Essa ação importará dois agentes de gerenciamento de Active Directory junto com o esquema do metaverso e a regra de provisionamento.
    

    > [!TIP]
    > Durante a importação, você deve fornecer o nome da floresta e as credenciais e as partições do importados Active Directory agente de gerenciamento (ADMA) para o nome da partição faz a correspondência de sua configuração para a origem e o destino ADMAs.



5.  Para o ADMA oferecer suporte a floresta de destino Exchange 2013, na página **Criação do agente de gerenciamento**, no painel **Configurar extensões**, selecione **Exchange 2013** no menu suspenso **provisão para** e insira o URI remota do Windows PowerShell de um servidor de acesso para cliente Exchange 2010 no **URI de RPS do Exchange 2013**.
    
    **Criar página de agente de gerenciamento**
    
    ![Provisionamento do Agente de Gerenciamento do Exchange 2010](images/Aa998597.8f403cda-e5e4-4edf-887f-c1ed46cee3f5(EXCHG.150).gif "Provisionamento do Agente de Gerenciamento do Exchange 2010")  

6.  No Console do Gerenciador de identidades do ILM no painel de **Criação do agente de gerenciamento**, abra as **Propriedades** para o agente de gerenciamento de floresta de origem. Selecione o Assistente de **Partições do diretório de configurar** e, em seguida, clique em **contêineres** para selecionar o contêiner que conterá as caixas de correio que for mover para a floresta de destino. Desmarque as seleções para todos os outros contêineres, ou seja, o agente de gerenciamento apenas gerenciar este um contêiner de escopo. Da mesma forma, para a floresta de destino MA, selecione o recipiente ao qual usuários habilitados para email serão provisionados, ou seja, o TargetOU especificado na etapa 2.
    

    > [!TIP]
    > Se você estiver usando esta amostra junto com o ILM 2007 do GalSync, exclua ambos desses contêineres da lista de contêineres gerenciados por GalSync 2007.



7.  Execute uma importação completa inicial (estágio) de destino, MAs, para que o ILM pode descobrir o TargetOU especificado na etapa 2.

## Etapa 2: Criar o usuário de email na floresta do Exchange de destino

Agora que você instalou o código de exemplo, use o procedimento a seguir para criar o usuário de email necessários na floresta de Exchange de destino para que **New-MoveRequest** possa ser executado para realizar uma movimentação de caixa de correio online.

1.  Na floresta de origem, use o Centro de administração do Exchange para criar usuários de caixa de correio no contêiner selecionado na etapa 4 "Instalar o código de amostra do ILM". Você também pode usar Active Directory usuários e computadores para mover usuários de caixa de correio existente para o contêiner.

2.  Execute a importação Delta e sincronização Delta executado na fonte de MA descubram as caixas de correio adicionadas ao contêiner de origem e provisionar usuários de email para o MA de destino.

3.  Execute o destino MA para exportar os usuários de email provisionados na etapa 1 para o destino Active Directory de execução de exportação.

4.  Execute a importação Delta no destino MA para confirmar as alterações exportadas na etapa 2.

5.  Na floresta de destino, abra o Exchange Shell de gerenciamento e use o cmdlet de **New-MoveRequest** para mover caixas de correio da floresta de origem.

## Como saber se funcionou?

Para verificar se você concluiu com êxito a migração, faça o seguinte:

  - Da floresta de destino, verifique se os usuários que você moveu da floresta de origem estão presentes na floresta de destino.

