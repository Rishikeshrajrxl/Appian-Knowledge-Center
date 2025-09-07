**What are Integration touchpoints in your current application.**
- Integration touchpoints in my application are the places where Appian interacts with external systems. For example, in my current project we integrate with a SQL database via data stores, Salesforce and DocuSign REST APIs, Outlook for email processing, and SharePoint for document storage. These are the key integration touchpoints where our application exchanges data with other systems.

**Id and UUID difference** 
 - In Appian, **IDs** are numeric and environment-specific, mainly used for runtime objects like documents, records, and process instances. **UUIDs** are globally unique alphanumeric identifiers used for design-time objects like rules, interfaces, and process models, ensuring consistency across environments.
**UUID (Universally Unique Identifier)**
 - A **128-bit alphanumeric identifier** (e.g., `550e8400-e29b-41d4-a716-446655440000`).
- ==Globally unique across environments.==
- Does not change between environments → reliable for object migration and integration.
- Used for **Appian design objects** (rules, interfaces, constants, process models, etc.).

**Reasoning behind why Appian moved from MySQL to MariaDB in recent versions**
 - Appian moved to MariaDB for licensing freedom, open-source reliability, compatibility, and performance improvements while avoiding Oracle’s restrictions on MySQL.

==**How Oath 2.0 works**==
 * In Appian, OAuth 2.0 is supported through Connected System objects and HTTP OAuth 2.0 configuration.
 * Appian supports two main OAuth 2.0 grant types:
 1. **Authorization Code Grant (User Delegated Access)**
	  - Used when Appian must act **on behalf of a logged-in user**.
	  - Example: Fetching a user’s Outlook emails (`/me/messages`).
	  - Flow:
		  1. User logs in → Appian redirects to the provider’s login page.
		  2. User grants consent → provider issues an **Authorization Code**.
		  3. Appian exchanges that code for an **Access Token** (+ Refresh Token).
		  4. Access Token is used in API calls (expires in ~1 hour).
		  5. Refresh Token silently renews access without re-login.
2. **Client Credentials Grant (System-to-System)**
	- Used when Appian acts as a **service account** (no user login).
	- Example: Appian needs to push data to an external system nightly.
	- Flow:
	    1. Appian sends its **Client ID + Secret** to the OAuth server.
	    2. Provider issues an **Access Token**.
	    3. Appian uses this token in API calls.

**How can I move forward a parent process based on the value changed in the second node of Subprocess.**
 - By Pass by reference

**Default alert goes to which users**
 - By default, alerts are automatically sent to process administrators, process model administrators, and system administrators.

**Case: Two different UITs with different assignees**
 - If two chained UIs are assigned to different users, the chain will break after the first UI. The next UI will be generated as a separate task for the second user, and they’ll need to open it from their task list(or receive it via email/task assignment).

**How can we configure the process that can be trigger from email**
1. Parsing the details of the email
	 - Inside the Data -> New mapping section use the **msg!properties** domain and **msg!body** domain to map the email metadata.
2. Allowing the process model to receive emails
	 - Once you have parsed the email contents, now it is time to allow the Process Model to receive these emails. It can be done simply by checking a box in the process properties.
	 - **Check right Public Events**, which Allow anyone to fire triggers.
3. Constructing the email ID
	 - Now comes the final part, to construct the email ID to which these emails will be sent. For that, you will need to copy the UUID of the process model and paste it in below text along with the URL of your Appian environment.
	 - processmodeluuiduuid@yourappianenvironment.appiancloud.com
		 Example: processmodeluuid0006e543-b132-8000-01f5-7f0000014e7a@appianspace.appiancloud.com.

**What is the main difference between dictionary and map in Appian?**
- Normally, if Appian needs to store a mix of types, it wraps them in ==**Variants**, like in Dictionary==.
- But with **Maps (`a!map()`)**, Appian stores the values **directly**, _without extra wrapping_.
- This makes maps more efficient and easier to handle when interacting with **APIs / JSON**.
- - In a **Dictionary/Typed CDT**, Appian might internally wrap these as `Variant(Text)`, `Variant(Integer)`, etc.
- In a **Map**, they’re stored as raw values → `"Ravi"`, `29`, `true`, `2025-09-05`.


**Is there any other way we can type cast the integer value without using tointeger()**
 - `cast( 'type!{http://www.appian.com/ae/types/2009}Integer', "12" )`

**what will happen on Deleting a process instance?**
 - Deleting a process will also delete any synchronous subprocesses and pending tasks associated with those subprocesses. Processes and pending tasks started with the Start Process smart service will not be deleted automatically, but you can select and delete them if required.

**How to display archived process to user**
 - Leverage the Process Activity tab in the Monitor view to allow users with appropriate permissions to see the history of archived processes for auditing
 - select a archived instance, click on unarchive, it will be visible in the completed instance. Or we can also see the History of the process variables.
 
 **How to display 40-80k excel rows to the user with performant way?**