# **Study Case: User and Permission Management in a Linux Environment**

---

## **Objective**

To demonstrate and apply Linux user and permission management techniques using commands such as:
`useradd`, `usermod`, `passwd`, `chown`, `chmod`, and `sudo`.

This case study simulates a real-world scenario of onboarding new team members into a secure Linux-based development environment.

---

## **Scenario Overview**

A new development team is joining **TechCorp’s** internal Linux server. The team includes:

- **Alice** (Team Lead)  
- **Bob** (Developer)  
- **Charlie** (Developer)  

The system administrator must create and configure their user accounts and access permissions according to the following requirements:

### **Requirements**

- Each user must have a personal login and home directory.  
- A shared project directory must be accessible to all team members.  
- Each user should only access their own files, except within the shared directory.  
- Only Alice, as the team lead, should have administrative (`sudo`) privileges.  

---

## **Implementation Steps**

### 1. **Create User Accounts**

Use the `useradd` command to create users and `passwd` to set initial passwords.

```bash
sudo useradd -m alice
sudo passwd alice

sudo useradd -m bob
sudo passwd bob

sudo useradd -m charlie
sudo passwd charlie
