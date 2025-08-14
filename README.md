# Investor Uploading Identification Documents - Test Plan & Investigation

## Part 1: Test Plan

### Objectives
- The main objective of testing the feature is to verify and validate that a user as an investor can upload the supported identification documents types like passport and ID card, The verification process works as per design synchronous or asynchronously, ensure correct business rules are being applied to each upload, Ensure correct error handling in case of failures, test edge cases which can be easily overlooked.
- Ensure compliance with financial regulations like GDPR, KYC etc.
- Validate secure handling of sensitive data during upload, transmition, storage.
  
### Scope

#### Included:
- Happy path flow of uploading an ID document as an investor.
- Negative flow of uploading an ID document as an investor and error handling.
- UI and API integration.
- Synchronous or asynchronous request and jobs handling.
- OCR technology data extraction and matching with investor information (if used in the verification process).
- Compliance testing with regulatory standards of data privacy, processing and other regulations.
- Complete in house built software feature
- Security testing, API authentication and authorization flows.
- Regression tesing to ensure other parts do not get affected by the changes.
- Database validation.
- Multiple browsers and devices compatitbility.
- Non functional testing of the feature (accessibility, performance etc).
- Relevant features testing which require the verified ID document of investor as a prerequisite
- Risk of fradulent ID documents.

#### Excluded:
- Other non relevant features testing. e.g (payment, widrawals)
- Third party API integrations or dependencies.
- Non functional testing of the entire platform as a whole.

---

### Test Types
- Manual test everything to add by default human factor for usability and user experience testing.
- Automated E2E tests to cover main flow of feature.
- API testing to test backend stability and functionality.
- Backend database validation.

---

### Test Techniques to be used
- Functional testing: Positive & negative test scenarios plus business rules of actual functionality
- Integration testing: Api integration with UI, correct synchronization handling.
- Security testing: Data encryption, penetration testing for file upload.
- Compliance testing: GDPR and KYC compliance standards as per requirements of busienss.
- Performance testing: Response time of APIs and uploading documents one after the other for verification.
- Accessibility testing: 
- Boundary value analysis.
- Error guessing.
- State transition testing
- Monkey testing.
---
###  Test Environment & Tools
- Test Environment: Staging environment mirroring production.

- Data: Synthetic test data compliant with GDPR.

- Postman (API testing) 

- Selenium / Cypress (UI automation)

- JMeter & Google lighthouse (performace testing)

- OWASP ZAP (security testing)
  
- aXe Tool (Accessibility testing)
  
---

###  Entry Criteria
- Requirements, user stories, Test plan finalized and approved.

- Test environment ready with integrated verification API.

- Test data prepared.
  
---

###  Exit Criteria
- All planned test cases executed.

- No open high/critical severity defects.

- Compliance checks passed.

---

### Test Scenarios

#### Sub task 1 and sub task 2 included:
It includes Positive test cases, Negative test cases and edge cases:

