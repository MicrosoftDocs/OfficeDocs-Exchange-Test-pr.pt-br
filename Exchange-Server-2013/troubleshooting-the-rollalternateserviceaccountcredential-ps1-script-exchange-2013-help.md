---
title: 'O script RollAlternateServiceAccountCredential.ps1 de solução de problemas'
TOCTitle: O Script RollAlternateServiceAccountCredential.ps1 de solução de problemas
ms:assetid: 2bbf36d3-eb89-4f92-a8de-259a7cb64d62
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff808310(v=EXCHG.150)
ms:contentKeyID: 63914374
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# O Script RollAlternateServiceAccountCredential.ps1 de solução de problemas

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-01-14_

Este tópico fornece informações sobre erros comuns que podem ocorrer quando você usar o script RollAlternateServiceAccountPassword.ps1 e soluções.

## Um ou mais servidores de acesso do cliente não podem ser atualizadas com a senha

## Problema

Quando você usa os parâmetros *ToEntireForest* ou *ToArrayMembers* com o script, em alguns casos, um ou mais servidores de acesso do cliente não podem ser atualizado.

## Solução

Verifique se os servidores o script direcionar necessários todos os servidores usando o cmdlet **Get-ClientAccessArray** , conforme mostrado no exemplo a seguir.

    Get-ClientAccessArray | fl members

Se o servidor que está falhando para atualizar é um membro da matriz de acesso para cliente e não ainda está atualizando corretamente, execute novamente o Exchange instalação e adicione a função de servidor acesso para cliente ao servidor novamente. Você também pode especificar servidores individuais para o destino usando o parâmetro *ToSpecificServers*.

## Alguns servidores não estão respondendo ao script

## Problema

Em alguns casos, os servidores podem falhar ao atualizar devido a erros transitórios, como uma conexão de rede ruim.

## Solução

Verificar se os servidores em questão tem conectividade de rede e Active Directory e tente novamente o script.

## Alguns membros de matriz estão fora de serviço por um longo período de tempo

## Problema

Se um servidor estiver fora de rotação para um período de tempo maior, mas ainda é um membro da matriz, conforme determinado pelo **Get-ClientAccessArray cmdlet**, a funcionalidade de script pode ser prejudicada, ao usar os parâmetros *ToArrayMembers* e *ToEntireForest*. O mesmo problema ocorrerá se um servidor que teve uma falha permanente, mas não tenha sido interrompida completamente removido da sua implantação.

## Solução

Para resolver esse problema, remova o servidor de sua implantação usando Exchange instalação ou executar o script no modo assistido, até que o servidor pode ser removido.

Se o servidor só será para baixo por um curto período e você não deseja remover permanentemente Exchange, você pode ajustar o script a ser executado em servidores específicos usando o parâmetro *ToSpecificServers* para que apenas os servidores ativos direcionados. Ou então, você pode remover o serviço de acesso para cliente RPC do objeto de Active Directory sem resposta do servidor usando o cmdlet **Remove-ClientAccessArray** , conforme mostrado no exemplo a seguir.

    Remove-RPCClientAccess -Server Server.Contoso.com

Depois que o serviço de acesso para cliente RPC foi removido, o servidor não será retornado como um membro da matriz por [Get-ClientAccessArray](https://technet.microsoft.com/pt-br/library/dd297976\(v=exchg.150\)) e o script não têm como destino. Assim que o servidor está funcionando novamente, você pode adicionar novamente o serviço de acesso para cliente RPC usando o cmdlet **New-RpcClientAccess** . Quando o serviço de acesso para cliente RPC é adicionado novamente, certifique-se de reiniciar o serviço de catálogo de endereços do Microsoft Exchange no servidor afetado.


> [!CAUTION]
> Antes de remover o serviço de acesso para cliente RPC de um servidor, consulte o tópico <A href="https://technet.microsoft.com/pt-br/library/dd298151(v=exchg.150)">Remove-RPCClientAccess</A>.



## Para Obter Mais Informações

Para obter mais informações sobre como usar a autenticação Kerberos com uma matriz de servidores de acesso para cliente ou uma solução de balanceamento de carga, consulte os tópicos a seguir:

  - [Configurando a autenticação Kerberos para servidores de acesso para cliente com balanceamento de carga](configuring-kerberos-authentication-for-load-balanced-client-access-servers-exchange-2013-help.md)

  - [Usando o Script de RollAlternateserviceAccountCredential.ps1 no Shell](using-the-rollalternateserviceaccountcredential-ps1-script-in-the-shell-exchange-2013-help.md)

