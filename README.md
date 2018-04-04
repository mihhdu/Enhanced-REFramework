### Enhanced ReFrameWork Template ###
**Enhanced Robotic Enterprise Framework**

A UiPath Studio template upon which you can build, test and run attended and unattended business processes.

Features:
* Low code signature: A handful of clearly written, commented reusable functions written in VB.NET that anyone can understand and a Main.xlsx bringing structure to the process design architecture
* Separation Of Concerns: We keep framework implementation separate from business logic code, allowing developers and SMEs alike to focus on developing business logic code.
* Reusability: Works for any type of process, Independent of Data sources (QueueItems, local excel files, Database data, API retrieved data), Independent of process linearity
* Maintain, Upgrade, Extend: easy to Maintain, thanks to code lightness and SOC; Upgrade or extend framework independently of business code, by editing only one file; Extend to achieve process behavior by editing 5 empty workflows that connect to the Main with a standard interface.
* Exception Recovery and Retry: If all recovery options are exhausted, closing and restarting the application environment while remembering your data is what humans do too. Top-level exception recovery is managed by the framework layer.
* Audit: Keep track of the robot's work, with as much detail and privacy as you choose with the new Workblock concept; Add business information of your choosing to the published log.

Details:

* composed of configurable functional components called Workblocks.
* using *State Machine* layout with Workblocks in each state.
* offering high level exception handling and application recovery.
* offer a mechanism to abort process execution in certain cases where continuing is distructive
* keeps external settings in *Data\Config.xlsx* file and Orchestrator assets.
* pulls credentials from *Credential Manager* and Orchestrator assets.
* takes screenshots in case of application exceptions.
* provides extra utility workflows.
* implements services (off by default - see *Data\Config.xlsx*) to solve specific tasks independently.

### How It Works ###
*This version of the framework is not yet final (use caution) but has been heavily tested and should be safe to use*

[ReFrameWork Documentation - the workblock concept](https://github.com/mihhdu/UiPath_REFramework/blob/master/Documentation/Work%20Block%20UML.pdf)

[ReFrameWork Workblocks, multi layered view UML](https://github.com/mihhdu/UiPath_REFramework/blob/master/Documentation/REFramework%20Work%20Blocks.pdf)

[ReFrameWork Architecture, Flat view UML](https://github.com/mihhdu/UiPath_REFramework/blob/master/Documentation/REFramework%20architecture%20UML.pdf)

[ReFrameWork Manual - not updated](https://github.com/mihhdu/UiPath_ReFrameWork/blob/master/Documentation/REFramework%20documentation.pdf)

### For New Project ###
To begin implementing take the following steps:

1. Check out the *Data\Config.xlsx* file and add/customize any required fields and values. Also change the names of workblocks and enable system tasks if you need them.

2. Decide what the process is going to achieve. Think about what kind of data is moving around in the process. Think about wheather or not it is a cyclical process or executes just once.

3. Go in Main.xaml and change the following data types to suit your project needs:
TransactionItem - by default a QueueItem represents one transaction worth of data
TransactionData - by default a Datatable represents the collection of transaction data to be used in this process run
Ignore errors being generated for the moment.

4. Open *ProcessLayer\GetSetTransactionData.xaml* and change io_TransactionItem and io_TransactionData datatypes to match the ones you set up in the Main.xaml file.

5. Open *ProcessLayer\ProcessTransaction.xaml* and change io_TransactionItem's datatype to match the one you set up in the Main.xaml file.

6. Open Main.xaml and update the interfaces to the functions in the **GET/SET TRANSACTION DATA** and **PROCESS TRANSACTION** states by clicking the import button. The errors from point 1. should now dissapear.

7. Begin writing business code in the workflows located in the *ProcessLayer* folder

*ProcessLayer\InitAllApplications.xaml* - write business code to open all applications needed during processing.

*ProcessLayer\CloseAllApplications.xaml* - write business code to close all applications you have opened at previous step.

*ProcessLayer\KillAllProcesses.xaml* - write business code to kill all applications (only invoked when applications not responding).

*ProcessLayer\GetTransactionData.xaml* - write business code to fetch data for the current transaction and save/write it to the io_TransactionItem variable. Decide when the process will end by setting io_TransactinItem to Nothing. Make use of external iterator in_TransactionNumber and in_RetryNumber if io_TransactionItem is an element of io_TransactionData. (Ex. io_TransactionItem = io_TransactionData(in_TransactionNumber - 1).

*ProcessLayer\ProcessTransaction.xaml* - write business code to use applications that are open and data from io_TransactionItem and complete the transaction. At the end of the transaction, take the applications to the page they were at when you began the transaction.

8. Execute and have fun!
