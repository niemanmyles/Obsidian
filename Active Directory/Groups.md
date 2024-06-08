Groups are used to place users, computers, and contacts into management units. Groups have two fundamental characteristics: *type* & *scope* 

**type**: defines purpose
- Security
	- Primarily used for assigning permissions and rights to groups of users
- Distribution
	- Mainly used by email applications to distribute messages to members, similar to mailing lists
**scope**: defines how the group can be used, and there are three scopes that can be assigned.
- Domain Local Group: Can only be used to manage perms to domain resources in the domain where it was created. Can contain users from other domains
- Global Group: Can be used to grant access to resources in other domains
- Universal Group: Used to give perms to any object within a forest

Group scopes can be changed, but there are a few caveats:

- A Global Group can only be converted to a Universal Group if it is NOT part of another Global Group.
    
- A Domain Local Group can only be converted to a Universal Group if the Domain Local Group does NOT contain any other Domain Local Groups as members.
    
- A Universal Group can be converted to a Domain Local Group without any restrictions.
    
- A Universal Group can only be converted to a Global Group if it does NOT contain any other Universal Groups as members.


## Important Group Attributes

Like users, groups have many [attributes](http://www.selfadsi.org/group-attributes.htm). Some of the most [important group attributes](https://docs.microsoft.com/en-us/windows/win32/ad/group-objects) include:

- `cn`: The `cn` or Common-Name is the name of the group in Active Directory Domain Services.
    
- `member`: Which user, group, and contact objects are members of the group.
    
- `groupType`: An integer that specifies the group type and scope.
    
- `memberOf`: A listing of any groups that contain the group as a member (nested group membership).
    
- `objectSid`: This is the security identifier or SID of the group, which is the unique value used to identify the group as a security principal.