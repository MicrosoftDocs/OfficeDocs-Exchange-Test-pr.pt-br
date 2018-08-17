---
title: 'Criar uma regra de proteção do Outlook: Exchange 2013 Help'
TOCTitle: Criar uma regra de proteção do Outlook
ms:assetid: da64750d-faaf-44de-ad8c-888eba7fbdbf
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd638196(v=EXCHG.150)
ms:contentKeyID: 50486816
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar uma regra de proteção do Outlook

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Usando regras de proteção do Microsoft Outlook, você pode proteger mensagens com o gerenciamento de direitos de informação (IRM) aplicando um modelo de Rights Management Services (AD RMS) do Active Directory no Outlook 2010 antes que as mensagens são enviadas.

Para tarefas de gerenciamento adicionais relacionadas a IRM, consulte [Procedimentos de gerenciamento de direitos de informação](information-rights-management-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Proteção por direitos" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Você deve ter um servidor [AD RMS](https://technet.microsoft.com/en-us/library/hh831364.aspx) implantado na mesma floresta que o servidor que executa o Microsoft Exchange Server 2013Active Directory.

  - Se você configurar regras de proteção de Outlook às mensagens de proteger o IRM, considere habilitar a descriptografia de transporte permitir que os agentes de transporte, incluindo o agente de regras de transporte, para descriptografar e acessar a mensagem. Se você usar o registro no diário, você também deve considerar a habilitação de descriptografia do relatório de diário permitir que o agente de registro no diário salvar uma cópia não criptografada da mensagem no relatório de diário. Para obter mais informações, consulte [Criptografia do relatório de diário](journal-report-decryption-exchange-2013-help.md).

  - Você não pode usar o Centro de administração do Exchange (EAC) para criar regras de proteção de Outlook. Você deve usar o Shell.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o Shell para criar uma regra de proteção do Outlook

Este exemplo cria a regra de proteção de Outlook Project Contoso. A regra protege as mensagens enviadas para o grupo de distribuição de ContosoPMs com o modelo de AD RMS Business Critical.

    New-OutlookProtectionRule -Name "Project Contoso" -SentTo "DL-ContosoPMs@contoso.com" -ApplyRightsProtectionTemplate "Business Critical"


> [!NOTE]
> Quando você usa o predicado <CODE>SentTo</CODE> para uma regra de proteção de Outlook e especificar um grupo de distribuição, somente as mensagens endereçadas ao grupo de distribuição no para, Cc ou Cco campos são protegidas por IRM. Proteção de IRM não é aplicada às mensagens endereçadas a membros individuais do grupo de distribuição.



Você também pode usar os predicados `FromDepartment` e `SentToScope` para aplicar a proteção IRM a mensagens enviadas de usuários no departamento especificado ou as mensagens enviadas para o escopo especificado (`InOrganization` para mensagens internas, `All` para todos os destinatários).

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [New-OutlookProtectionRule](https://technet.microsoft.com/pt-br/library/dd298182\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você criou com êxito uma regra de proteção do Outlook, faça o seguinte:

  - Execute o cmdlet [Get-OutlookProtectionRule](https://technet.microsoft.com/pt-br/library/dd298004\(v=exchg.150\)) para certificar-se de que a regra foi criada e visualizar as propriedades da regra. Para obter um exemplo de como recuperar uma regra de proteção do Outlook, consulte os [Examples](https://technet.microsoft.com/pt-br/dd298004\(exchg.150\)#examples) em **Get-OutlookProtectionRule**.

  - Use Outlook 2010 para criar uma mensagem de teste que atenda a condição da regra e certificar-se de que a regra for acionada no cliente.
    

    > [!NOTE]
    > Pode levar algum tempo para que uma regra de proteção do Outlook esteja disponível no Outlook.


