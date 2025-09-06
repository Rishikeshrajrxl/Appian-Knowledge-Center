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