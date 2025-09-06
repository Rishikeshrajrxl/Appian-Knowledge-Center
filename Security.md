**Why we use deny**
- The Deny option explicitly blocks a user or group from accessing an object even if they inherit access from elsewhere.
	
**What happens if a person is in both Deny Group and Access Group in Appian?**
- The Deny always wins.
- Even if the user has Viewer/Editor/Admin access through another group,
- If they are also part of a Deny group, they will be completely blocked from the object.