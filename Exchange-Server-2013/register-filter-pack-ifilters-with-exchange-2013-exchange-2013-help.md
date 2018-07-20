---
title: 'Registrar IFilters do Filter Pack com o Exchange 2013: Exchange 2013 Help'
TOCTitle: Registrar IFilters do Filter Pack com o Exchange 2013
ms:assetid: 0338980f-3a64-49d3-bc3c-bf6f10f88cb4
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ837174(v=EXCHG.150)
ms:contentKeyID: 50556135
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Registrar IFilters do Filter Pack com o Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Regras de transporte com condições de verificação de anexo executam extração de texto ao analisar o conteúdo de anexos. O Exchange 2013 pode verificar tipos de anexo mais comumente usados de maneira nativa. Tipos adicionais de anexo podem ser incluídos registrando IFilters no Exchange 2013. Este tópico mostra como registrar IFilters liberados pela Microsoft e por provedores de terceiros.

Após registrar um IFilter para um tipo de arquivo específico, as regras de transporte com condições de processamento de anexo poderão verificar esses anexos. Como resultado, esses tipos de arquivo não dispararão a condição *AttachmentIsUnsupported*.


> [!WARNING]
> Os procedimentos listados neste tópico envolvem a modificação do Registro nos servidores do Exchange. A edição incorreta do Registro pode causar problemas graves que podem exigir a reinstalação do sistema operacional. Talvez não seja possível resolver os problemas resultantes da edição incorreta do Registro. Antes de editar o Registro, faça backup de todos os dados importantes.<BR>Esses procedimentos também exigem que você interrompa e reinicie o serviço de Transporte do Microsoft Exchange em seus servidores de Caixa de Correio.



