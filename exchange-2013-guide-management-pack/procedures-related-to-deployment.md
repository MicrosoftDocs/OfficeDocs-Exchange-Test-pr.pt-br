---
title: Procedimentos Relacionados à Implantação
TOCTitle: Procedimentos Relacionados à Implantação
ms:assetid: 6b7682bd-fe3d-43b9-a7db-66c0ac17656f
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn195909(v=EXCHG.150)
ms:contentKeyID: 53275642
ms.date: 08/29/2014
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Procedimentos Relacionados à Implantação

 

_**Tópico modificado em:**  2013-04-17_

Esta seção contém os procedimentos que você pode usar como referência para o Pacote de Gerenciamento do Exchange Server 2013. Para procedimentos relacionados à operação pós-implantação, veja [Procedures related to post-deployment operation](procedures-related-to-post-deployment-operation.md)

## Verifique o status de implantação do agente

Antes de importar o Pacote de Gerenciamento do Exchange Server 2013, verifique se os agentes SCOM no seus servidores do Exchange estão operacionais e se a integridade do seu sistema operacional está sendo relatada corretamente no SCOM.

Sua conta de usuário precisa ser um membro da função Administradores do Operations Manager para realizar esse procedimento.

1.  Faça logon no seu servidor SCOM e abra o console SCOM.

2.  Clique em **Monitoramento** e depois clique em **Computadores Windows**.

3.  Certifique-se de que todos os seus servidores Exchange exibem **Íntegro**.

![Agentes adequados no console do SCOM](images/Dn195909.7d1ff0bb-419e-40dc-babf-5fa2fb7229a8(EXCHG.150).png "Agentes adequados no console do SCOM")

## Verifique a configuração do proxy do agente

Antes de importar o Pacote de Gerenciamento do Exchange Server 2013, verifique se o proxy do agente está habilitado para descoberta no SCOM. Senão, os agentes nos seus servidores do Exchange não relatarão o status de integridade do Exchange. Você precisa verificar esta configuração para todos os Servidores Exchange.

Sua conta de usuário precisa ser um membro da função Administradores do Operations Manager para realizar esse procedimento.

1.  Faça logon no seu servidor SCOM e abra o console SCOM.

2.  No console de Operações, clique em **Administração**.

3.  Clique em **Agente Gerenciado**. , clique com o botão direito no servidor Exchange, e depois selecione **Propriedades**.

4.  Na guia **Segurança** , verifique se a caixa de seleção **Permitir que este agente funcione como um proxy e descubra objetos gerenciados em outros computadores** está selecionada.

5.  Clique em **OK**.

## Verifique a configuração de segurança do agente

Devido ao modelo de segurança usado para testar o Exchange 2013, não há suporte para executar o agente SCOM nos seus servidores Exchange com uma conta que não seja a **SistemaLocal** . Se você executar o agente com qualquer outra conta que não seja a SistemaLocal, as transações sintéticas não serão executadas. Você também pode ter outros problemas.

A sua conta precisa ser um membro do grupo da função Gerenciamento de Servidor para realizar este procedimento.

1.  Fala logon no seu servidor Exchange.

2.  Clique em **Iniciar** \> **Ferramentas Administrativas** \> **Serviços**.

3.  Role a lista de serviços para baixo para encontrar o serviço de **Gerenciamento do System Center** .

4.  Verifique se a coluna **Fazer Logon Como** exibe **Sistema Local**.

5.  Se a coluna **Fazer Logon Como** exibir algo diferente disso, altere o logon do serviço para Sistema Local.
    
    1.  Clique com o botão direito no serviço de **Gerenciamento do System Center** e selecione **Propriedades**.
    
    2.  Selecione a guia **Fazer Logon** .
    
    3.  Clique na opção **Conta do Sistema Local** .
    
    4.  Clique em **OK**.

