---
title: 'Aplicativos para Outlook: Exchange 2013 Help'
TOCTitle: Aplicativos para Outlook
ms:assetid: 28b6f2a1-a235-4023-b561-6fd304962775
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ943753(v=EXCHG.150)
ms:contentKeyID: 52058804
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Aplicativos para Outlook

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2017-03-13_

**Resumo:**  uma visão geral dos suplementos do Outlook, que funcionam com o Outlook em computadores Windows e MacIntosh, em dispositivos móveis e no Outlook Web App e Outlook na web.

Suplementos para Outlook são aplicativos que estendem a utilidade dos clientes do Outlook, adicionando informações ou ferramentas que os usuários podem utilizar sem precisar sair do Outlook. Suplementos são criados pelos desenvolvedores de terceiros e podem ser instalados a partir de um arquivo ou uma URL ou do Office Store. Por padrão, todos os usuários podem instalar suplementos administradores do Exchange podem usar funções para controlar a capacidade dos usuários de instalar suplementos.


> [!TIP]
> Para obter informações sobre suplementos para Outlook de uma perspectiva do usuário final, confira o tópico de Ajuda <A href="https://go.microsoft.com/fwlink/p/?linkid=282387">suplementos Installed</A> no Office.com. Esse tópico fornece uma visão geral dos add-ins e também mostra algumas dos suplementos para Outlook que pode ser instalado por padrão.



## Os suplementos do Office Store e suplementos personalizados

Clientes do Outlook suporta uma variedade de suplementos disponíveis por meio da loja do Office. Outlook também oferece suporte a suplementos personalizados que você pode criar e distribuir aos usuários em sua organização.


> [!NOTE]
> Acesso ao armazenamento do Office não é compatível com caixas de correio ou organizações em regiões específicas. Se você não vir <STRONG>Adicionar da Office Store</STRONG> como uma opção no <STRONG>Centro de administração do Exchange</STRONG> em <STRONG>organização</STRONG> &gt; <STRONG>suplementos</STRONG> &gt; <IMG title="Ícone Adicionar" alt="Ícone Adicionar" src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif">, você poderá instalar um suplemento para Outlook a partir de um local de arquivo ou URL. Para obter mais informações, contate o provedor de serviço.




> [!NOTE]
> Alguns suplementos do Outlook são instalados por padrão. Suplementos de padrão para o Outlook somente ativar no conteúdo de idioma inglês. Por exemplo, endereços postais alemão no corpo da mensagem não ativar o suplemento do Bing Maps.



## Instalação e o suplemento do access

Por padrão, todos os usuários podem instalar e remover os administradores do Exchange de suplementos tiverem um número de controles disponíveis para gerenciamento de complementos e acesso de usuários a eles. Os administradores podem desabilitar os usuários instalem os suplementos que não são baixados da Office Store (em vez disso, eles são "lado carregado" de um arquivo ou URL). Os administradores também podem desabilitar usuários instalem os suplementos do Office Store e desde a instalação de suplementos em nome de outros usuários. Também é possível atribuir usuários a uma função que permite que eles instalar suplementos para sua organização ou por um subconjunto de usuários em sua organização.

Para impedir que os usuários instalem um suplemento que não seja da Office Store, remova a função de **Meus aplicativos de sinalizador**-los. Para desabilitar os usuários instalem suplementos da Office Store, remova a função de **Meus aplicativos do Marketplace**-los. Para obter mais detalhes, consulte [Especificar os administradores e usuários que podem instalar e gerenciar suplementos do Outlook](specify-the-administrators-and-users-who-can-install-and-manage-add-ins-for-outlook-exchange-2013-help.md).

Para instalar suplementos para alguns ou para todos os usuários em sua organização, consulte [Instalar ou remover aplicativos do Outlook para sua organização](install-or-remove-add-ins-for-outlook-for-your-organization-exchange-2013-help.md).

Se for necessário, você pode limitar a disponibilidade de um suplemento a usuários específicos na sua organização. Para obter mais informações, consulte [Gerenciar o acesso de usuário aos aplicativos para Outlook](manage-user-access-to-add-ins-for-outlook-exchange-online-help.md).

## Tarefas administrativas comuns com suplementos para Outlook

Existem alguns cenários comuns que os administradores do Exchange gerenciam em suas organizações.

**Se você quiser impedir que os usuários finais instalem suplementos do Outlook em todos os clientes do Outlook, faça as seguintes alterações às funções no Exchange admin center**:

  - Para impedir que os usuários instalem os suplementos do Office Store, remova a função **Marketplace meu**-los.

  - Para impedir que os usuários Carregando suplementos de fontes que não seja a Office Store, remova a função de **Meus aplicativos de sinalizador** -los.

  - Para impedir que os usuários instalem todos os suplementos, remova ambas as funções acima-los.

Consulte [Especificar os administradores e usuários que podem instalar e gerenciar suplementos do Outlook](specify-the-administrators-and-users-who-can-install-and-manage-add-ins-for-outlook-exchange-2013-help.md) para obter mais informações.

**Se seus usuários finais estão atualmente podem acessar os suplementos e você deseja remover esse acesso, use o cmdlet de `Get-App` para ver quais suplementos cada usuário tenha instalado.**

Em seguida, use o cmdlet `Remove-App` para remover os suplementos de um ou mais usuários.

Para obter mais informações, consulte [Get-App](https://technet.microsoft.com/pt-br/library/jj218673\(v=exchg.150\)) e [Remove-App](https://technet.microsoft.com/pt-br/library/jj218709\(v=exchg.150\)) para o Exchange 2013. Para o Exchange Online ou Exchange 2016, acesse [aqui](https://go.microsoft.com/fwlink/p/?linkid=844721).

## Permitir que administradores e usuários instalar suplementos

Você pode especificar quais administradores em sua organização têm permissão para instalar e gerenciar suplementos do Outlook. Você também pode especificar quais usuários em sua organização têm permissão para instalar e gerenciar suplementos para seu próprio uso. Para obter mais informações, consulte [Especificar os administradores e usuários que podem instalar e gerenciar suplementos do Outlook](specify-the-administrators-and-users-who-can-install-and-manage-add-ins-for-outlook-exchange-2013-help.md).

