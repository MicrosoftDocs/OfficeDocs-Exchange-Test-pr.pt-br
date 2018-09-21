---
title: 'Preparar o Active Directory e domínios: Exchange 2013 Help'
TOCTitle: Preparar o Active Directory e domínios
ms:assetid: f895e1ce-d766-4352-ac46-ec959c9954a9
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb125224(v=EXCHG.150)
ms:contentKeyID: 50487030
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Preparar o Active Directory e domínios

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Antes de instalar o Microsoft Exchange Server 2013, você precisa preparar sua floresta e domínios do Active Directory. O Exchange precisa preparar o Active Directory de modo que ele possa armazenar informações sobre as caixas de correio de seus usuários e a configuração dos servidores do Exchange na organização. Se você não estiver familiarizado com florestas ou domínios do Active Directory, confira [Visão geral do Active Directory Domain Services](https://go.microsoft.com/fwlink/p/?linkid=399226).


> [!NOTE]
> Se esta for a primeira instalação do Exchange em seu ambiente ou se você já tiver versões anteriores do Exchange Server em execução, prepare o Active Directory para o Exchange 2013. Confira <A href="exchange-2013-active-directory-schema-changes-exchange-2013-help.md">Alterações de esquema do Active Directory no Exchange 2013</A> para obter detalhes sobre novas classes de esquema e atributos que o Exchange 2013 adiciona ao Active Directory, incluindo aqueles feitas pelos Service Packs (SPs) e as Atualizações Cumulativas (CUs).



Há duas maneiras de preparar o Active Directory para o Exchange. A primeira é deixar o Assistente de instalação do Exchange 2013 fazer isso para você. Se você não tiver uma implantação de grande porte do Active Directory, e não tiver uma equipe separada que gerencie o Active Directory, recomendamos o uso do assistente. A conta usada por você deverá ser membro dos grupos de segurança Administradores de esquemas e Administradores de empresa. Para obter mais informações sobre como usar o Assistente de instalação, confira [Instalar o Exchange 2013 usando o Assistente para Configuração](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md).

Se você tiver uma implantação de grande porte do Active Directory, ou se uma equipe separada gerenciar o Active Directory, este tópico é para você. As etapas deste tópico proporcionam a você um controle muito maior sobre cada estágio de preparação, e sobre quem executa cada etapa. Por exemplo, talvez os administradores do Exchange não tenham as permissões necessárias para estender o esquema do Active Directory.

O que você precisa saber antes de começar?

1\. Estender o esquema do Active Directory

2\. Preparar o Active Directory

3\. Preparar os domínios do Active Directory

Como saber se funcionou?

Curioso para saber o que acontece quando o Active Directory está sendo preparado para o Exchange? Consulte [O que muda no Active Directory quando o Exchange 2013 é instalado?](what-changes-in-active-directory-when-exchange-2013-is-installed-exchange-2013-help.md)

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 10 a 15 minutos (não incluindo a replicação do Active Directory) ou mais, dependendo do tamanho da organização e do número de domínios filhos.

  - O computador que você usa para executar essas etapas precisa atender aos [Requisitos de sistema do Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md). Além disso, sua floresta do Active Directory precisa atender aos requisitos na seção "Servidores de rede e de diretório" em [Requisitos de sistema do Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

  - Se a sua organização tiver vários domínios do Active Directory, recomendamos o seguinte:
    
      - Executar as etapas abaixo de um site do Active Directory com um servidor Active Directory em qualquer domínio.
    
      - Instalar o primeiro servidor do Exchange em um site do Active Directory com um servidor de catálogo global gravável de todo domínio.


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## 1\. Estender o esquema do Active Directory

A primeira etapa para preparar a sua organização para o Exchange 2013 é estender o esquema do Active Directory. O Exchange armazena muitas informações no Active Directory, mas antes de poder fazer isso, ele precisa adicionar e atualizar as classes, atributos e outros itens. Se você estiver curioso sobre as mudanças em seu esquema após a extensão, confira [Alterações de esquema do Active Directory no Exchange 2013](exchange-2013-active-directory-schema-changes-exchange-2013-help.md).

Antes de estender o esquema, existem algumas coisas que você deve ter em mente:

  - A conta que você usou para se conectar deve ser membro dos grupos de segurança Administradores de esquemas e Administradores de empresa.

  - O computador no qual você executará o comando para estender o esquema precisa estar no mesmo domínio e site do Active Directory que o esquema mestre.

  - Se você usar o parâmetro *DomainController*, use o nome do controlador de domínio que é o esquema mestre.

  - A única maneira de estender o esquema para o Exchange é usar as etapas neste tópico ou usar a Instalação do Exchange 2013. Não há suporte para outras maneiras de estender o esquema.


> [!TIP]
> Se não houver uma equipe separada que gerencie seu esquema do Active Directory, ignore esta etapa e vá direto para Preparar o Active Directory. Se o esquema não for estendido na etapa 1, os comandos na etapa 2 estenderão o esquema para você. Se você decidir ignorar a etapa 1, as informações acima ainda precisão ser lembradas.



Quando você estiver pronto, faça o seguinte para estender seu esquema do Active Directory. Se você tiver várias florestas do Active Directory, conecte-se à floresta certa.

1.  Certifique-se de que o computador esteja pronto para executar a Instalação do Exchange 2013. Para ver o que é necessário para a execução da Instalação, confira a seção [Active Directory preparation](exchange-2013-prerequisites-exchange-2013-help.md) em [Pré-requisitos do Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

2.  Abra uma janela do Prompt de comando do Windows e vá até onde você baixou os arquivos de instalação do Exchange.

3.  Execute o seguinte comando para estender o esquema:
    
    ```powershell
Setup.exe /PrepareSchema /IAcceptExchangeServerLicenseTerms
```

Após a Instalação terminar de estender o esquema, será necessário aguardar enquanto o Active Directory replica as alterações a todos os controladores de domínio. Se você quiser verificar o andamento da replicação, use a ferramenta `repadmin`. A `Repadmin` está incluída como parte do recurso Ferramentas de Serviços de Domínio do Active Directory no Windows Server 2012 R2, Windows Server 2012 e no Windows Server 2008 R2. Para saber mais sobre como usar essa ferramenta, confira [Repadmin](https://go.microsoft.com/fwlink/p/?linkid=257879).

## 2\. Preparar o Active Directory

Agora que o esquema do Active Directory foi estendido, você pode preparar outras partes do Active Directory para Exchange 2013. Durante esta etapa, o Exchange criará contêineres, objetos e outros itens no Active Directory que usará para armazenar as informações. O conjunto de todos os contêineres, objetos, atributos etc. do Exchange é chamado de *Organização do Exchange*.

Antes de preparar o Active Directory para o Exchange, há algumas coisas que você deve se lembrar:

  - A conta que você usou para se conectar deve ser membro do grupo de segurança Administradores de empresa. Se você ignorou a etapa 1 porque queria que o comando *PrepareAD* estendesse o esquema, a conta usada também precisará ser membro do grupo de segurança Administradores de esquema.

  - O computador no qual você executará o comando precisa estar no mesmo domínio e site do Active Directory que o esquema mestre. Também precisará contatar todos os domínios na floresta na porta TCP 389.

  - Antes de executar esta etapa, aguarde até que o Active Directory tenha replicado as alterações feitas na etapa 1 a todos os seus controladores de domínio.

Quando você executa o comando abaixo para preparar o Active Directory para Exchange, é necessário nomear a organização do Exchange. Este nome é usado internamente pelo Exchange e não é normalmente visto pelos usuários. Normalmente, o nome da empresa na qual o Exchange está sendo instalado é usado como o nome da organização. O nome que você usa não afetará a funcionalidade do Exchange ou determinará o que você pode usar para endereços de email. Você pode dar o nome que quiser, contanto que se lembre do seguinte:

  - Você pode usar letras maiúsculas ou minúsculas de A a Z.

  - Você pode usar números de 0 a 9.

  - O nome pode conter espaços contanto que eles não estejam no início ou no final do nome.

  - Você pode usar um hífen ou um traço no nome.

  - O nome pode ter até 64 caracteres, mas não pode ficar em branco.

  - O nome não pode ser alterado depois que é definido.

Quando você estiver pronto, faça o seguinte para prepara o Active Directory para o Exchange. Se o nome da organização que você quiser usar tiver espaços, coloque-o entre aspas (").

1.  Abra uma janela do Prompt de comando do Windows e vá até onde você baixou os arquivos de instalação do Exchange.

2.  Execute o comando a seguir:
    
        Setup.exe /PrepareAD /OrganizationName:"<organization name>" /IAcceptExchangeServerLicenseTerms

Após a Instalação terminar de preparar o Active Directory para Exchange, será necessário aguardar enquanto o Active Directory replica as alterações a todos os seus controladores de domínio. Se você quiser verificar o andamento da replicação, use a ferramenta `repadmin`. A `repadmin` está incluída como parte do recurso Ferramentas de Serviços de Domínio do Active Directory no Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008 R2. Para saber mais sobre como usar a ferramenta, confira [Repadmin](https://go.microsoft.com/fwlink/p/?linkid=257879).

## 3\. Preparar os domínios do Active Directory

A etapa final para preparar o Active Directory para o Exchange é preparar cada um dos domínios do Active Directory no qual o Exchange será instalado ou no qual os usuários habilitados para email ficarão localizados. Esta etapa cria contêineres e grupos de segurança adicionais e define permissões de modo que o Exchange possa acessá-los.

Se você tiver vários domínios em sua floresta do Active Directory, terá duas opções para prepará-los. Selecione a opção que corresponde a o que você deseja fazer. Se você tiver apenas um domínio, ignore esta etapa, pois o comando *PrepareAD* na etapa 2 já preparou o domínio para você.

## Preparar todos os domínios em minha floresta do Active Directory

Para preparar todos os domínios do seu Active Directory, use o parâmetro *PrepareAllDomains* durante a execução da Instalação. A Instalação preparará cada domínio para o Exchange em sua floresta do Active Directory.

Antes de preparar todos os domínios em sua floresta do Active Directory, lembre-se do seguinte:

  - A conta que você usa deve ser membro do grupo de segurança Administradores de empresa.

  - Aguarde até que o Active Directory tenha replicado as alterações feitas na etapa 2 a todos os seus controladores de domínio. Se não fizer isso, você pode receber um erro durante a tentativa de preparação do domínio.

Quando você estiver pronto, faça o seguinte para preparar todos os domínios em sua floresta do Active Directory para Exchange.

1.  Abra uma janela do Prompt de comando do Windows e vá até onde você baixou os arquivos de instalação do Exchange.

2.  Execute o comando a seguir:
    
    ```powershell
Setup.exe /PrepareAllDomains /IAcceptExchangeServerLicenseTerms
```

## Deixe-me escolher quais domínios do Active Directory eu quero preparar

Se você quiser escolher os domínios do Active Directory que quiser preparar, use o parâmetro *PrepareDomain* ao executar a Instalação. Quando você usa o parâmetro *PrepareDomain*, é necessário incluir o nome de domínio totalmente qualificado (FQDN) do domínio que você quer preparar.

Antes de preparar os domínios em sua floresta do Active Directory, lembre-se do seguinte:

  - A conta que você usa precisa de permissões dependendo de quando o domínio foi criado.
    
      - **Domínio criado antes da execução do PrepareAD**   Se o domínio tiver sido criado **antes** da execução do comando *PrepareAD* na etapa 2 acima, a conta usada precisará ser membro do grupo Administradores de domínio no domínio que você deseja preparar.
    
      - **Domínio criado após da execução do PrepareAD**   Se o domínio tiver sido criado **após** a execução do comando *PrepareAD* na etapa 2 acima, a conta usada precisará 1) ser membro do grupo de função Gerenciamento de organização e 2) ser membro do grupo Administradores de domínio no domínio que você deseja preparar.

  - Aguarde até que o Active Directory tenha replicado as alterações feitas na etapa 2 a todos os seus controladores de domínio. Se não fizer isso, você pode receber um erro durante a tentativa de preparação do domínio.

  - É necessário preparar todo domínio no qual um servidor do Exchange será instalado. Também será necessário preparar qualquer domínio que tenha usuários habilitados para email, mesmo se esses domínios não tiverem servidores do Exchange.

  - Não é necessário executar o comando *PrepareDomain* no domínio no qual o comando *PrepareAD* foi executado. O comando *PrepareAD* prepara esse domínio automaticamente.

Quando você estiver pronto, faça o seguinte para preparar um domínio individual em sua floresta do Active Directory para Exchange.

1.  Abra uma janela do Prompt de comando do Windows e vá até onde você baixou os arquivos de instalação do Exchange.

2.  Execute o seguinte comando. Inclua o FQDN do domínio que você deseja preparar. Se você quiser preparar o domínio no qual você está executando o comando, não será necessário incluir o FQDN.
    
        Setup.exe /PrepareDomain:<FQDN of the domain you want to prepare> /IAcceptExchangeServerLicenseTerms

3.  Repita as etapas para cada domínio do Active Directory no qual você instalará um servidor do Exchange ou onde os usuários habilitados para email estarão localizados.

## Como saber se funcionou?

Após a execução de todas as etapas acima, verifique se tudo correu bem. Para fazer isso, você usará uma ferramenta chamada Service Interfaces Editor do Active Directory (Editor ADSI). O Editor ADSI está incluído como parte do recurso Ferramentas de Serviços de Domínio do Active Directory no Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008 R2. Se você quiser saber mais sobre isso, confira [Editor ADSI (adsiedit.msc)](https://go.microsoft.com/fwlink/p/?linkid=294644).


> [!WARNING]
> Nunca altere valores no Editor ADSI, a menos o Suporte da Microsoft o instrua a isso. A alteração dos valores no Editor ADSI pode causar danos irreparáveis à sua organização do Exchange e ao Active Directory.



Após o Exchange estender seu esquema do Active Directory e preparar o Active Directory para o Exchange, várias propriedades serão atualizadas para mostrar que a preparação foi concluída. Use as informações na lista a seguir para assegurar que essas propriedades tenham os valores certos. Cada propriedade precisa coincidir com o valor na tabela abaixo da versão do Exchange 2013 que você está instalando.

  - No contexto de nomeação **Esquema**, verifique se a propriedade **rangeUpper** em **ms-Exch-Schema-Verision-Pt** está configurado com o valor mostrado para a sua versão do Exchange 2013, na tabela do Versões do Active Directory do Exchange 2013.
    
     

  - No contexto de nomeação **Configuração**, verifique se a propriedade **objectVersion** no contêiner CN=\<*sua organização*\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<*domínio*\> está configurada com o valor mostrado para a sua versão do Exchange 2013 na tabela do Versões do Active Directory do Exchange 2013.
    
     

  - No contexto de nomeação **Padrão**, verifique se a propriedade **objectVersion** no contêiner **Objetos de Sistema do Microsoft Exchange** em DC=\<*domínio raiz* está configurada com o valor mostrado para a sua versão do Exchange 2013 na tabela do Versões do Active Directory do Exchange 2013.
    
     

Você pode também verificar o log de configuração do Exchange para verificar se a preparação do Active Directory foi concluída com êxito. Para mais informações, consulte [Verificar uma instalação do Exchange 2013](verify-an-exchange-2013-installation-exchange-2013-help.md). Você não conseguirá usar o cmdlet **Get-ExchangeServer** mencionado no tópico [Verificar uma instalação do Exchange 2013](verify-an-exchange-2013-installation-exchange-2013-help.md) até concluir a instalação de pelo menos uma função de servidor de Caixa de Correio e uma função de servidor de Acesso para Cliente em um site do Active Directory.

## Versões do Active Directory do Exchange 2013

A tabela a seguir mostra os objetos do Exchange 2013 no Active Directory que são atualizados sempre que você instala uma nova versão do Exchange 2013. É possível comparar as versões de objeto que você vê com os valores na tabela abaixo a fim de verificar se a versão do Exchange 2013 instalada atualizou o Active Directory durante a instalação.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th> </th>
<th>Versão do Exchange</th>
<th>rangeUpper</th>
<th>objectVersion</th>
<th>objectVersion</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Contexto de nomeação</strong></p></td>
<td><p> </p></td>
<td><p>Schema</p></td>
<td><p>Default</p></td>
<td><p>Configuration</p></td>
</tr>
<tr class="even">
<td><p><strong>Contêiner</strong></p></td>
<td><p> </p></td>
<td><p>ms-Exch-Schema-Version-Pt</p></td>
<td><p>Objetos do Sistema do Microsoft Exchange</p></td>
<td><p>CN=&lt;<em>your organization</em>&gt;, CN=Microsoft Exchange, CN=Services, CN=Configuration, DC=&lt;<em>domain</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Exchange 2013 CU10 e posterior</p></td>
<td><p>15312</p></td>
<td><p>13236</p></td>
<td><p>16130</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Exchange 2013 CU9</p></td>
<td><p>15312</p></td>
<td><p>13236</p></td>
<td><p>15965</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Exchange 2013 CU8</p></td>
<td><p>15312</p></td>
<td><p>13236</p></td>
<td><p>15965</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Exchange 2013 CU7</p></td>
<td><p>15312</p></td>
<td><p>13236</p></td>
<td><p>15965</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Exchange 2013 CU6</p></td>
<td><p>15303</p></td>
<td><p>13236</p></td>
<td><p>15965</p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Exchange 2013 CU5</p></td>
<td><p>15300</p></td>
<td><p>13236</p></td>
<td><p>15870</p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Exchange 2013 SP1</p></td>
<td><p>15292</p></td>
<td><p>13236</p></td>
<td><p>15844</p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Exchange 2013 CU3</p></td>
<td><p>15283</p></td>
<td><p>13236</p></td>
<td><p>15763</p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Exchange 2013 CU2</p></td>
<td><p>15281</p></td>
<td><p>13236</p></td>
<td><p>15688</p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Exchange 2013 CU1</p></td>
<td><p>15254</p></td>
<td><p>13236</p></td>
<td><p>15614</p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Exchange 2013 RTM</p></td>
<td><p>15137</p></td>
<td><p>13236</p></td>
<td><p>15449</p></td>
</tr>
</tbody>
</table>