| Testcase Name | Precondition | Description | Test Scenario | Test Type | Expected results |
|--------------|--------------|-------------|---------------|-----------|------------------|
| Valid file format | a) File size is less then 5 mb. b) Valid documen witht future expiry date. c) Select only one file while uploading | Upload file in pdf or JPG format. | Positive | Automated UI and API | UI should show the uploaded document. API should return 202 accepted. |
| Valid File size | a) Valid File format JPG or PDF. b) Valid document with future expiry date. c) Select only one file while uploading | Upload file with file size less then 5 mb e.g 4.99 mb | Positve | Automated UI and API | UI should show the uploaded document. API should return 202 accepted. |
| Valid Until date of document | a) Valid File format JPG or PDF. b) Valid file size less then 5 mb. c) Select only one file while uploading | Upload file with valid date in future. | Positve | Manual test | UI should show the uploaded document. API should return 202 accepted (Postman). |
| Replace existing uploaded file | a) Valid File format JPG or PDF. b) Valid file size less then 5 mb. c) Valid document with future expiry date. | Upload a new file to replace the existing file. | Positve | Automated UI and API | UI should show the new uploaded document in file preview and the old file should not be visible. |
| Upload the same file again | a) Valid File format JPG or PDF. b) Valid file size less then 5 mb. c) Valid document with future expiry date. | Upload same  file to replace the existing file. | Positve | Automated UI and API | UI should show the only one uploaded document in file preview. |
| Upload file with file name including special characters | a) Valid File format JPG or PDF. b) Valid file size less then 5 mb. c) Valid document with future expiry date. d) Select only one file while uploading. e) File name containing special characters | Upload file with file name including special characters i.e ()"$#* e.t.c. | Positve | Automated UI and API | UI should show the uploaded file. |
| InValid File size | a) Valid File format JPG or PDF. b) Valid document with future expiry date. c) Select only one file while uploading | Upload file with file size greater  then 5 mb e.g 5.01 mb | Negative | Automated UI and API | UI should provide error message for file size. API should return bad request 404. |
| InValid file format | a) File size is less then 5 mb. b) Valid document with future expiry date. c) Select only one file while uploading | Upload file other than pdf and JPG format e.g. docs, Png, xlsx, pptx, JPEG, SVG, Gif, Webp | Negative | Automated UI and API | UI should provide error message for unsupported file format. API should return bad request 404. |
| InValid Until date of document | a) Valid File format JPG or PDF. b) Valid file size less then 5 mb. c) Select only one file while uploading | Upload file with Invalid date in past. | Negative | Manual UI test | Valid uploaded file is rejected after review or processing. |
| Upload two files | a) Valid Files format JPG or PDF. b) Valid documents with future expiry date. c) Select two files while uploading d) Valid file sizes less then 5 mb. | Try to select and upload two files at the same time | Negative | Manual test | The upload functionality should not allow selecting two files to upload. |
| Upload same file two times | a) Valid Files format JPG or PDF. b) Valid documents with future expiry date. c) Select two files while uploading d) Valid file sizes less then 5 mb. | Try to select and upload the same file consectively | Negative | Manual test | The upload functionality should not replace the existing file and should show fedback that this document is already in review. |
| Upload file with file name containing 300 characters | a) Valid File format JPG or PDF. b) Valid file size less then 5 mb. c) Valid document with future expiry date. d) Select only one file while uploading. e) File name containing  300 characters | Upload file with file name containing 300 characters. | Positive Edge case | Automated UI | UI should show the uploaded file. (depends on requirements) |
| Upload file with size 5 mb | a) Valid File format JPG or PDF. b) File size equal to 5 mb. c) Valid document with future expiry date. d) Select only one file while uploading. e) File name containing  300 characters | Upload file with size exactly equal to 5 mb | Negative Edge case | Automated UI and API | UI should provide error message for file size. API should return bad request 404. |
| Valid Until date of document of today | a) Valid File format JPG or PDF. b) File size equal to 5 mb. c) Valid document with expiry date of today. d) Select only one file while uploading. | Upload file with valid unti date of todays date. | Negative Edge case | Manual UI/API test | Valid uploaded file is rejected after review or processing. |
| Refresh  or Close the page while uploading valid file | a) Valid File format JPG or PDF. b) Valid document with future expiry date. c) Select only one file while uploading d) Valid file size less then 5 mb. | While the valid file is getting uploaded , refresh or close the current page. | Negative Edge case | Manual UI test | UI should show the Pop up message asking for confimration to refresh or exit as the changes will not be saved in this scenario. |
| Upload multiple files sequentially | a) Valid Files format JPG or PDF. b) Valid documents with future expiry date. c) Select two files while uploading d) Valid file sizes less then 5 mb. | Try to select and upload the mutiple files sequentially one after the other | Negative edge case | Manual test | The system should block the user to upload multiple documents sequentially within quick span. |
| Click upload document button multiple times in one go | a) Valid Files format JPG or PDF. b) Valid documents with future expiry date. c) Select two files while uploading d) Valid file sizes less then 5 mb. | Try to click upload document button at UI multiple times | Negative edge case | Manual test | The system should only show one upload document pop up to select and only one request at a time. |
| Test valid upload functionality as non-investor | a) Valid Files format JPG or PDF. b) Valid documents with future expiry date. c) Select two files while uploading d) Valid file sizes less then 5 mb. | Test valid upload functionality as a non investor | Negative edge case | Manual test | The upload functionality should not be available for other users except investor role users |
| Test valid upload functionality with slow internet | a) Valid Files format JPG or PDF. b) Valid documents with future expiry date. c) Select two files while uploading d) Valid file sizes less then 5 mb. | Test valid upload functionality with slow internet e.g 3G | Negative edge case | Manual test | The upload functionality should sync with the slow internet and processing should be asynchronous |
| Test valid upload functionality with no internet | a) Valid Files format JPG or PDF. b) Valid documents with future expiry date. c) Select two files while uploading d) Valid file sizes less then 5 mb. | Test valid upload functionality with no internet e.g no wifi | Negative edge case | Manual test | The upload functionality should handle the error of upload correctly |


# Three easy-to-overlook but important edge cases are:

### File name containing 300 characters

Reason it’s important: Many systems fail on extremely long file names due to OS or database field limits, even if the file content itself is valid. This is an edge case that can break the upload flow silently if not handled. Plus XSS attacks possible with the filename.
It Needs explicit handling.

