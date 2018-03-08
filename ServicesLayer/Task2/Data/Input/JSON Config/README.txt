****** IMPORTANT  ******
*
* Before running the application, please install the custom package from this folder. 
*
****** IMPORTANT  ******

* The present project demonstrates how we can use Json configuration files to store any kind of settings in clear text using the Json format. I included a custom activity that facilitates the reading of the Json configuration files and also allows the user to validate a configuration based on a predefined template. 

* The validation considers all the elements from the template and also their type and expects that the actual configuration files match the structure of the template completely. You can modify the files to test how that works. 

* The idea behind this came from the desire to pass just the right amount of information from one workflow to another, without having "global" blobs of information that we pass everywhere or to have too many arguments as input to a workflow. The Json format allows to send exactly the required Json Object to a subworkflow and we can structure the configuration hierarchy exactly as we structure the workflow hierarchy, allowing for a better organization and cleanness of the code.

* Note that Json objects can easily be serialized and stored as Assets in the Orchestrator if that way of managing them is preffered.