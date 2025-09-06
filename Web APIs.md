**Security needed to invoke Web API from outside.**
	To invoke a Web API from outside Appian, you need:
	1. Object Security → Caller must have **==Viewer==** access on the Web API.
	2. Authentication → Done via API Key, OAuth 2.0, or Basic Auth.
    3. Service Account → Usually created just for integrations, with minimum required rights. (In both API key or OAuth 2.0 we need service account)
    
**You are facing a performance issue in Web API response, what will be your approach to resolve this?** 
	First, I’d identify where the delay is coming from – Appian expressions, database queries, or external integrations. Then I’d optimize queries with proper filters/indexes, streamline Appian logic, and minimize payloads. If the issue is external, I’d handle it with asynchronous calls or caching. Finally, I’d check server resources and apply best practices to ensure the API responds quickly.

**Web API Methods** 
 - So Basically in Appian there are 2 ways to make a Web API 
 1.  Create from template
 2. From Scratch
	 - Here we have all the methods available:
	 1. **GET**:  Used to **retrieve** data from Appian.
	 2. **POST**:  Used to **create** or submit data to Appian.
	 3. **PUT**:  Used to **update/replace** existing data. Overwrites the full record. Payload Must include all fields (even if only one changed).
	 4. **PATCH**:  Used to **partially update** existing data (only specific fields). Modifies only specified attributes.
	 5. **DELETE**:  Used to **remove** data.