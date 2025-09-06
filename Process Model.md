**Ways to start a process**
1. Manual Start by exposing a **Related Action or Record Action** on a Record.
2. One process model can start another as a **sub-process node** (synchronous or asynchronous).
3. **a!startProcess()** → to launch from an expression (inside saveInto).
4. **a!startProcessLink()** -> to launch a chained UIT form inside a process.
5. **Start Process Smart Service** → inside another process.
6. A process can be started via a **Web API**.
7. Process models can be scheduled to start at a specific **time** or interval.
8. **Receive Message Event** from another process.
9. A process can be configured to start when a specific **email** is received.


**Start Process Smart Service**
 - The smart service can start other processes in  both synchronously and asynchronously.
 - You can use the Start Process smart service to start multiple processes at the same. The method for starting multiple processes differs depending on whether [autoscale is enabled](https://docs.appian.com/suite/help/25.3/autoscale-processes.html)
 - If the process model does not have autoscale enabled: Use the **Multiple Node Instances (MNI)** option on the Start Process smart service.
 - If the process model has autoscale enabled: Build a **looping flow** to start multiple asynchronous processes with the Start Process smart service.
 - If you chain through an asynchronous Start Process node or use `a!startProcess()` with `isSynchronous` set to `false`, the original process continues without interruption. No connection is maintained with the process that is started by the smart service, and any activity chaining is separate from the original process.
 - If you chain through a synchronous Start Process node or use `a!startProcess()` with `isSynchronous` set to `true`, the original process waits for other process to complete before continuing. Any activity chaining in the started process is not connected to the original process, so a [broken chain](https://docs.appian.com/suite/help/25.3/Process_Model_Recipes.html#breaking-a-chain) will not return process variables to the original process. If a chained flow encounters an attended activity, the activity will be assigned to the user that the Start Process smart service was run as, but it will not open the associated form.
 
**a!startProcess()**
 - The [Start Process smart service](https://docs.appian.com/suite/help/25.3/Start_Process_Smart_Service.html#) is available as an expression function that can be executed inside a saveInto on a [Interface Component](https://docs.appian.com/suite/help/25.3/executing_smart_services.html) or as part of a [Web API](https://docs.appian.com/suite/help/25.3/Web_APIs.html).
 - **isSynchronous** : When true, onSuccess is not evaluated until the child process is complete. If the process is not completed ==**within 30 seconds**==, onIncomplete is triggered. The child process will continue to run and can complete beyond the timeout.
 - **onSucess**:List of saves, fv!processInfo is only available when isSynchronous is true and will otherwise be null.
 - **onIncomplete**: A list of a!save() or an httpResponse() to execute when isSynchronous is true and any of the following occur: the process is canceled, the process cannot complete because of errors, the process does not finish within 30 seconds, or the initiator does not have permission to view the process.

**Sub Process**
 - It has both option as asynchronous and synchronous.
 - When an asynchronous subprocess is started, the parent process flow does not wait for the child process to complete. The flow continues without pausing.
 - When a synchronous subprocess is started, the parent process flow waits for the child process to complete before continuing the flow.

**Main Difference b/w Sub Process and Start Process**
1. Using sub process, adds readability to understand, which process has been invoked while debugging whereas in case of start process we need to search for target process using its UUID (if the process UUID gets change based on provided input).  
2. If we want to switch from one process to another along with its respective parameters, based on provided input, then it's preferable to go for start process instead of sub process  
3. If you want to invoke a process from an Interface or Web API in such case you have only one option i.e. startProcess .
4. ==And the most major difference, start process invokes the target process on a separate engine of Appian to Balance the load, hence we can't give guarantee, whenever we use start process, will immediately trigger the target process, whereas sub process gives you assurance of starting the child process immediately once after the flow hits this node.==

**Passing a Process Variable as Reference**
- Normally, when you pass a variable from a parent process to a subprocess → the **subprocess gets a copy**.
- Any changes inside the sub process do **not** affect the parent until the subprocess **ends**.
 If you select **"Pass as Reference"** →
- The subprocess works on the **same variable instance** as the parent.
- Changes made in either process are **immediately reflected** in both even if the child process is not completed.
- This also works across **multiple nested subprocesses**.


**Difference between exception & escalation?**
**Exceptions:** (present in **==UIT==**, Script Task, **==Integrations==**, **==Sub-Process==**)
- In Appian, an exception is a process event that diverts the normal flow, usually triggered by an exception flow path from an activity (task or node).  
- When an exception is triggered, the associated task is abandoned or cancelled, and the process follows the defined alternate (exception) path.  
- Exceptions can be:  
	- Timer-based (e.g., boundary timer events to exit a task after a timeout),  
	- Rule-based (e.g., conditional expressions), 
	- Message-based (e.g., receiving external input that interrupts the task).  
- The process continues on the exception path toward the next logical step — often a termination or alternate handling flow.  

**Escalations:**( Present Only in **==UIT==**, **==Integrations==**, **==Sub-Process==**)
- An escalation in Appian refers to an action taken on a task without cancelling it.  
- Escalations are typically time-based and are configured through the task assignment settings (e.g., in a User Input Task).  
- When a task is not completed within a defined time frame, escalation rules can: 
	- Send alerts or reminders to the current assignee,  
	- Reassign the task to another user or group,  
	- Change the task’s priority, or 
	- Notify supervisors for intervention. 
- The task remains active, and the escalation is intended to prompt timely action or reassignment not divert process flow.

**Use of Swim Lanes in the Process model?**
1. Swim lanes are used to override the assignment of nodes present in that lane. 
2. It help is visually dividing the flow, making your PM easier to understand by a consultant or even by an Analyst.

**Annotations in Appian**
 - Annotations in Appian are text notes that can be added inside process models to document and explain the workflow. They don’t impact execution but help improve readability, collaboration, and maintainability.

**How Timer Works in Appian**
 - A **timer event** in a process model (e.g., “Wait for X days/hours”) evaluates its **configuration at runtime** when the process instance is started.
 - In Appian, timers read their configuration at the time the process instance starts. If you update the constant used in a timer, running processes will continue with the old value, but new process instances started afterward will use the updated value.