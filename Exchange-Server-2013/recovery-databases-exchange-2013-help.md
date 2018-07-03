---
title: 'Bancos de dados de recuperação: Exchange 2013 Help'
TOCTitle: Bancos de dados de recuperação
ms:assetid: f3c6fd0b-2e25-442e-a0fc-46f663130c3e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd876954(v=EXCHG.150)
ms:contentKeyID: 50486999
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Bancos de dados de recuperação

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-11-02_

Um banco de dados de recuperação (RDB) é um tipo especial de banco de dados de caixa de correio que permite que você monte um banco de dados de caixa de correio restaurado e extrair dados de banco de dados restaurado como parte de uma operação de recuperação. Você pode usar o cmdlet [New-MailboxRestoreRequest](https://technet.microsoft.com/pt-br/library/ff829875\(v=exchg.150\)) para extrair dados de um RDB. Após a extração, os dados podem ser exportados para uma pasta ou mesclados em uma caixa de correio existente. RDBs permitem que você recuperar dados de um backup ou a cópia de um banco de dados sem prejudicar o acesso de usuário aos dados atuais.

Microsoft Exchange Server 2013 oferece suporte à capacidade para restaurar os dados diretamente para um banco de dados de recuperação. Os dados recuperados como um banco de dados de recuperação de montagem permite ao administrador restaurar itens individuais em uma caixa de correio ou caixas de correio individuais. Restaurando um banco de dados de recuperação pode ser feito de duas maneiras:

  - Se já existir um banco de dados de recuperação, o aplicativo pode desmontar o banco de dados, restaure os dados para os arquivos de log e de banco de dados de recuperação e monte o banco de dados novamente.

  - Os arquivos de log e de banco de dados podem ser restaurados para qualquer local do disco. Exchange analisa os dados restaurados e repete os logs de transação para trazer os bancos de dados atualizados e, em seguida, um banco de dados de recuperação pode ser configurado para apontar para os arquivos de banco de dados já recuperada.

## Diferença entre um banco de dados de caixa de correio e um banco de dados de recuperação

RDBs são diferentes dos bancos de dados de caixa de correio padrão em vários aspectos:

  - Um RDB é criado utilizando o Exchange Management Shell.

  - Mensagens não sejam enviadas para ou de um RDB. Todos os clientes protocolo acessem um RDB (incluindo SMTP, POP3 e IMAP4) está bloqueado. Esse projeto impede que usando um RDB para inserir um email em ou remover emails do sistema de mensagens.

  - Acesso do cliente MAPI usando o Microsoft OfficeOutlook ou Outlook Web App é bloqueado. Acesso MAPI é suportado para uma RDB, mas apenas por aplicativos e ferramentas de recuperação. A GUID da caixa de correio e o GUID do banco de dados devem ser especificados ao usar o MAPI para efetuar logon em uma caixa de correio em um RDB.

  - Caixas de correio em um RDB não podem ser conectadas às contas de usuário. Para permitir que um usuário acesse os dados em uma caixa de correio em um RDB, a caixa de correio deve ser mesclada em uma caixa de correio existente ou exportada para uma pasta.

  - Políticas de gerenciamento de sistema e de caixa de correio não serão aplicadas. Esse projeto impede que os itens em uma RDB seja excluído pelo sistema durante o processo de recuperação.

  - Manutenção online não é executada para RDBs.

  - O log circular não pode ser habilitado para RDBs.

  - Apenas um RDB pode ser montado a qualquer momento em um servidor de caixa de correio. O uso de um RDB não conta com relação ao limite de banco de dados por servidor de caixa de correio.

  - É possível criar cópias de banco de dados de um RDB para caixa de correio.

  - Um RDB pode ser usado como um destino para operações de restauração, mas as operações de backup não.

  - Um banco de dados recuperado montado como um RDB não está vinculada à caixa de correio original de nenhuma maneira.

## Usando um banco de dados de recuperação

Antes de poder usar um RDB, há certos requisitos que devem ser atendidos. Um RDB pode ser usada para Exchange 2013 caixa de correio somente bancos de dados. Bancos de dados de caixa de correio de versões anteriores do Exchange não são suportados. Além disso, a caixa de correio de destino usada para mesclagens de dados e extração deve ser na mesma floresta Active Directory como o banco de dados montado o RDB.

Um RDB pode ser usado para recuperar dados em várias situações, tais como:

  - **Recuperação de sinal do mesmo servidor**   Você pode executar uma recuperação de uma RDB depois que o banco de dados original foi restaurado do backup, como parte de uma operação de recuperação de tom de discagem.

  - **Recuperação de sinal de servidor alternativo**   Você pode usar um servidor alternativo para hospedar o banco de dados de tom de discagem e, em seguida, posteriormente recuperar dados de um RDB depois que o banco de dados original foi restaurado do backup.

  - **Recuperação de caixa de correio**   Você pode recuperar uma caixa de correio individual de backup quando o período de retenção de caixa de correio excluída tiver decorrido. Você, em seguida, extrair dados de caixa de correio restaurado e copiá-lo para uma pasta de destino ou mesclar com outra caixa de correio.

  - **Recuperação de item específico**   Você pode restaurar os dados de backup que tenha sido excluída ou removidos de uma caixa de correio.


> [!TIP]
> Listas de controle de acesso (ACLs) pasta não são preservadas ao recuperar o conteúdo em uma caixa de correio ativa. Como o processo de recuperação geralmente envolve a recuperação de dados de caixa de correio e mesclando o conteúdo de volta no banco de dados original, não deve haver nenhuma necessidade de recuperar ou copie as ACLs.



Um RDB destina-se a recuperação de banco de dados de caixa de correio sob as condições e os cenários a seguir:

  - As informações lógicas sobre o banco de dados original e as caixas de correio no banco de dados permanecem intacta e inalterados no Active Directory.

  - Você precisa recuperar uma única caixa de correio ou um único banco de dados. Cenários de recuperação incluem:
    
      - Recuperando ou reparo de um banco de dados enquanto um tom de discagem de banco de dados está em uso, com o objetivo de mesclar os dois bancos de dados.
    
      - Recuperando um banco de dados em um servidor diferente do servidor original ao banco de dados. Se necessário, você pode mesclar os dados recuperados de volta ao servidor original.
    
      - Recuperando itens excluídos que os usuários excluídos previamente suas caixas de correio, depois que o período de retenção de item excluído expirou.

Geralmente, a RDBs não foram projetados para cenários nos quais você tem que restaurar todo servidores, quando você tem que restaurar vários bancos de dados, ou quando você estiver em uma situação de emergência que exige a alteração ou reconstruir sua topologia Active Directory.

Para obter instruções detalhadas sobre como criar um RDB, consulte [Criar um banco de dados de recuperação](create-a-recovery-database-exchange-2013-help.md). Para obter instruções detalhadas sobre como usar um RDB, consulte [Restaurar dados usando um banco de dados de recuperação](restore-data-using-a-recovery-database-exchange-2013-help.md).