### Refresh or close the page while uploading

Reason it’s important: This tests resilience against user interruption and ensures that partial uploads or canceled requests don’t corrupt data or leave the system in an inconsistent state.

### Click upload document button multiple times in one go

Why important: Tests concurrency control to prevent duplicate uploads, multiple requests, or race conditions in UI/API.

These all target non-happy-path scenarios that aren’t obvious, but can cause serious bugs in production.


---


### Special Considerations
**Sub task 3 Background processing for uploads**  
I will explain how I will test if the system uses background processing for uploads. Infact, Most of the test cases I have derived already have the asumption that they can be done only when the upload processing is asnchronous.

1. I will verify that the UI shows correct feedback during the upload process and during validation.
2. The states during the backend processing are synched with the Frontend UI updates and do not contradict each other. For example, uploading state, processing state, error in upload state, error in verifications state, Invalid document upload state, rejected or accepted state, verified state and more depending on specifications.
3. Test that the uploaded file is available on frontend with its status only after successful upload and during verification by backend job.
4. Ensure in case of file not following the criterion described in above test cases, UI provides correct reletive feedback.
5. Correct error handling of file upload functionality at all layers and the errors are linked with each other.
6. I wil try to test with the slow internet and see whats the behavour of the e2e functionality as a system.
7. Focus on integration testing and API testing.
8. When replacing an existing document, It only updates the document at the UI when backend gets updated after all validations. (integration of API and DB layer with UI, DB testing if it ensures only the latest uploaded document entry remains and replaces the already placed entry).
9. Ensure the edge case when the existing document is still in state processing and user uploads second document for verification. How system behaves, does it replace the existing document and creates new job and kills the old job of processing.
10. What if I upload the same file two times, does it get detected or does it replace the existing document being processed and restarts the whole verification process.
11. Some of the test cases will be sifted from manual or automated UI testing type to API focused testing and backend testing.

---

## Part 2: Investigate and Debug a Realistic Bug Report

**Bug report:**  
“A user uploaded a valid ID document, and the upload was accepted, but a few minutes later it disappeared from their dashboard.”

### 1. Investigation Plan
a) First step to investigate the reported bug is to reporduce it on local or test instance or try to get exact steps to reproduce the bug.  
b) If the bug is reproduced we can investigate further and if it is not reproducable then we should halt the investigation and mark it as un reproducable, contact product owner to clarify requirement and set a call with dev team to discuss and investigate further together.  
c) If the bug is reproduced, Then I will investigate the first instance of the bug logged into the system. This will help check what sort of feature updates were done at that exact point in time and in further analysis of the code.  
d) After that, I will try to investigate the Network tab in browser dev tools. Verify the API calls in network tab, what is the reponse code from the api call.  If API response code is not according to specifications, I will assign the bug ticket with all documentation to dev team.  
e) If the API shows success response in the network tab, I will try to investigate the issue further using the backend server or Job management platform for the jobs of upload file if it is successful or in th queue still. If the job is not running at the backend server, I will assign the bug ticket with all documentation to dev team.  
f) If the Job is successfully running in the backend server, then I will investigate the database for the new entries into the db. If it does not show the new entry into the databse then I will assign the bug ticket with all documentation to dev team.  
g) If, database shows the new entry then I will contact Dev team to investigate using mob testing and pair programming for further diagnosis.  

### 2. Hypotheses for Root Cause
a) Incorrect or missing syncing of the backend job runs and UI.  
b) Exception handling not done properly.  

### 3. Prevention
a) Add error logging, sync UI with backend properly i.e unexpected deletion at the backend or refresh.  
b) Ensure 100% coverage of the backend functionality using integration testing (manual plus automated).  

---

## Part 3: Communicate with the Team

**Scenario:**  
You notice that a recent feature behaves differently from the product specification. The investor sees a success message even when the upload fails due to a background error (e.g., storage issue).

**Message to Product Owner/Engineer:**

Hi team,  
I have found a bug in the recent feature that deviates slightly from product specifications or actual expected behavior. While using the system as an Invester to upload a valid file, The user is able to upload file on the frontend web application and sees success message of upload even when the upload functionaliyt fails in actual. May be due to backend job, database issue, or the API layer error the file does not get saved into the backend. This shows that the UI and backend is not synched for proper success and error handling. The impact of this is that user will have the confirmation that the file is uploaded but in reality it is not in the system. This would cause user to not do the verification again. This is a major issue as it will affect the functionality which will be only available for investors whose ID is verified in the system. 

**Improvement Suggestion:**  
a) I would suggest to add snyching flow of UI and API in the E2E testing suite or if budget constraints are present then focus on Integration testing plus proper testing of negative test cases or error handling.
