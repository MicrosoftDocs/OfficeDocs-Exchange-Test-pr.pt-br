---
title: 'Exchange 2013: edições e versões: Exchange 2013 Help'
TOCTitle: 'Exchange 2013: edições e versões'
ms:assetid: b563b543-fb3f-4465-9a54-cbfd680aee1f
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232170(v=EXCHG.150)
ms:contentKeyID: 50556282
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013: edições e versões

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2016-12-09_

O Microsoft Exchange Server 2013 está disponível em duas edições de servidor: Standard Edition e Enterprise Edition. O Enterprise Edition pode ser dimensionado para 50 bancos de dados montados por servidor nas versões Release to Manufacturing (RTM) e Atualização Cumulativa 1 (CU1), e 100 bancos de dados montados por servidor na versão Atualização Cumulativa 2 (CU2) e versões posteriores; a Standard Edition está limitada a 5 bancos de dados montados por servidor. Um banco de dados montado é um banco de dados que está em uso. Um banco de dados pode ser montado um banco de dados de caixa de correio ativa que é montado para uso pelos clientes, ou um banco de dados de caixa de correio passiva que é montado na recuperação para a replicação de log e replay. Embora seja possível criar mais bancos de dados do que os limites descritos acima, você só pode montar o número máximo especificado acima. O banco de dados de recuperação não conta neste limite.

Essas são edições de licenciamento definidas por uma chave de produto. Quando você insere uma chave de licença do produto válida, a edição com suporte para o servidor é estabelecida. As chaves de produto podem ser usadas somente para trocas e atualizações de chaves da mesma edição e não podem ser usadas para downgrades. Você pode utilizar uma chave de produto válida para migrar da versão de avaliação (Trial Edition) do Exchange 2013 para a Standard Edition ou a Enterprise Edition. Também é possível usar uma chave de produto válida para migrar da Standard Edition para a Enterprise Edition.

O servidor poderá ser licenciado novamente usando a mesma chave de produto da edição. Por exemplo, se você tinha dois servidores Standard Edition com duas chaves, mas utilizou acidentalmente a mesma chave nos dois servidores, é possível mudar a chave de um deles para a outra chave. Essas ações podem ser executadas sem que nenhuma reinstalação ou reconfiguração seja necessária. Depois de inserir a chave do produto e reiniciar o serviço de Armazenamento de Informações do Microsoft Exchange, a edição correspondente a essa chave será refletida.

Nenhuma perda de funcionalidade ocorrerá quando a Edição de Avaliação expirar, portanto, é possível manter os ambientes de laboratório, demonstração, treinamento e outros de não produção por mais de 120 dias, sem a necessidade de reinstalar essa edição do Exchange 2013.

Conforme mencionado anteriormente, não é possível usar chaves de produto para fazer downgrade da Enterprise Edition para a Standard Edition, nem usá-las para reverter para a Edição de Avaliação. Esses tipos de regressões só podem ser feitas desinstalando o Exchange 2013, reinstalando o Exchange 2013, e inserindo a chave correta do produto.

## Versões do Exchange 2013

Para obter uma lista de versões do Exchange 2013 e informações sobre como baixar e atualizar a última versão do Exchange 2013, veja estes tópicos:

  - [Atualizações do Exchange Server: números de versão e datas de lançamento](https://technet.microsoft.com/pt-br/library/hh135098\(v=exchg.150\))

  - [Atualizar o Exchange 2013 para a atualização cumulativa ou pacote de serviço mais recente](upgrade-exchange-2013-to-the-latest-cumulative-update-or-service-pack-exchange-2013-help.md)

Para ver o número de compilação da versão atual do Exchange 2013, execute o seguinte comando no Shell de Gerenciamento do Exchange.

    Get-ExchangeServer | fl name,edition,admindisplayversion

## Tipos de licença do Exchange 2013

O Exchange 2013 é licenciado no modelo CAL (Licença de Acesso para Cliente/Servidor) similar a como o Exchange 2010 foi licenciado. A seguir, os tipos de licenças:

  - **Licenças de servidor**   Uma licença deve ser atribuída a cada instância do software de servidor que está sendo executado. A licença do Servidor é vendida em duas edições de servidor: Standard Edition e Enterprise Edition.

  - **Licenças de Acesso para Cliente (CALs)**   O Exchange 2013 também vem em duas edições de licença de acesso para cliente (CAL), indicadas como Standard CAL e Enterprise CAL. Você pode misturar e combinar as edições de servidor com os tipos de CAL. Por exemplo, você pode usar Enterprise CALs com o Exchange 2013 Standard Edition. Da mesma forma, você pode usar as Standard CALs com o Exchange 2013 Enterprise Edition.

Confira mais informações sobre os tipos de licenças do Exchange em [Licenciamento](https://go.microsoft.com/fwlink/p/?linkid=392675).

