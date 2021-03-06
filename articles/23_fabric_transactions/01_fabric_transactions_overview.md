# Fabric Transaction Management

Fabric has a built-in Transaction management mechanism that handles a transaction during data processing. Transactions are handled differently in different data processing modules.

### Sync Process

During the synchronization of an [LU Instance (LUI)](/articles/01_fabric_overview/02_fabric_glossary.md#lui), the data is retrieved from the source systems and loaded into the Fabric database. The [LU tables population](/articles/07_table_population/01_table_population_overview.md) and [enrichment functions](/articles/10_enrichment_function/01_enrichment_function_overview.md) are both executed in a [Sync process](/articles/01_fabric_overview/02_fabric_glossary.md#sync). 

The Sync process is managed as a single transaction that starts at the beginning of the Sync process and finishes at its end. If the Sync is completed successfully, the data is committed to the Fabric database. However, if an error occurs at any point during the Sync process, the transaction is rolled back.

When a Sync process is invoked by a [Web Service](/articles/15_web_services_and_graphit/01_web_services_overview.md) or a [User Job](/articles/20_jobs_and_batch_services/01_fabric_jobs_overview.md), the transaction can be managed by the calling process. For example, you can start a transaction in a Web Service, get an LUI, perform additional updates on the Fabric database and then commit. In this scenario, all the changes including those of the Sync will be committed.

[Click for more information about Sync LUI](/articles/14_sync_LU_instance/01_sync_LUI_overview.md).

### Broadway Flows

[Broadway](/articles/19_Broadway/01_broadway_overview.md) flows can be split into two categories: [an LU table population based on a Broadway flow](/articles/07_table_population/14_table_population_based_Broadway.md) and [a regular Broadway flow](/articles/19_Broadway/02a_broadway_flow_overview.md) executed not as part of a population. The transaction is managed differently in each of these categories:

* Broadway population flows are executed during the Sync process and therefore the management of a transaction in a flow is done as part of the overall Sync process transaction. There is no separate transaction for a Broadway flow in this case.
* When a Broadway flow is executed not as part of a population, Broadway must manage this transaction. 

Note that when a Broadway flow is invoked by a Web Service or a User Job, the transaction can also be managed by the calling process, as explained [above](/articles/23_fabric_transactions/01_fabric_transactions_overview.md#sync-process) in reference to the Sync process.

[Click for more information about Transactions in Broadway flows](/articles/19_Broadway/23_transactions.md).

### Fabric Transactions

Fabric enables updating a specific [LU table](/articles/06_LU_tables/01_LU_tables_overview.md) for the given LUI ([Instance ID](/articles/01_fabric_overview/02_fabric_glossary.md#instance-id)) in the Fabric database or an entry in the [Reference table](/articles/22_reference(commonDB)_tables/01_fabric_commonDB_overview.md) instead of synchronizing the entire Instance ID or the Reference table from the source. This functionality is used when:

* Fabric is the master of the specific data.
* Fabric needs to be updated if the feeds from the source didn't arrive or the data is not in-sync for some reason.

[Click for more information about Fabric Transactions](02_fabric_transactions.md).



[<img align="right" width="60" height="54" src="/articles/images/Next.png">](02_fabric_transactions.md)



