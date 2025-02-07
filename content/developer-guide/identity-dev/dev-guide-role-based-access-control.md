---
uid: accessControl
---

# Role-based access control

Use an Access Control List (ACL) to manage role-based access control to entities such as namespaces and streams. ACLs control user access to entities based on their roles. Each entity has an owner, who has access for all operations regardless of the contents of the ACL. Not all entities support role-based access control.  <!--Angela Flores 6/23/21 We should not talk about unreleased functionality or future functionality in the end-user documentation. Original text "Not all entities in the OCS system support role-based access control at this time, but the list will quickly grow and currently includes Namespaces and several unreleased entities." We should list all the entities that do support an ACL. How does access work for entities that don't support an ACL? -->

## Access Control Lists

Access Control Lists (ACLs) contain sets of Access Control Entries (ACEs), which contain the following information:

- TrusteeType - the role for whom access is set 
- AccessType - the access permitted, either allowed or denied
- AccessRights - the access rights allowed or denied to the Trustee specified 

A user or application that attempts to read, write, delete, or manage access control of an entity assigned an ACL must be assigned a trustee that has `AccessType` set to `Allowed` for the AccessRight corresponding to that operation.

### Collections with ACL endpoints

The following table shows whether endpoint collections have an endpoint for access control. For more information on using access control for each supported collection, select the collection link.

| Endpoint Collection | ACL Endpoint |
|--|:--:|
| [Asset store](xref:assets-access-control-list) | &#10004; |
| [Communities: Communities](xref:community-communities#accesscontrollist)<sup>1</sup> | &#10004; |
| [Communities: Tenants](xref:community-tenants)<sup>1</sup> | &#10004; |
| [Data collection](xref:omf-ingress-access-control) | &#10004; |
| [Data views](xref:DataViewsAccessControlAPI) | &#10004; |
| Identity and access management | ✘ |
| Operations | ✘ |
| [Rules: Asset rules](xref:assets-access-control-list) | &#10004; |
| [Rules: Metadata rules](xref:metadata-access-control-list) | &#10004; |
| [Sequential Data Store](xref:sds-access-control-list) | &#10004; |
| [Tenant Management](xref:tenant-root-access-control) | &#10004; |

<sup>1</sup>: The Communities collection contains two different access control endpoints—one for communities and one for community tenants.

### Notes

- If an operation requires more than one access right, then an identity obtains those rights from multiple ACL entries.
- `AccessType.Denied` takes precedence over `AccessType.Allowed`.
  - For example, a role that is assigned `AccessType.Denied` for `AccessRights.All` will receive a `forbidden` for all  requests unless they are the owner of the entity.
- Roles are the only TrusteeType supported for AccessControlList ACEs.
- At least one role must be given Manage Permission access.

### Trustee

The following table shows TrusteeTypes and the corresponding TypeIds.

| TrusteeType           | TypeId |
|-----------------------|--------|
| User                  | 1      |
| Application           | 2      |
| Role                  | 3      |

The following table shows AccessTypes and the corresponding TypeIds.

| AccessType            | TypeId |
|-----------------------|--------|
| Allowed               | 0      |
| Denied                | 1      |

### Common access rights
The following table shows predefined access rights and their corresponding integer and bitwise information.

| AccessRights          | int  | bitwise |
|-----------------------|------|---------|
| None                  | 0    |   00000 |
| Read                  | 1    |   00001 |
| Write                 | 2    |   00010 |
| Delete                | 4    |   00100 |
| ManageAccessControl   | 8    |   01000 |
| Share                 | 16   |   10000 |
| All                   | 31   |   11111 |

Access rights are determined by the union or summation of one or more individual access rights. For example `AccessRights: 3` indicates that the `Read (1)` and `Write (2)` access are permitted.

### Sample Access Control List

The following code sample shows the structure and format for an ACL that gives Role 1 `Read` access, Role 2 `All` access but denies Role 3 `ManageAccessControl` access:

**Body**

Sample  body:

```json
HTTP/1.1 200
Content-Type: application/json

{
  "RoleTrusteeAccessControlEntries": [
    {
    	"Trustee": {
    		"Type": 3,
    		"RoleId": "11111111-1111-1111-1111-111111111111"
    	},
    	"AccessType": 0,
    	"AccessRights": 1
    },
    {
		"Trustee": {
			"Type": 3,
    		"RoleId": "22222222-2222-2222-2222-222222222222"
    	},
    	"AccessType": 0,
    	"AccessRights": 15
    },
    {
		"Trustee": {
    		"Type": 3,
    		"RoleId": "33333333-3333-3333-3333-333333333333"
    	},
    	"AccessType": 1,
    	"AccessRights": 8
	}
],
}
```

## Owner

Set an owner on an entity to grant access for all operations on the entity regardless of the access set in the ACL. Only users and applications are valid owners for entities. Users are identified with their `ObjectId`, and applications are identified with the `ApplicationId`.

The following code samples shows the format and structure of an owner object.

**User Owner Body**

```json
"Owner": {
	"Type": 1,
	"TenantId": "55555555-5555-5555-5555-555555555555",
	"ObjectId": "44444444-4444-4444-4444-444444444444"
},
```

**Application Owner Body**

```json
"Owner": {
	"Type": 2,
	"TenantId": "55555555-5555-5555-5555-555555555555",
	"ApplicationId": "66666666-6666-6666-6666-666666666666"
},
```
