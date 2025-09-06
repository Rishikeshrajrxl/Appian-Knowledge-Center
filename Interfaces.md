**Document upload min security**
 - If you're using a [record type to manage the documents](https://docs.appian.com/suite/help/25.3/manage-docs-with-records.html), users must have at least ==**Viewer**== permission to the record type.
- If you're using a [folder to manage the documents](https://docs.appian.com/suite/help/25.3/folder-and-document-management.html), users must have at least ==**Editor**== permission to the target folder or document.

**a!fileUploadField()**
 - Allows users to upload one or more files. To upload files outside of a [start form](https://docs.appian.com/suite/help/25.3/process-model-object.html#process-start-form-tab) or [task](https://docs.appian.com/suite/help/25.3/Tasks.html), use [a!submitUploadedFiles()](https://docs.appian.com/suite/help/25.3/fnc_system_a_submituploadedfiles.html) in the _saveInto_ parameter of a submit [button](https://docs.appian.com/suite/help/25.3/Button_Component.html) or [link](https://docs.appian.com/suite/help/25.3/Link_Component.html). Uploaded documents are not accessible until after form submission.
 - We can scan the uploaded files for virus configured in admin console.
 - In portals, the size limit for uploaded files is 10 MB. Everywhere else, the file size limit is 1GB.

**User Input Task (UIT)**
 - If **Save Into is NOT defined** in the UIT input fields → then Appian will use the **Output variable mapping** defined in the process model.  
 - If **Save Into IS defined** in the UIT input fields → then the value entered by the user will be saved through the input itself, and output mapping won’t override it.

**Embedded Interfaces**
 - Embedded interfaces are one of the user experience options available in Appian, alongside Tempo, [sites](https://docs.appian.com/suite/help/25.3/Sites.html), and [portals](https://docs.appian.com/suite/help/25.3/portal-object.html). Embedded interfaces allow Appian interfaces to be embedded in external web pages. This lets users interact with Appian forms and interfaces directly within those external pages, without navigating to a distinct Appian environment like a site. In fact, users may not even realize they are interacting with an Appian-powered interface, especially if a custom [theme](https://docs.appian.com/suite/help/25.3/Themes_for_Embedded_Interfaces.html) is applied.