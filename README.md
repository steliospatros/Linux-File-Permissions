# Linux File System Security & Access Management

## 1. Project Overview
This project details the auditing and modification of file and directory permissions within a Linux environment to enforce the Principle of Least Privilege (PoLP). The objective was to update authorization levels for specific project directories and hidden files to align with organizational security policies.

## 2. Tools & Environment
* **OS Environment:** Linux (Bash Shell)
* **Commands Used:** ls, chmod
* **Concepts:** User/Group/Other access levels, Read/Write/Execute (rwx) permissions, Hidden files management.

## 3. Auditing Existing Permissions
The initial step involved utilizing the ls -la command to generate a detailed, hidden-inclusive listing of the /home/researcher2/projects directory contents. 

By analyzing the 10-character permission strings, unauthorized access levels were identified (e.g., 'Other' entities possessing write capabilities on sensitive files).

## 4. Remediation & Access Control Enforcement

### Scenario A: Revoking Unwanted Write Access
Organizational policy dictates that 'Other' users should not possess write access to project files. This was corrected using the chmod command.

```bash
-- Verify initial permissions
ls -la

-- Revoke write permissions (w) from 'other' (o) for the specified file
chmod o-w project_k.txt
```

### Scenario B: Securing Archived Hidden Files
An archived hidden file (.project_x.txt) required strict access modifications: removal of write access for both User and Group, and assignment of read-only access to the Group.

```bash
-- Modify user (u) and group (g) permissions simultaneously
-- Remove write from user/group, add read to group
chmod u-w,g-w,g+r .project_x.txt
```

### Scenario C: Restricting Directory Execution
To secure the drafts subdirectory, execute permissions were restricted exclusively to the primary researcher, stripping access from the broader group.

```bash
-- Remove execute permissions (x) from 'group' (g) for the drafts directory
chmod g-x drafts

-- Verify the final security posture of the directory
ls -la
```

## 5. Key Takeaways
Proper file permission management is a foundational element of system security. This project demonstrates proficiency in reading Linux authorization structures and utilizing command-line tools to swiftly enforce strict access control models.
