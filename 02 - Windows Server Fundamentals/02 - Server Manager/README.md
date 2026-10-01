# Server Manager

## 1. What is Server Manager?

Server Manager can be defined as follows.

**Server Manager** is a Windows Server management console that provides administrators with a centralized interface for viewing and managing Windows Server systems, roles, features, services, events, and administrative tools.

Instead of opening many different Windows management utilities individually, Server Manager gives an administrator a central place to access many of them.

The overall relationship can be represented as:

```text

                    SERVER MANAGER

                          │

        ┌─────────────────┼─────────────────┐

        │                 │                 │

     Server             Roles             Tools

     Status             Features          Utilities

        │                 │                 │

     Events             AD DS            Event Viewer

     Services           DNS              Services

     Performance        DHCP             Task Scheduler

     Updates            etc.             Computer Management

```

Server Manager is not the server itself; it is a **management interface** used to administer Windows Server.

## 2. Why does Windows Server have Server Manager?

For an administrator responsible for multiple Windows servers, common requirements include:

* Are the servers healthy?

* Are there errors?

* What roles are installed?

* What services are running?

* Are there notifications?

* What administrative tools are available?

* Are there configuration issues?

* Do any servers require attention?

Opening dozens of separate utilities for every server would be inefficient. Server Manager provides a **centralized administrative experience**.

In a small environment:

```text

  Administrator

        ↓

      DC01

        ↓

  Server Manager

```

In a larger environment, Server Manager can also be used to manage multiple Windows Server machines:

```text

                 Administrator

                       │

                Server Manager

                       │

        ┌──────────────┼──────────────┐

        ↓              ↓              ↓

      DC01           SRV01          SRV02

   Domain/DNS      File Server     Application

```

This represents one of the main purposes of Server Manager: **centralized Windows Server administration.**

## 3. Server Manager vs Windows Settings

This distinction helps clarify the different management environments.

On **Windows 11**, you commonly use:

* Settings

* Control Panel

* Windows Tools

On **Windows Server**, administrators frequently work with:

* Server Manager

* Computer Management

* PowerShell

* Command Prompt

* Administrative Tools

Server Manager is designed specifically around **server administration**.

## 4. History of Server Manager

* **Before Server Manager:** Older Windows Server versions relied heavily on separate management consoles and tools. Administrators often had to work with different utilities individually.

* **Windows Server 2008:** Microsoft introduced Server Manager as a central management interface. It became an important part of Windows Server administration.

* **Later versions:** Server Manager continued evolving and gained capabilities for server roles, features, remote server management, events, services, performance, Best Practices Analyzer, server grouping, and administrative tools.

Windows Server 2022 therefore includes a mature version of Server Manager.

## 5. Exploring DC01

 **No configuration changes are required at this stage.**

1. Log into **DC01**.

2. Open **Server Manager**.

*Server Manager usually opens automatically after logging into Windows Server. If it is not open, use Start → Server Manager.*

The Server Manager dashboard is displayed.

## 6. Dashboard

The first area documented here is the **Dashboard**. The dashboard provides an overview of the server environment.

![Server Manager Dashboard](<../Screenshots/03 - Server Manager.png>)

> *"What information is Server Manager presenting to the administrator?"*

The dashboard contains areas related to:

* Roles and Server Groups

* Local Server

* Events

* Services

* Performance

* Best Practices Analyzer

* Notifications

The dashboard acts as the starting point for server management. The basic flow is:

`Server Manager → Dashboard → "What needs my attention?"`

## 7. Local Server

Select **Local Server**.

The Local Server page provides information about the server currently being managed. In this lab, the server is **DC01**.

![Local Server](<../Screenshots/04 - Local Server.png>)

You'll encounter information such as:

* Computer name

* Domain

* Windows activation

* Windows Update

* Remote management

* Remote Desktop

* Network configuration

* Windows Defender-related information

* NIC/team information

* Time zone

* Hardware-related information

**No configuration changes are required here; the purpose is to review the available information.**

