### ReFrameWork V2 Template ###
**Robotic Enterprise Framework**

The role of the framework is to be an engine that will run business logic in a safe and reproducibile manner. This engine should serves the following purpose:

* deliver a platform upon which to build business logic 
* run and report on execution of said business logic. 
* manage transaction exception recovery independently of the business logic.
* offer a mechanism to abord process execution in certain cases where continuing is destructive.
* achieve layer separation (business only edits business code).

Features:

* composed of configurable functional components called workblocks. 
* using *State Machine* layout with workblocks in each state.
* offering high level exception handling and application recovery.
* keeps external settings in *Data\Config.xlsx* file and Orchestrator assets.
* pulls credentials from *Credential Manager* and Orchestrator assets.
* takes screenshots in case of application exceptions.
* provides extra utility workflows.
* implements services (off by default - see *Data\Config.xlsx*) to solve specific tasks idependently.

### How It Works ###
*This version of the framework is not yet final (use caution) but has been heavily tested and should be safe to use*

[ReFrameWork Documentation - the workblock concept](https://github.com/mihhdu/UiPath_REFramework/blob/master/Documentation/Work%20Block%20UML.pdf)

[ReFrameWork Workblocks, multi layered view UML](https://github.com/mihhdu/UiPath_REFramework/blob/master/Documentation/REFramework%20Work%20Blocks.pdf)

[ReFrameWork Architecture, Flat view UML](https://github.com/mihhdu/UiPath_REFramework/blob/master/Documentation/REFramework%20architecture%20UML.pdf)

[ReFrameWork Manual - not updated](https://github.com/mihhdu/UiPath_ReFrameWork/blob/master/Documentation/REFramework%20documentation.pdf)

### For New Project ###
To begin implementing take the following steps:

1. Check out the *Data\Config.xlsx* file and add/customize any required fields and values. Also change the names of workblocks and enable system tasks if you need them.

1. Decide what the process is going to achieve. Think about what kind of data is moving around in the process. Think about wheather or not it is a cyclical process or executes just once. 

2. Go in Main.xaml and change the following data types to suit your project needs:
TransactionItem - by default a QueueItem represents one transaction worth of data
TransactionData - by default a Datatable represents the collection of transaction data to be used in this process run
Ignore errors being generated for the moment. 

3. Open *ProcessLayer\GetSetTransactionData.xaml* and change io_TransactionItem and io_TransactionData datatypes to match the ones you set up in the Main.xaml file.

4. Open *ProcessLayer\ProcessTransaction.xaml* and change io_TransactionItem's datatype to match the one you set up in the Main.xaml file.

5. Open Main.xaml and update the inferfaces to the functions in the **GET/SET TRANSACTION DATA** and **PROCESS TRANSACTION** states by clicking the import button. The errors from point 1. should now dissapear.

6. Begin writing business code in the workflows located in the *ProcessLayer* folder
*ProcessLayer\InitAllApplications.xaml* - write business code to open all applications needed during processing.
*ProcessLayer\CloseAllApplications.xaml* - write business code to close all applications you have opened at previous step
*ProcessLayer\KillAllProcesses.xaml* - write business code to kill all applications (only invoked when applications not responding)
*ProcessLayer\GetTransactionData.xaml* - write business code to fetch data for the current transaction and save/write it to the io_TransactionItem variable. Decide when the process will end by setting io_TransactinItem to Nothing. Make use of external iterator in_TransactionNumber and in_RetryNumber if io_TransactionItem is an element of io_TransactionData. (Ex. io_TransactionItem = io_TransactionData(in_TransactionNumber - 1).
*ProcessLayer\ProcessTransaction.xaml* - write business code to use applications that are open and data from io_TransactionItem and complete the transaction. At the end of the transaction, take the applications to the page they were at when you began the transaction. 

7. Execute and have fun! 

