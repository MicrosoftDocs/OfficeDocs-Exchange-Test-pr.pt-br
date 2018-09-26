---
title: 'Configurar a filtragem para usar os dados de domínio seguro de conteúdo'
TOCTitle: Configurar a filtragem para usar os dados de domínio seguro de conteúdo
ms:assetid: 1ee2b663-b4f3-4fef-8954-986f2d820924
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn467930(v=EXCHG.150)
ms:contentKeyID: 59635875
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar a filtragem para usar os dados de domínio seguro de conteúdo

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-12-16_

Dados de domínio seguro são um domínio inteiro (por exemplo, @contoso.com) é armazenado na lista de remetentes confiáveis do usuário. Por padrão, o agente Filtro de conteúdo não usa dados domínios seguros para identificar remetentes que são permitidos para ignorar a filtragem de conteúdo.

Essa configuração padrão ajuda a reduzir a quantidade de spam é entregue em sua organização. Por exemplo, um usuário pode adicionar o domínio de um provedor de email grande à sua lista de remetentes seguros. Se esse domínio é frequentemente usado ou falsificado por remetentes de spam, e filtragem de conteúdo está configurado para usar dados domínios seguros para marcar as mensagens como seguros, mensagens de qualquer remetente no domínio poderiam ser entregue aos destinatários na sua organização.

Recomendamos que você não modifique a configuração padrão na maioria dos casos. No entanto, você pode configurar os dados dos usuários de domínio seguro para ser armazenado em Active Directory e usado por para marcar as mensagens como seguros de filtragem de conteúdo. Para fazer isso, você precisará modificar o arquivo de configuração de aplicativo XML MSExchangeMailboxAssistants.exe.config associado com o serviço de assistentes de caixa de correio do Microsoft Exchange, conforme detalhado neste tópico. Quando você faz com que essa configuração alteração, os dados de domínio seguro é em hash e armazenados no atributo de objeto de usuário de cada usuário **msExchSafeSenderHash** em Active Directory como parte de agregação de lista segura. O agente de filtro de conteúdo, em seguida, pode usar os dados de domínio seguros para marcar as mensagens de remetentes nesses domínios como seguros. Para obter mais informações sobre a agregação, consulte [Agregação de Lista Segura](safelist-aggregation-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 10 minutos

  - Permissões do Exchange não se aplicam aos procedimentos neste tópico. Esses procedimentos são realizados no sistema operacional do Exchange Server.

  - As alterações que salvas no arquivo MSExchangeMailboxAssistants.exe.config são aplicadas depois que você reiniciar o serviço de assistentes de caixa de correio do Microsoft Exchange.

  - Quaisquer configurações personalizadas em cada servidor feitas nos arquivos de configuração de aplicativo XML do Exchange, por exemplo, os arquivos web.config em servidores de acesso para cliente ou o arquivo EdgeTransport.exe.config em servidores de Caixa de Correio, são substituídos quando você instala uma Atualização Cumulativa do Exchange (CU). Não deixe de salvar essas informações para poder reconfigurar facilmente o servidor após a instalação. Você deve redefinir essas configurações depois de instalar uma Atualização Cumulativa.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Use um prompt de comando para configurar a filtragem de conteúdo para usar os dados de domínio seguro

1.  Na janela de Prompt de comando, abra o arquivo de MSExchangeMailboxAssistants.exe.config no bloco de notas executando o seguinte comando:
    
    ```powershell
    Notepad %ExchangeInstallPath%Bin\MSExchangeMailboxAssistants.exe.config
    ```

2.  Localize a chave *\</appsettings\>* no final do arquivo e cole a seguinte chave antes da tecla *\</appsettings\>* :
    
    ```command line
    <add key="IncludeSafeDomains" value="true" />
    ```

3.  Quando tiver terminado, salve e feche o arquivo MSExchangeMailboxAssistants.exe.config.

4.  Reinicie o serviço de assistentes de caixa de correio do Microsoft Exchange executando o seguinte comando:
    
    ```powershell
        net stop MSExchangeMailboxAssistants && net start MSExchangeMailboxAssistants
    ```

## Como saber se funcionou?

Para verificar se você configurou com êxito a filtragem de conteúdo para usar os dados de domínio seguro, faça o seguinte:

1.  Verifique se que a adição de um domínio à lista de remetentes confiáveis do usuário no Outlook atualiza o atributo de **msExchSafeSenderHash** do usuário em Active Directory. Para fazer isso, exibir o atributo em ADSIEdit.exe ou LDP.exe, abra a caixa de correio do usuário no Outlook, adicione um domínio à lista de remetentes confiáveis, execute o comando `Update-Safelist <username>`e verifique se os valores originais e atuais dos **msExchSafeSenderHash** são diferentes.

2.  Depois de verificar que os dados de domínio seguro são armazenados em Active Directory, envie uma mensagem de teste de um remetente externo nesse domínio para um usuário em sua organização. Verifique se que a mensagem é marcada como seguro examinando os campos de cabeçalho de antispam no cabeçalho da mensagem.