### Administrator Perspective

The Local Server page can be reviewed with the following question:

> *"If this server were handed over for administration, what information could be identified from this page?"*



## 8. Manage

The **Manage** menu is located in the top-right corner.

The menu contains options related to server administration, including:

![Manage](<../Screenshots/05 - Manage.png>)

* Add Roles and Features

* Remove Roles and Features

* Add Servers

* Server Manager Properties

**Manage = actions for managing servers, roles, and features.**

## 9. Tools

The **Tools** menu is located in the top-right corner.

The Tools menu provides access to a large collection of Windows administrative utilities, including:

![Tools](<../Screenshots/06 - Tools.png>)

* Computer Management

* Event Viewer

* Services

* Task Scheduler

* Device Manager

*(Additional administrative utilities are also available.)*



`Server Manager → Central management interface → Tools → Individual management consoles`

For example:

```text

Server Manager

      │

      ├── Event Viewer

      ├── Services

      ├── Task Scheduler

      ├── Computer Management

      └── Device Manager

```

## 10. Notifications

The **Notifications** area is represented by the flag icon.

![alt text](<../Screenshots/07- Notifications.png>)

This area reports conditions that may require administrator attention.

`Server Manager → Notifications → Something requires attention`

This provides a centralized way to identify conditions that may require attention without manually inspecting every component continuously.

## 11. Performance

Server Manager also provides access to server performance information. At this stage, the focus is on understanding the purpose of this information rather than memorizing individual metrics.

![Performace](<../Screenshots/08 - Performance.png>)

The basic relationship is: **Performance → How is the server behaving?**

Typical areas of interest include:

* CPU

* Memory

* Disk

* Network



## 12. Add Roles and Features

One of the primary Server Manager functions is **Add Roles and Features**, available under **Manage → Add Roles and Features**.

![Add Roles and Features](<../Screenshots/09 - Add Roles and Features.png>)

This wizard is used to install Windows Server roles and features:

* **Roles** (provide a major server function)

* *Examples:* Active Directory Domain Services, DNS Server, DHCP Server, File and Storage Services, Web Server (IIS)



* **Features** (provide an additional capability)

* *Examples:* Additional Windows capabilities that are not necessarily complete server roles.



## 13. Refresh

A **Refresh** button is available throughout Server Manager because server information can change.

![Refresh](<../Screenshots/10 - Refresh.png>)

`Service status changes → Server Manager information → Refresh → Updated information`

It updates the displayed information to reflect the current server state.

## 14. Events

Server Manager can surface events from Windows systems. This is relevant to SOC operations because Windows events provide important information for later log analysis and investigation.

![Events](<../Screenshots/11 - Events.png>)

At this stage, the relationship can be summarized as:

`Windows → Events generated → Event logs → Server Manager can surface relevant information`



## 15. BPA — Best Practices Analyzer

Another Server Manager component is **BPA (Best Practices Analyzer)**.

BPA is designed to check server roles against Microsoft's recommended configuration practices and identify potential issues.

![BPA](<../Screenshots/12 - BPA.png>)

`Server configuration → BPA checks → Potential configuration issues → Administrator reviews them`

*Important:* BPA does not automatically determine that a server is secure. It helps administrators identify configuration conditions that may not follow recommended practices.

---

### Server Manager Mental Model

The overall Server Manager relationship can be represented as follows:

```

                         SERVER MANAGER

                               │

          ┌────────────────────┼────────────────────┐

          │                    │                    │

      Dashboard          Local Server             Manage

          │                    │                    │

      Overview          Current server       Administrative

                         information             actions

                                                   │

                                                   ↓

                                          Roles&Features



                         SERVER MANAGER

                               │

                               ↓

                             Tools

                               │

          ┌────────────┬───────┼────────┬────────────┐

          ↓            ↓       ↓        ↓            ↓

     Computer       Services  Event   Task       Device

     Management               Viewer  Scheduler  Manager

```

*The objective is to understand the relationship rather than memorize the diagram.*