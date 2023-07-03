Intro:
Slide 1: 

Hey everyone,
This is team 2 Hyderabad team of ptct summer interns.
Giving a brief before we begin:
Our project has 2 key components, the first one is a program which validates a version of sample JSON data against a schema setup by SEDA team. This program will alert when data doesn't follows desired format, and sends back a business object for valid sample data.

Second component is about creation of a utility where at real time, XML upo gets converted to json and vice versa on the fly with the help of mapping sheet.


Slide2
XML translator

Real problem occurring (why we need this)
Different banks and org uses different message formats, majorly XML and JSON, and their conversion is difficult, hectic and time consuming.


Slide 3:
Problem statement formation:
Hence we come up with task of building of a utility which when provided with a mapping sheet, and a input message 
(Please show inputs here)
Convert the given message to other desired format on fly with minimum time.

Slide4:
Solution:
First, we validate the input provided by the user. If the validation is unsuccessful, an error file is returned. If the validation is successful, the translation process takes place. Initially, we read the mapping sheet using the apache.poi library and store it in a hash map. Then, we convert the input file to a JsonObject using the Jackson and Gson libraries. Using this JsonObject and the hashmap, we create another JsonObject that aligns with the mapping sheet. Finally, we convert it to the required file type.
(To increase, we can add api calls here.)

Slide5:
Diagram explaination:
Takes atleast 1 minute. Please modify.
Tx service called by txserviceimpl, error service finds errors in input, builds xmlerrorfile.....zzz
.
.
 
.
 
.
.

Slide 6:
Domonstration:

The entire demonstration
It takes 1 minute
Here is the ui,
It is build using react, responsive, user friendly. 

Coming to XML to json facility, here we upload input XML document and mapping sheet in correct format first,
And the results are here.
It gives option to download after processing, opening the downloaded file, 
Let's verify it and done.
Trying it with wrong inputs, let us put in wrong file, and processing on downloding we get a .text file with errors in it.

Similarly , json to XML, can be done
Here we upload the files, correct ones and the output can be now downloaded,
Then finally, we can verify, here also, similarly we can download error file.


Slide 7:
Learning:

While working on this problem statement, we encountered numerous new terminologies and libraries. We came to know about the ISO20022 standard for exchange of financial messages between Financial Institutions. We also familiarized ourselves with various message formats such as PACS.008, PACS.007, and so on. Additionally, all of us gained experience with the Spring Boot framework for the first time. We learned about libraries like Apache.poi for reading Excel files, as well as Jackson and Gson for processing JsonObjects. Furthermore, we gained an understanding of how the organization's artifactor y operates and how to import dependencies from it.
 
Future scope:
Yml and other files
CSV files change format 


Slide8:
Xsd real problem faced by wells Fargo

The SEDA team regularly updates the Global Schema UPO, which is used by Java-based applications, to incorporate new requirements.
When a new version of XSD Schema goes live, it may cause issues for applications that are still using the previous version. 

Slide 9:
Problem statemen formation
We need an utility which must update our system with the new schema version as well as validate whether our schema is compatible with the current version. That is where the XSD Governance application comes in.


Slide 10:
Solution

There are 2 components to it: Update and Validate
For updating the UPO, the new version of schema is uploaded which is then........

Whereas for validating our sample against the current version of schema, the schema uploaded is........


Slide 11:
Class diagram
Explaination
(.
.
.
.
.
.
.
.
.
.
.
.
)


Slide 12: 
Domonstration:

The entire demonstration
It takes 1 minute
Here is the ui,
It is build using react, responsive, user friendly. 

Coming to upload version facility, handled by SEDA team, here they upload input json schema (latest version) and it processed and makes updated pojo here.

Now the version validator
We keep the correct input here the json sample data,
Now it verifies internally and if validated, we can check the created buisness objects after the text converts to validated, otherwise we can download the error file.





Slide 13:
Learning 
Learning XSD :
While solving this problem statement, we realized the importance of effective communication of schema updates within an organization to ensure seamless operation of development teams. We gained a better understanding of the structure and functionality of JSON schemas and discovered the jsonschema2pojo library, which facilitates the generation of POJOs (Plain Old Java Objects). It's important to note that not all libraries may meet our requirements, in which case we may need to extend the functionality to a widely used library.

In conclusion, we also recognized the need for backward compatibility in applications to ensure that they continue to function with older schemas, preventing any disruptions in the process.



Future scope
Future Scope:
1. To have a backward compatibility feature
2. Conversion from one version to another without needing to upgrade/ downgrade
3. EPL Pipeline Integration 
Usage of artifactory for other project .









Last slide:
Thankyou note
Thank you for listening, we are now open for questions.