Para outras tarefas de gerenciamento adicionais relacionadas a regras de Transporte, consulte [Gerenciar regras de fluxo de emails](manage-mail-flow-rules-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos por servidor.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Definições de configuração do servidor do Exchange" no tópico [Permissões de infraestrutura do Exchange e do Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Você deve realizar o procedimento a seguir nos servidores que já possuem a função de servidor de Caixa de Correio do Exchange 2013 instalada. Se você adicionar servidores de Caixa de Correio adicionais depois de realizar esses procedimentos, será necessário realizá-los novamente nos servidores recém-provisionados.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Registrar o Microsoft Office 2010 Filter Pack

Por padrão, os seguintes tipos de arquivo do Office não são aceitos pelas regras de transporte do Exchange:

  - Office OneNote

  - Office Publisher

Se deseja oferecer suporte para esses arquivos, você deve implantar o Microsoft Office 2010 Filter Pack. Esse Filter Pack não é implantado durante a instalação do Exchange 2013 e não é um pré-requisito para a implantação.

## Implantar o Microsoft Office 2010 Filter Pack

Implantar o Office 2010 Filter Pack consiste em duas etapas principais:

  - Baixar e instalar o Filter Pack, que registra os IFilters com o Windows (Pesquisa).

  - Modificar o registro para que os IFilters também sejam registrados com Exchange 2013. Isso permite que o Exchange ofereça suporte à verificação de anexos para os formatos de arquivo.


> [!IMPORTANT]
> É necessário executar esse procedimento em todos os servidores de Caixa de Correio em sua organização.



1.  Baixar e salvar o Microsoft Office 2010 Filter Pack (`FilterPack64bit.exe`) a partir do [Centro de Download da Microsoft](https://go.microsoft.com/fwlink/?linkid=191548).

2.  Execute o arquivo do `FilterPack64bit.exe` em seu servidor de Caixa de Correio e siga as instruções para concluir a instalação.

3.  Inicie o Editor do Registro e localize a seguinte subchave do Registro:
    
        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\HubTransportRole\CLSID

4.  Em **CLSID**, adicione uma subchave para arquivos do OneNote da seguinte maneira:
    
    1.  Clique com o botão direito do mouse em **CLSID**, aponte para **Novo** e clique em **Chave**.
    
    2.  Altere o nome da nova chave para `{B8D12492-CE0F-40AD-83EA-099A03D493F1}`.
    
    3.  Clique na chave que acabou de criar e defina o valor **(Padrão)** para onde você instalou o Office 2010 Filter Pack. Por padrão, o filter pack é instalado em `C:\Program Files\Common Files\Microsoft Shared\Filters\ONIFilter.dll`.
    
    4.  Clique com o botão direito em **{B8D12492-CE0F-40AD-83EA-099A03D493F1}**, aponte para **Novo** e depois clique em **Valor da Cadeia de Caracteres**.
    
    5.  Nomeie o novo valor de cadeia de caracteres `ThreadingModel` e defina-o como `Both`.

5.  Em **CLSID**, adicione uma subchave para arquivos do Publisher da seguinte maneira:
    
    1.  Clique com o botão direito do mouse em **CLSID**, aponte para **Novo** e clique em **Chave**.
    
    2.  Altere o nome da nova chave para `{A7FD8AC9-7ABF-46FC-B70B-6A5E5EC9859A}`.
    
    3.  Clique na chave que acabou de criar e defina o valor **(Padrão)** para onde você instalou o Office 2010 Filter Pack. Por padrão, o filter pack é instalado em `C:\Program Files\Common Files\Microsoft Shared\Filters\PUBFILT.dll`.
    
    4.  Clique com o botão direito em **{A7FD8AC9-7ABF-46FC-B70B-6A5E5EC9859A}**, aponte para **Novo** e depois clique em **Valor da Cadeia de Caracteres**.
    
    5.  Nomeie o novo valor de cadeia de caracteres `ThreadingModel` e defina-o como `Both`.

6.  Localize a seguinte chave do Registro:
    
        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\HubTransportRole\filters

7.  Em **filtros**, adicione uma subchave para extensões .one da seguinte maneira.
    
    1.  Clique com o botão direito do mouse em **filtros**, aponte para **Novo** e clique em **Chave**.
    
    2.  Altere o nome da nova chave para `.one`.
    
    3.  Clique na chave que acabou de criar e defina o valor de **(Padrão)** como `{B8D12492-CE0F-40AD-83EA-099A03D493F1}`.

8.  Em **filtros**, adicione uma subchave para extensões .pub da seguinte maneira:
    
    1.  Clique com o botão direito do mouse em **filtros**, aponte para **Novo** e clique em **Chave**.
    
    2.  Altere o nome da nova chave para `.pub`.
    
    3.  Clique na chave que acabou de criar e defina o valor de **(Padrão)** como `{A7FD8AC9-7ABF-46FC-B70B-6A5E5EC9859A}`.

9.  Feche o editor de Registro.

10. No seu servidor de Caixa de Correio, interrompa e depois reinicie os seguintes serviços na ordem especificada:
    
    1.  Pare o serviço de Transporte do Microsoft Exchange.
    
    2.  Interrompa o Serviço de Gerenciamento de Filtragem da Microsoft.
    
    3.  Inicie o Serviço de Gerenciamento de Filtragem da Microsoft.
    
    4.  Inicie o Serviço de Transporte do Microsoft Exchange.

## Como saber se funcionou?

Para verificar se você registrou com êxito os IFilters do Microsoft Office 2010 Filter Pack, faça o seguinte:

1.  Crie uma regra de Transporte com as seguintes propriedades. Para obter instruções detalhadas sobre como criar regras de Transporte, consulte [Gerenciar regras de fluxo de emails](manage-mail-flow-rules-exchange-2013-help.md).
    
      - O remetente é sua caixa de correio.
    
      - Qualquer conteúdo de anexo inclui "Testando IFilters".
    
      - Gere um relatório de incidente e envie-o para sua caixa de correio.

2.  Crie um arquivo do OneNote que contenha a frase "Testando IFilters", anexe-o a uma nova mensagem de email e envie-a para si mesmo.

3.  Verifique se recebeu um relatório de incidente de regra de Transporte para a regra que você criou. Isso confirma que o mecanismo de regras pode analisar o conteúdo de arquivo do OneNote.

4.  Repita as etapas 2 e 3 com um arquivo do Publisher.

## Registre IFilters de terceiros para dar suporte a formatos de arquivo adicionais

Você pode estender o recurso de verificação de anexos para tipos de arquivos adicionais registrando IFilters de terceiros adicionais. O suporte a arquivos adicionais pode ser adicionado instalando e registrando o IFilter do tipo de arquivo em cada servidor de Caixa de Correio.


> [!IMPORTANT]
> A Microsoft não testou nenhum IFilter de terceiros com as regras de transporte, portanto, recomendamos que você implante e teste todos os IFilters de terceiros em um ambiente de teste antes de implantá-los no seu ambiente de produção.



## Implantar o IFilter do Adobe PDF

Este procedimento mostra como implantar o [IFilter do Adobe PDF](https://www.adobe.com/support/downloads/detail.jsp?ftpid=4025) para oferecer suporte a processamento de anexos PDF nas regras de transporte.


> [!TIP]
> Por padrão, o Exchange 2013 dá suporte à verificação de arquivos PDF nas regras de transporte. O exemplo de PDF aqui é usado simplesmente para ilustrar como você pode ampliar o suporte para tipos de arquivos adicionais usando IFilters de terceiros.



1.  Baixe o [IFilter do Adobe PDF](https://www.adobe.com/support/downloads/detail.jsp?ftpid=4025)e siga as instruções de instalação.

2.  Inicie o Editor do Registro e localize a seguinte subchave:
    
        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\HubTransportRole\CLSID

3.  Em **CLSID**, adicione uma subchave para arquivos PDF, da seguinte maneira:
    
    1.  Clique com o botão direito do mouse em **CLSID**, aponte para **Novo** e clique em **Chave**.
    
    2.  Altere o nome da nova chave para `{E8978DA6-047F-4E3D-9C78-CDBE46041603}`.
        

        > [!TIP]
        > Cada IFilter tem uma ID de única classe (CLSID). Você pode encontrar o CLSID na documentação de instalação para o IFilter que registrou para a extensão de arquivo na chave <CODE>HKEY_CLASSES_ROOT\CLSID</CODE> no registro.

    
    3.  Clique na chave que acabou de criar e defina o valor **(Padrão)** para onde você instalou o IFilter de PDF. Por padrão, o IFilter de PDF é instalado em `C:\Program Files\Adobe\Adobe PDF IFilter 9 for 64-bit platforms\bin\PDFFilter.dll`.

4.  Localize a seguinte chave do Registro:
    
        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\HubTransportRole\filters

5.  Em **filtros**, adicione uma subchave para extensões .pdf, da seguinte maneira:
    
    1.  Clique com o botão direito do mouse em **filtros**, aponte para **Novo** e clique em **Chave**.
    
    2.  Altere o nome da nova chave para `.pdf`.
    
    3.  Clique na chave que acabou de criar e defina o valor de **(Padrão)** como `{E8978DA6-047F-4E3D-9C78-CDBE46041603}`.

6.  Feche o editor de Registro.

7.  No seu servidor de Caixa de Correio, interrompa e reinicie os seguintes serviços na ordem especificada:
    
    1.  Pare o serviço de Transporte do Microsoft Exchange.
    
    2.  Interrompa o Serviço de Gerenciamento de Filtragem da Microsoft.
    
    3.  Inicie o Serviço de Gerenciamento de Filtragem da Microsoft.
    
    4.  Inicie o Serviço de Transporte do Microsoft Exchange.

## Como saber se funcionou?

Use o mesmo procedimento listado na seção How do you know this worked? anterior nesse tópico, substituindo arquivos do Publisher por arquivos do Adobe PDF.

## Para obter mais informações

[Usar regras de transporte para inspecionar anexos de mensagens](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md)

[Regras de fluxo de emails ou de transporte](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[Condições de regra de transporte (predicados)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[Ações de regra de transporte](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)

