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

**Sources of Record**
 *  The source of a record is defined either through the **Data Source Management** settings in the Admin Console or by creating **Connected Systems**, after which it becomes available in Appian record as a data source.

**What comes after selecting different type of sync when creating record**
1. Incase of **Sync record**
	  - It asked to **choose Database table**.
2. Incase of **disable sync record**
	 - It is asked to **choose Data Store and Entity.**
	 - Therefore, creating a sync record we need to first create a datastore and its entity.

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
	 - ==**processmodeluuid<uuid>@yourappianenvironment.appiancloud.com.==
		 Example: processmodeluuid0006e543-b132-8000-01f5-7f0000014e7a@appianspace.appiancloud.com