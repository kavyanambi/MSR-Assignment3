# MSR-Assignment3
Note : This is a MSR study as part of the MSR course 2022 at UniKo, CS department, SoftLang Team

**Team name: echo**

**Student names:**


Kavya Sasikumar

Poornima Muddajji Kariyanna

**Underlying paper : https://ieeexplore.ieee.org/document/9796219**


**Reproduced baseline:**


**Description:**


Reproducting the framework(inspect4Py) for feature extraction which can be used to train machine learning models.Any GitHub repo can be run against Inspect4py will extract all the metadata and features in a JSON file.The evaluation includes a lot of annotation of each repositories info to csv manually.so we reproduced the feature extraction of the python repository with different cases


**Input Data** : GitHub repositories containing python files.


**Output Data** : The OutputDir directory will have the same subdirectory structure as the input directory given by the user. In order to ease the inspection of all the features extracted for a given directory (and its subdirectories) we have aggregated all generated json information in a single JSON file stored at OutputDir/DirectoryInfo.json.In other words, OutputDir/DirectoryInfo.json, represents all the features extracted of all files found in a given directory (and its subdirectories).


**Findings of reproduction**:


**Process delta**:
inspect4py extracts relevant code features, detects class and function metadata and identifies the main entry points for using it


**Output delta**:
*The are few repositories with package which have customised scripts instead of setup.py,Those are not captured.



*Some scripts are misclassified as tests therefore lot of scripts are missing when compared to given input file



*If repo has different extension other than .py ,it does’t identify ex:html,java them as different file



**Implementation of reproduction**

• Hardware requirements: 64bit CPU, 4 or more than works with both Mac or Linux OS

• Software requirements : Windows 10 or 11 with python version 3.7 or higher
Jyupter Notebook
Git repository access to get all the input python files



• Validation: The evaluation metric is not exactly calculated as mentioned in the paper since lot of manually annotation is the procedure followed in the paper. The reproducibility mainly hints as a preprocessing step which can be used for feature extraction before training machine learning models. It can also be used to automatically fill up Readme file which gives a summary of the project.

• Data : Input: Repository of python files, same as the paper suggested.

Output: Extracted features produced as a JSON file


**MSR study enhancements**


**Threat**: If repository has different extension other than.py ,it does’t identify ex:html,java them as different file. Also if the repository dosen't have a .py files the model crashes with no proper information.


**Traces** : “If there is significant overlap, we mark the software repository as a package. If not, or if there are no entry points, we consider the code repository to be a library. Next, we analyze the rest of the files of the repository individually” [266]-[270]


**Theory**: Currently, inspect4py framework only handles.py extension files and python repositories. In a case where the python repositories contain an extra file such as html, it will misclassify them and consider it as a library. This misclassification makes the annotation of json file harder and hinder the evaluation process.


**Methodology**: We would like to propose the methodology to build a function which checks the file extension inside a python repository and to skip if the extension of files is not .py rather than labelling it as scripts or library package. Labelling wrongly seems to affect the annotation and hence the evaluation results.

**Feasibility**:  When the repository did not have any .py files, error messages used to be found which gives no information about the issue which made annotation of json files( which already includes a lot of manual task )and further evaluation and ranking of the model difficult. This has been handled by the enhancement where proper message will be displayed and files which has extension other than .py will be skipped before creating the output directory which has improved the performance.
The files other than .py will be excluded which makes the annotation of json file easier as it already includes lot of manual task. 


**Process**: The process followed can be explained as follows.


1)If .py files are present, output directory is created. Other extension files such as .js and html,.txt will are identified and will skipped automatically with the enhancements


2) When the sample repository path is passed through the enhanced function in ‘cli.py’ checks for the file with .py extension, if not present the project used to throw an error which has been handled to provide a message as “no .py file was found in the repository ”.



**Data**: The code was run against 3 cases:

i) When parsed against github repo having no ‘.py’ file and contains only files with other extensions, Proper message will be displayed which tells you to run against a repo with ‘.py’ extension and no output directory file is created.


ii) When parsed against a repo containing .py file and .js file , it will successfully create an output dir with just .py file, with .js file being successfully skipped.


iii) When parsed against with repositories having just .py file,Output directory(of json format) correctly identifying the methods, classes and libraries of the file was created


**Results**:  From the enhancement it can be concluded that the tool(inspect4py) will provide an area for more improvement in files with extensions other than .py and also ensures that proper skipping of files in the preprocessing stage is happening which will inturn improve the overall F1 score for the application.



**Implementation** 


• Hardware requirements: 64bit CPU,  or more that works with both Mac or Linux OS


• Software requirements :


Unix and Mac Os with python version 3.7 or higher

 Jyupter Notebook 
 
Git repository access to get all the input python files

• Validation: The enhancement gives more clear idea about the flow of process. Information about files skipped can be identified. The screenshot of the difference has been added to the doc folder.

• Data :

Input data: Repository of python files and non-python files(for enhancement)
 
 
Output data: Output directory of json format which contains classes,methods and libraries of just .py files. While consisting of non .py files, proper message explaining the issue will be displayed.

