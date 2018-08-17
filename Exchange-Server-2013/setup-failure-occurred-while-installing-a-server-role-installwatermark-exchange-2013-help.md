---
title: 'Ocorreu falha na instalação ao instalar uma função de servidor'
TOCTitle: Falha na instalação ocorreu durante a instalação role_InstallWatermark um servidor
ms:assetid: ad89ebd5-f9bb-40c1-8811-09b145c2b341
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.installwatermark(v=EXCHG.150)
ms:contentKeyID: 50486386
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Falha na instalação ocorreu durante a instalação role\_InstallWatermark um servidor

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2016-12-09_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Instalação do Microsoft Exchange Server 2007 não pode continuar porque uma falha de instalação anterior ocorreu durante a instalação de uma função de servidor.

Requer a instalação do Exchange 2007 que uma instalação da função de servidor com falha ser com êxito reinstalado ou removidos do processo de instalação, antes de continuar com qualquer outra tarefa de configuração.

Para resolver esse problema, reinstale apenas as funções de servidor com falha, ou remova as funções de servidor.

Reinstalar a função de servidor com falha da linha de comando

1.  Abra uma janela de Prompt de comando e navegue até os arquivos de instalação.

2.  Execute o seguinte comando:
    
        Setup /roles:<Failed Server Role>
    
    Selecione uma ou mais das seguintes funções, em uma lista separada por vírgulas:
    
    ClientAccess (ou autoridade de certificação ou C)
    
    EdgeTransport (ou ET ou F)
    

    > [!NOTE]
    > A função de servidor de transporte de borda não pode coexistir no mesmo computador com nenhuma outra função de servidor.

    

    > [!NOTE]
    > Você deve implantar a função de servidor de transporte de borda na rede de perímetro e fora da floresta Active Directory.

    
    HubTransport (ou HT ou H)
    
    Caixa de correio (ou MB ou M)
    
    UnifiedMessaging (ou UM ou U)
    
    ManagementTools (ou MT ou T)
    

    > [!NOTE]
    > Se você especificar ManagementTools, você instalará o Exchange Console de gerenciamento, os cmdlets Exchange para Exchange Shell de gerenciamento, Exchange o arquivo de Ajuda, Exchange Best Practices Analyzer Tool e Exchange Assistente de solução de problemas. Se você instalar qualquer outra função de servidor, as ferramentas de gerenciamento serão instaladas automaticamente.

    
    Por exemplo, para adicionar a função de servidor de transporte de Hub a um servidor de caixa de correio existente, digite o seguinte: **%LocalExchangeInstallationDir%\\bin\\Setup.com /role:HubTransport /Mode**


> [!NOTE]
> Se qualquer função de servidor do Exchange Server 2007 instalado anteriormente com êxito, o assistente será executado no modo de manutenção do programa de instalação. Se nenhuma função de servidor do Exchange 2007 anteriormente foram instaladas com êxito, o Assistente de instalação será iniciado de onde foi interrompido.



Usar o Assistente de instalação do Exchange Server 2007 no modo de manutenção para reinstalar a função de servidor com falha

1.  Faça logon no servidor para o qual você deseja reinstalar a uma função de servidor.

2.  Abra o painel de controle e, em seguida, clique duas vezes em **Adicionar ou remover programas**.

3.  Na página **alterar ou remover programas**, selecione **Microsoft Exchange Server** e, em seguida, clique em **Alterar**.

4.  No Assistente de instalação Exchange Server 2007, na página do **Modo de manutenção do Exchange**, clique em **Avançar**.

5.  Na página **Seleção da função de servidor**, marque as caixas de seleção para as funções de servidor que você deseja instalar e clique em **Avançar**.
    

    > [!NOTE]
    > A função de servidor de transporte de borda não pode coexistir no mesmo computador com nenhuma outra função de servidor.

    

    > [!NOTE]
    > Você deve implantar a função de servidor de transporte de borda na rede de perímetro e fora da floresta Active Directory.

    

    > [!NOTE]
    > Se você selecionar ferramentas de gerenciamento, você instalará o Exchange Console de gerenciamento, os cmdlets do Exchange para Exchange Shell de gerenciamento e o arquivo de Ajuda Exchange. As ferramentas de gerenciamento serão instaladas automaticamente se você instalar qualquer outra função de servidor.



6.  Se você selecionou a **Função Transporte de Hub**, e se você estiver instalando Exchange 2007 em uma floresta que tem um existente Exchange Server 2003 ou Exchange 2000 Server organização, na página **Configurações de fluxo de email**, selecione um servidor bridgehead na organização existente que seja membro do Exchange 2003 ou grupo de roteamento Exchange 2000 ao qual você deseja criar um conector de grupo de roteamento.

7.  Na página **Verificações de preparação**, exibir o status para determinar se a organização e a server role verificações de pré-requisito forem concluídas com êxito. Se eles foram concluídas com êxito, clique em **instalar** para instalar o Exchange 2007.

8.  Na página **Conclusão**, clique em **Concluir**.

Para usar o Assistente de instalação do Exchange Server 2007 para reinstalar a função de servidor com falha quando nenhuma outra função de servidor foi previamente instalado com sucesso

1.  Siga as orientações em "Como para executar a instalação usando o Exchange Server 2007 instalação personalizada" ([https://go.microsoft.com/fwlink/?LinkId=86648](https://go.microsoft.com/fwlink/?linkid=86648)) na documentação do produto Exchange Server 2007.

Para remover a função de servidor com falha

1.  Siga as orientações em "Como para remover o Exchange 2007 Server Roles" ([https://go.microsoft.com/fwlink/?LinkId=86649](https://go.microsoft.com/fwlink/?linkid=86649)) na documentação do produto Exchange Server 2007.

## Para Obter Mais Informações

Para obter mais informações sobre como instalar o Exchange 2007 no modo autônomo, consulte "Como para instalar o Exchange 2007 no modo autônomo" ([https://go.microsoft.com/fwlink/?LinkId=86476](https://go.microsoft.com/fwlink/?linkid=86476)).

