# elavate-lab-task-4 
## Task 4  : Setup and Use a Firewall on Windows/Linux

### Objective: Configure and test basic firewall rules to allow or block traffic.
### Tools:  Windows Firewall / UFW (Uncomplicated Firewall) on Linux.
### Deliverables: Screenshot/configuration file showing firewall rules applied


# Step 1: Install and Enable UFW ( not already installed)
## Open your terminal and run:

sudo apt install ufw -y

![WhatsApp Image 2025-08-08 at 19 30 57_b5db693a](https://github.com/user-attachments/assets/70ed21d7-df3b-47cb-abdb-f6ff1b262502)


Enable UFW:
sudo ufw enable

Check UFW status:
sudo ufw enable

![WhatsApp Image 2025-08-08 at 19 30 55_106c29a1](https://github.com/user-attachments/assets/9d71f411-3041-4820-88a2-df9c4168030d)


Check UFW status:
sudo ufw status verbose

![WhatsApp Image 2025-08-08 at 19 30 55_106c29a1](https://github.com/user-attachments/assets/be76df72-be0e-4f2f-872c-052fe9dbcffc)


# Step 2: List Current Firewall Rules

## To see current rules:
--> sudo ufw status numbered

![WhatsApp Image 2025-08-08 at 19 30 55_0b745f0c](https://github.com/user-attachments/assets/47a19d0c-8c71-4bc3-a987-cbfea63b0f25)


# Step 3: Add a Rule to Block Inbound Traffic on Port 23 (Telnet)
## This blocks Telnet (port 23):
--> sudo ufw deny 23

### Check if the rule was added:
--> sudo ufw status numbered

![WhatsApp Image 2025-08-08 at 19 36 34_fd351ad6](https://github.com/user-attachments/assets/10352fc4-fa8a-4ae0-8614-8e4c8987ab8e)


# Step 4: Test the Rule
##  To test port 23 is blocked:

### Open another terminal.

### Use telnet or nmap from the same or another VM to test port 23.

Example with telnet:
-->  telnet localhost 23


![WhatsApp Image 2025-08-08 at 19 30 57_308966a6](https://github.com/user-attachments/assets/c258077e-2d17-44bc-9d98-acea52575fc8)



You should get a "Connection refused" or it will just hang.

Example with nmap:

-->  nmap -p 23 localhost
Expected: Port 23 should show as "filtered" or "closed"

![WhatsApp Image 2025-08-08 at 19 30 58_f593fc31](https://github.com/user-attachments/assets/b2e47c81-a121-4481-a43e-8e832f9506ef)


# Step 5: Allow SSH (Port 22)
##  This is important so you don’t accidentally block remote access (if using SSH):

-->  sudo ufw allow 22
Confirm it:

sudo ufw status numbered

![WhatsApp Image 2025-08-08 at 19 30 57_02194be4](https://github.com/user-attachments/assets/109d2800-e2dc-4e55-9e03-226de6e2e9c0)


#  Step 6: Remove the Test Block Rule (Restore Original State)
##  To delete the Telnet (port 23) rule:

###   First, find the rule number using:

-->  sudo ufw status numbered
### Delete the rule for port 23 using the rule number. For example, if it’s rule #1:

--> sudo ufw delete 2

![WhatsApp Image 2025-08-08 at 19 30 57_4fa07fb2](https://github.com/user-attachments/assets/3ac0dbcb-fb97-4138-b57a-028451874ace)


Confirm it's gone:
--> sudo ufw status numbered

#  Outcome:
## Basic firewalls management skills and understanding of network traffic filtering

# skills learned

 ### Firewall configuration
 ### network traffic filtering
 ### ports
 ### UFW
 ### Windows Firewall.

# Interview questions 

### ✅ **1. What is a firewall?**

A **firewall** is a security system that monitors and controls **incoming and outgoing network traffic** based on predefined rules. It acts as a barrier between a trusted internal network and untrusted external networks, such as the internet.

---

### ✅ **2. Difference between Stateful and Stateless Firewall?**

| Feature             | **Stateful Firewall**                             | **Stateless Firewall**                         |
| ------------------- | ------------------------------------------------- | ---------------------------------------------- |
| **Tracks sessions** | Yes, tracks active connections and session states | No, treats each packet independently           |
| **Security level**  | Higher (context-aware)                            | Lower (packet-based only)                      |
| **Example**         | iptables with connection tracking                 | Simple ACLs (Access Control Lists)             |
| **Use case**        | Enterprise firewalls, dynamic environments        | Simpler setups or performance-critical systems |

---

### ✅ **3. What are Inbound and Outbound Rules?**

* **Inbound rules**: Control traffic **coming into** your system from the network (e.g., blocking port 23).
* **Outbound rules**: Control traffic **leaving your system** to the network (e.g., restricting access to external servers).

---

### ✅ **4. How does UFW simplify firewall management?**

UFW (Uncomplicated Firewall) provides a **user-friendly command-line interface** to manage firewall rules in Linux. It simplifies complex `iptables` commands into **simple, readable syntax**, making firewall configuration easier for users and system admins.

Example:

```bash
sudo ufw allow 22
sudo ufw deny 23
```

---

### ✅ **5. Why block port 23 (Telnet)?**

Port 23 is used by **Telnet**, which sends data (including passwords) in **plain text**, making it insecure. It's often targeted by attackers. Blocking it helps **prevent unauthorized access** and **improves network security**.

---

### ✅ **6. What are common firewall mistakes?**

* Forgetting to **allow SSH (port 22)**, locking yourself out.
* Not reviewing or cleaning **old/unused rules**.
* Using **conflicting or overlapping rules**.
* Allowing **open ports** without restriction.
* Not applying the rules after configuration.

---

### ✅ **7. How does a firewall improve network security?**

A firewall:

* **Blocks unauthorized access**.
* **Limits attack surfaces** by restricting unnecessary ports.
* Helps detect and stop **malicious traffic**.
* Allows only **trusted services** (like SSH, HTTPS) to run.
* **Logs traffic activity**, useful for audits and investigation.

---

### ✅ **8. What is NAT in firewalls?**

**NAT (Network Address Translation)** allows multiple devices on a local network to share a **single public IP address**. In firewalls, NAT:

* **Hides internal IP addresses** from external networks.
* Adds an **extra layer of security** by preventing direct access to internal systems.
* Common in **home routers and corporate networks**.

---

