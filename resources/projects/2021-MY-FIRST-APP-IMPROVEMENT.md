### 2021 - My first App Improvement

![](../pictures/AWS-Lambda-Pipeline.PNG)

There was automated Cloud Pipeline which has final element as **AWS Lambda** function written in Java.
I joined this project when most of the active development was done, but entire implementation was not yet ready for production.
AWS Lambda was a complex one which parses custom events, works with PostgreSQL and InfluxDB, calls other services by HTTP, 
connects to AWS services through AWS SDK, sends emails, processes data, and generates MS Word document.
Project **goal** was to fix bugs and add new features as was requested by end users.
I got Key Developer role and started working on **AWS Lambda** improvement.

During development, testing and delivering, I faced several **challenges**:

- There were calculations and results didn't meet expectations.
  Starting fixing bugs, I reviewed functions and used debugger to check code line by line.   
  Still, it was not clear where was mistake as complex constructions were used. 
  So, I decided to do refactoring.
  I divided big functions into smaller ones, used plain java code instead of Stream API where it was overcomplicated and so on.
  While refactoring, issues were appearing one by one, and finally, I managed to fix all the bugs quickly.<br>
  As a **result**, code related to calculations became easy to maintain and there were no further bugs.

- While working on new features, I faced issues with application architecture.
  There was a lot of code duplication, and it was hard to integrate new components.
  The structure of the app was built based on a data model, but not on a logical algorithm steps.
  Literally, for each peace of data were performed several processing steps, something like this:
  ```
  /**
   * High level method - doesn't have an explicit passing of 1-5 steps
   */ 
  public void handleRequest(InputStream inputStream, OutputStream outputStream, Context context) {
        // Step 1
        AppEvent event = eventService.parseEvent(inputStream);
        // Steps 2, 3, 4 are hidden in low level method
        DocxFile document = documentService.generateDocument(event);
        // Step 5
        outputService.sendDocument(document);
  }
  /**
   * Low level method - responsible for more then one functionality and "knows" about high level elements
   */ 
  public void populateParagraph(Event event, DocxFile document) {
        // Step 2
        ParagraphData data = modelService.collectParagraphData(event);
        // Step 3
        ParagraphCalculetedData paragraphCalculetedData = calculationService.calculateParagraphData(data);
        // Step 4
        documentService.populateDocument(paragraphCalculetedData, document);
  }
  ```
  My solution was to have simple algorithm function at high level, something like this:
  ```
  /**
   * High level method - have an explicit passing of 1-5 steps
   */ 
  public void handleRequest(InputStream inputStream, OutputStream outputStream, Context context) {
        // Step 1
        AppEvent event = eventService.parseEvent(inputStream);
        // Step 2
        AppData data = modelService.collectData(event);
        // Step 3
        AppCalculetedData appCalculetedData = calculationService.calculateAppData(data);
        // Step 4
        DocxFile document = documentService.generateDocument(summary);
        // Step 5
        outputService.sendDocument(document);
  }
  ```
  and have separate implementations at low level, something like this:
  ```
  /**
   * Low level method - responsible only for one functionality and works only with low level objects
   */ 
  public ParagraphData collectParagraphData(EventPart eventPart) {
        // Step 2 implementation
        // ...
  }
  /**
   * Low level method - responsible only for one functionality and works only with low level objects
   */ 
  public ParagraphCalculetedData calculateParagraphData(ParagraphData paragraphData) {
        // Step 3 implementation
        // ...
  }
  /**
   * Low level method - responsible only for one functionality and works only with low level objects
   */ 
  public DocxParagraph generateParagraph(ParagraphCalculetedData paragraphCalculetedData) {
        // Step 4 implementation
        // ...
  }
  ```
  Also, there were unappropriated using of Design Patterns. 
  For example, *Chain of Responsibility* was used where it was possible to simply have the switch-case construction.
  I discussed these points with stakeholder representative, we agreed on refactoring,
  and then I successfully implemented the changes, working really hard and sometimes overtime, because I felt personal responsibility for this decision.
  As a result, code quality was significantly increased, it became easy to add new features and test application.

- There was an issue with performance. 
  AWS Lambda running time was supposed to be from 5 to 15 minutes.
