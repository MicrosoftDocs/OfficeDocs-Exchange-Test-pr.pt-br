---
title: 'Criar uma regra de proteção de transporte: Exchange 2013 Help'
TOCTitle: Criar uma regra de proteção de transporte
ms:assetid: 3a857185-ee16-4ee7-9e57-8be95f7e753a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd302432(v=EXCHG.150)
ms:contentKeyID: 50485397
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar uma regra de proteção de transporte

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Você pode usar regras de proteção de transporte para aplicar proteção de direitos persistente a mensagens com base em propriedades, como remetente, destinatário, assunto da mensagem e conteúdo.


> [!WARNING]
> Antes de criar regras de transporte em seu ambiente de produção, recomendamos criá-las em um ambiente de teste e testá-las exaustivamente. As regras de transporte criadas neste tópico são exemplos. Você pode criar regras de transporte usando os valores e predicados de regra de transporte apropriados com base em suas necessidades.



Para ver outras tarefas de gerenciamento relacionadas ao IRM (Gerenciamento de Direitos de Informação), consulte [Procedimentos de gerenciamento de direitos de informação](information-rights-management-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2-5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Regras de transporte" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Um servidor executando o [Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx) deve estar disponível em sua organização e contém modelos de RMS existentes.

  - Se você configurar regras de proteção de transporte para proteger mensagens usando IRM e também usar o registro em diário, considere habilitar a descriptografia de relatório de diário para permitir que o agente de Registro no Diário salve uma cópia sem criptografia da mensagem no relatório de diário. Para mais informações, consulte [Criptografia do relatório de diário](journal-report-decryption-exchange-2013-help.md).

  - Depois de criar uma regra de proteção de transporte, se a regra não puder ser aplicada a mensagens porque um servidor do AD RMS não está disponível, as mensagens serão enfileiradas pelo serviço de Transporte nos servidores de Caixa de Correio. Dependendo do volume dessas mensagens, espaço em disco adicional pode ser consumido nos servidores de Caixa de Correio. O Exchange vai tentar proteger a mensagem com IRM três vezes. Depois dessas tentativas, se o servidor AD RMS não puder ser alcançado ou se a mensagem não puder ser protegida com IRM, uma notificação de falha na entrega (NDR) será enviada ao remetente.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o EAC para criar uma regra de proteção de transporte

1.  Navegue até **Fluxo de email** \> **Regras**.

2.  No modo de exibição de lista, clique em **Novo**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

3.  Em **Nova Regra**, primeiro clique em **Mais opções** e preencha estes campos:
    
      - **Nome**   Digite um nome para a regra de transporte.
    
      - **Aplicar essa regra se**   Selecione uma condição e insira quaisquer valores exigidos por ela. Para adicionar condições, clique em **Adicionar Condição**.
        

        > [!IMPORTANT]
        > Se você não selecionar nenhuma condição, ao criar uma regra de proteção de transporte, todas as mensagens manipuladas por servidores Exchange 2013&nbsp;com o serviço de Transporte instalado em sua organização são protegidos com IRM. A proteção de todas as mensagens com IRM requer mais recursos. Sendo assim, recomendamos que você planeje a implantação do seu servidor de Caixa de Correio e do AD&nbsp;RMS de forma apropriada.

    
      - **Faça o seguinte**   Selecione **Aplicar proteção de direitos à mensagem com** e use a caixa de diálogo **Selecionar modelo RMS** para selecionar um modelo.
    
      - **Exceto se**   (Opcional) Clique em **Adicionar exceção**, para especificar uma exceção à regra.

4.  Clique em **Salvar**, para criar a regra de transporte.

## Usar o Shell para criar uma regra de proteção de transporte

  - Para criar uma regra de proteção de transporte, você precisa ter modelos de RMS existentes em sua implantação do AD RMS. Este exemplo recupera os modelos disponíveis do seu cluster do AD RMS.
    
    ```powershell
Get-RMSTemplate | format-list
```
    
    Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-RMSTemplate](https://technet.microsoft.com/pt-br/library/dd297960\(v=exchg.150\)).

  - Este exemplo cria a regra de proteção de transporte Protect-BusinessCriticalProject. A regra protege com IRM mensagens que contenham a expressão "Business Critical" no campo Assunto com o modelo **Não Encaminhar**.
    

    > [!NOTE]
    > O predicado <CODE>SubjectContainsWords</CODE> é usado nesse exemplo. Você pode usar qualquer combinação de predicados de regra de transporte para formar as condições e exceções da regra. Para informações sobre os predicados disponíveis, consulte <A href="mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md">Condições de regra de transporte (predicados)</A>.

    
        New-TransportRule -Name "Protect-BusinessCriticalProject" -SubjectContainsWords "Business Critical" -ApplyRightsProtectionTemplate "Do Not Forward"
    
    Para informações detalhadas de sintaxes e de parâmetros, consulte [New-TransportRule](https://technet.microsoft.com/pt-br/library/bb125138\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você criou com êxito uma regra de proteção de transporte, siga um destes procedimentos:

  - Use o EAC para verificar se a regra foi criada e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição"), para exibir as propriedades da regra.

  - Use o cmdlet [Get-TransportRule](https://technet.microsoft.com/pt-br/library/aa998585\(v=exchg.150\)) para recuperar a regra. Para um exemplo de como recuperar uma regra, consulte [Examples](https://technet.microsoft.com/pt-br/aa998585\(exchg.150\)#examples), em **Get-TransportRule**.

  - Usando o Outlook, o Outlook Web App ou um dispositivo móvel, envie uma mensagem de teste que atenda às condições da regra e verifique se a mensagem recebida pelo destinatário está protegida por IRM.

