# Home Network Documentation
This document provides a detailed record of the physical layout, logical structure, device configuration, and security management guidelines for the home network, and is intended for network maintenance and troubleshooting.

## 1. Physical Topology
Physical topology focuses on the physical locations of devices and the layout of their hardwired connections.
<img src="download.png.png" alt="Topology" width="500">
1. __Network Topology Diagram__
   
    Below is the comprehensive visualization of the home network's physical topology, showing device locations, connections, and medium types.

3. __List of Physical Equipment__





## PURPOSE OF THE DOCUMENT
_This SOP shows how to quickly set up a standard Linux server for web testing. By using the same system settings and tools every time, we make sure any bugs that we find are real and not just caused by a messy setup._
 <br><br/>
## AUDIENCE


## Approved Table:
| Role         | Name       | Signature | Date       |
| :------------ | :--------- | :-------- | :--------- |
| IT Manager    | Qianyi Wen |  Signed   | 2026/03/27 |
| QA Engineer   | Spike 1    |  Signed   | 2026/03/27 |
| DevOps Expert | Spike 2    |  Signed   | 2026/03/27 |
| Project Lead  | Spike 3    |  Signed   | 2026/03/27 |

## SCOPE/OBJECTIVES
This document defines how we set up test environments. Our goal is to keep operations focused and fast.
- __Applicable Audience__: This document applies only to the QA testing department.
- __Scope__: Limited to the setup of internal functional testing, integration testing, and security scanning environments.
Only the Ubuntu 22.04 LTS release is supported. 
## ACCOUNTABILITY MATRIX
| Task/Phase | QA engineer | IT manager | DevOps expert | Project lead |
| :------------ | :--------- | :-------- | :--------- | :--------- |
|Step 1: Virtual Machine Resource Configuration | Responsible | Accountable| Consulted | Informed|
|Step 2: System Initialization and Update | Responsible | Accountable| Informed | Informed|
|Step 3: Installing the Software Stack and Toolchain | Responsible | Accountable| Consulted | Informed|
|Step 4: Security Hardening and UFW Configuration | Responsible | Accountable| Consulted | Informed|
|Step 5: Environment Verification and Snapshot Creation | Responsible | Accountable| Informed | Consulted|
#### Role Definitions:

- __Responsible__: The person who performs the task. 

- __Accountable__: The person with final approval authority.

- __Consulted__: The expert who provides key technical knowledge.

- __Informed__: Members who need to be kept informed of progress and results.

## EXECUTION STEPS
__Step 1: Pre-creation planning and assessment__
- Step 1.1: Identify purpose and requirements
  1. Decide exactly what this VM will do.
  2. Start with these basics: ```CPU: 2 vCPUs / RAM: 4GB / Storage: 40G / Network: testing VLAN.```
- Step 1.2 Check the resources
  1. Make sure the server has enough leftover CPU and Memory.
  2. Use SSD storage for better speed.
  3. Decide if you need to "reserve" RAM so the VM stays fast during heavy testing.
- Step 1.3: Talk to the team
  1. Double-check which software versions they need
  2. Ask for static IP addresses and make sure the firewall rules for testing.

__Step 2: VM provisioning__
- Step 2.1: Start VM
  1. Open the vSphere Client and sign into your vCenter Server.
  2. Go to the Resource Pool where you want the VM to live.
  3. Right-click that spot and click ```"New Virtual Machine"```.
  4. Pick ```"Create a new virtual machine"``` and click Next.
- Step 2.2: Set up the VM details
  1. Enter ```test-01``` as the name and choose its folder.
  2. Select``` the specific ESXi host``` to run the VM.
  3. Select ```Linux and Ubuntu Linux 64-bit```.
  4. Set the CPU and RAM and make sure the Network is plugged into the right port group.

__Step 3: OS Installation and configuration__
- Step 3.1: Guest OS deployment
  1. attach the Ubuntu 22.04 ISO using the vSphere console.
  2. Follow the prompts to install the OS and create a local admin user named ```tester```.
  3. Run the following to improve performance: ```sudo apt install open-vm-tools -y```
- Step 3.2: System initialization
  1. Get the latest security patches: ```sudo apt update && sudo apt upgrade -y```
  2. Download the standard toolkit for troubleshooting:```sudo apt install curl git htop net-tools -y```

__Step 4: Web application environment setup__
- Step 4.1: Deploy container runtime
  1. Run the following command to download and install the Docker engine: ```curl -sSL https://get.docker.com | sh```
  2. Add the ```"tester"``` user to the Docker group. This lets you run containers without needing ```sudo``` every time.
- Step 4.2: Install testing dependencies
  1. Set up Nginx to handle web traffic and act as a gateway for your tests.
  2. Download the dependencies needed for automated UI testing.

__Step 5: Final security audit and snapshot__
- Step 5.1: Tighten network security
  1. Block everything except ports ```SSH```, ```HTTP```, and ```HTTPS```.
  2. Use SSH Keys for logging in instead of passwords
- Step 5.2: Final check
  1.Make sure the status shows as ```"Running, Version: Guest Managed."```
- Step 5.3: Save progress
  1. In vSphere, right-click your VM, go to ```Snapshots```, and select ```Take Snapshot```.
  2. Use the name ```Baseline_Setup```.
## REVISION HISTORY
| Version | User | Date | Brief description of changes Made | 
| :------------ | :--------- | :-------- | :--------- | 
| v1.0 | Qianyi	| 2026/03/27 |	Draft of standard operating procedures for web application test server. |
| v1.1 |  Qianyi | 2026/03/27 | Integrates RACI matrices and provides detailed vSphere execution steps. |
| v1.2	|  Qianyi | 2026/03/27 | The scope and objectives have been updated based on stakeholder feedback. |
