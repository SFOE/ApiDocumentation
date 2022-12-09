# Ilicop API with FME
This example shows you how to use the ilicop API with FME.

## General information
* FME Desktop 2020.1.3.0 was used.
* [Download Workbench file](https://github.com/nrohrbach/ApiDocumentation/raw/master/IlicopAPI_FME.zip)

## 1. Upload Interlis file for validation
Use the *POST Upload* endpoint to submit a xtf-file for validation.
Use a *HTTPCaller* transformer with the following options:

<img src="https://github.com/nrohrbach/ApiDocumentation/blob/master/images/1_upload.JPG" width="50%"/>

HTTP Client Options are as followed:
* Save Cookies: No
* Follow Redirects: No - do not follow redirects
* Verify SSL certificates: No
* Connection Timeout Length (seconds): 60
* Transfer Timeout Length (seconds): 90

File Upload - MIME Type: application/octet-stream

## 2. Get *JobId*
Use a *JSONExtractor* Transformer to get the jobid as followed:

<img src="https://github.com/nrohrbach/ApiDocumentation/blob/master/images/2_jobid.JPG" width="50%"/>

## 3. Check Status
The validation starts as soon as the Interlis file was uploaded. Use the *GET Status* endpoint to check status of the validation. Bigger files take some time to validate. Use a custom *Loop* transformer to check status as long as it is still beeing processed.

<img src="https://github.com/nrohrbach/ApiDocumentation/blob/master/images/3_checkstatus.JPG" width="50%"/>

Use a *Decelerator* transformer to get a request every 5 seconds:
* Processing Slowdown Method: Per Feature Delay
* Delay Per Feature (Seconds): 5

Use a *HTTPCaller* transfomer to request job status:
* Request URL: https://ilicop.ch/api/v1/status/@Value(jobid)
* HTTP Method: GET

Use a *JSONExtractor* transformer to receive status as followed:
'''json["status"]'''

Eventually use a *Tester* transformer to loop as long as status is 'processing'.

## 4. Download Logfiles
Now use a *tester* transformer to check if data is valid. If status is 'completed' proceed with valid data e.g. publication. If status is 'completedWithErrors' download log files to detect errors and stop process with a *Terminator* transformer:


<img src="https://github.com/nrohrbach/ApiDocumentation/blob/master/images/4_logfiles.JPG" width="50%"/>

Use a *HTTPCaller* transfomer to download log files:
* Log file: https://ilicop.ch/api/v1/download?jobId=@Value(jobid)&logType=log
* Xtf Log file: https://ilicop.ch/api/v1/download?jobId=@Value(jobid)&logType=xtf
