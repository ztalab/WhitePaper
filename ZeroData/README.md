# Zero Data White Paper

## Thank you for your attention to Zero Data.

Zero Data helps organizations improve database security by providing a better and simpler way to protect your database security.

The information contained in this document is designed to provide customers and potential customers with the security status, practices and processes of Zero Data. Zero Data ensuring database security is a continuous improvement process, and we will continue to evaluate and support it.

## Project Background

In the current environment, more and more applications are migrated to the cloud or provided by third-d platform providers, and more and more users work remotely at home or in public places, which will make the network environment more complex and bring more prominent data security issues, including database access security and connection information security. All right. Therefore, Zero Data makes its own thinking on database security and realizes a unique database security access system based on zero-trust network access.

**Database access security**：In its research, Imperva, a network security company, shows that nearly half of the database it scans contains CVE vulnerabilities. Therefore, it is essential for data access authorization and security protection. However, most enterprises do not provide sufficiently effective protection.

**Connection information security**：Because ordinary development and operation and maintenance personnel have access to service development containers and online service operation containers to facilitate problem isolation. The database connection information is exposed to environmental variables, so junior personnel may use the connection information to directly connect to the database and modify the data to destroy the normal development iteration process. And delete the entire database data due to misoperation. Therefore, the development of this system hides the database connection information and prevents most development operation and maintenance personnel from obtaining database connection information.

## Product Architecture Design

### Design Concept

Zero Data was originally designed to provide a secure solution for accessing the database. Access to the database is now diversified:

- Most projects access the database to configure database connection information in plain text.
- Most database access control uses database account password control.
- Database access is increasingly cloud-based or managed by third parties.

Therefore, traditional database access forms cannot meet today's security or availability needs. Zero Data provides a method based on the concept of zero trust access.

### Zero Trust Access (ZTA)

Unified management portal

- Provide a unified visualization platform to complete all access control, security policies and confidential information management.

Minimum Privilege Principle Permission Control

- Permission control can be set for instances, libraries, tables and fields. The permission product is closed, and visitors will not have access to the actual database account password.
- Provide a role-based user permission policy, which can flexibly configure different user permissions and support querying and changing different security permissions.
- Incidents should be recorded in detail to support monitoring, detection, investigation and other analysis.

Zero intrusion data security enhancement

- Improve security in a zero-intrusion way without any changes to the business code. Support with data for identity, authentication and authorization.
- Enable ubiquitous encryption and verification by default in a zero-trust mode to enhance the security of data transmission and data access.
- Sensitive data, such as database access account password, etc., are encrypted and stored. With the help of data-face agents, users do not need to touch real password information, reducing the possibility of leakage.
- Direct access to the database or public network exposure can be avoided through private structure proxy, ensuring that all access is authorized.

Automated threat mitigation, remediation and security audit, risk reporting

- Provide records of database access behaviors, alert risk behaviors, and provide the ability to track and analyze after the event.

- Provide various report and icon statistics functions, automate visibility, block high-risk behavior according to control access strategies and historical behavior analysis, and implement continuous monitoring.

  Dynamic desensitization support

- Through the data surface, dynamic data desensitization can be realized to protect key information from the source. It allows developers and testers to access information but cannot view sensitive content that should not be seen.

In summary, these principles are reflected in our products in the following ways:

- User and data flow authorizations are always confirmed by running multiple checks through multiple components. In addition, user data streams and user authentication streams are handled by separate components and require separate verification checks.
- We entrust user authentication to a third-party authentication provider (IdP), providing an additional layer of security.
- We support extensive logging, provide enhanced visibility, and help administrators monitor, troubleshoot and investigate the activities of the entire network and terminal, including unauthorized activities, as well as the activities of individuals authorized to access resources that may exceed their business authority.

From the customer's perspective, our product architecture provides additional security advantages in the following aspects:

- **Hide the network** - Zero Data does not expose access points publicly to your network to facilitate secure remote access to internal network resources and strong identification of connectors. Attack ransomware can be stopped before accessing the database.
- **Protect database account information **- Zero Data middleware can proxy database requests from the target service and parse database protocols. Therefore, when using the database service to initiate a connection to the middleware, the username password used is only a unique key tag. Middleware can replace verification information such as username and password with real verification information, and initiate a connection verification request to the real database service. Database request for proxy target service. This allows the service to complete data acquisition without access to information such as real passwords.
- **Runtime data confidentiality** - Some confidential data, such as the token of third-party systems, the data connection information mentioned above, etc., usually requires good encryption and storage. Through the platform management module, this part of information can be safely stored in the confidential storage component, and through the zero-trust runtime function, such data can be safely removed for the target service.
- **Centrally record all network activities** - The data surface can easily verify whether the visitor has access to the corresponding information, and can flexibly build authorization policies based on the information contained in the request context. At the same time, the behavior of the visitor is recorded, which can be used for subsequent analysis and audit.
- **Provide better availability for administrators** - Solutions that are easier to configure and maintain are less likely to make mistakes and more effective.

### Architecture & Component Overview

This section highly summarizes the main components that make up the Zero Data architecture and how they interact.

![image-20220518142331098](https://user-images.githubusercontent.com/52234994/169484736-0956e8fe-8ec9-40c3-baf5-72d483cb6910.png)

Zero Data protects access to the database. Together, they ensure that only authenticated users can access the resources they have access to. After Zero Data is fully configured, the final result is that authorized users can database without understanding the underlying network configuration. The main components are:

- Control plane - control strategy issued by the receiving management platform, dynamic regulation security strategy, receiving data plane reporting compliance evidence, telemetry data, etc.
- Data plane - the control policy issued by the receiving control platform, the implementer of the policy, providing runtime data security protection.
- Management platform - provides automated self-service tools for database access monitoring, orchestration and repair.
- Private proxy - When accessing data across public networks, it is necessary to prevent the database from being directly exposed to the public network, and deploy private agents before the database to strongly identify the connectors. Attack ransomware can be stopped before accessing the database.

## Application Scenarios

### Protect Database Account Information

Zero Data database middleware can proxy the database request of the target service and parse the database request protocol. Therefore, when using the database service to initiate a connection to the middleware, the username password used is only a unique key tag.

Middleware can replace verification information such as username and password with real verification information, and initiate a connection verification request to the real database service. Database request for proxy target service. This allows the service to complete data acquisition without access to information such as real passwords.

### Zero-trust Database Access

- Zero Data, as the data surface, can complete the identity verification, authentication and authorization of access. Its configuration is dynamically controlled by the control surface. Through the combination of control surface and data surface, it is convenient to finely control the permissions of each service/user, and data access control can be carried out with the principle of minimum privilege.
- Private proxy structure: When accessing data across public networks, it is necessary to prevent the database from being directly exposed to the public network, and deploy private agents before the database to strongly identify the connector. Attack ransomware can be stopped before accessing the database.
- Approval and audit: The data surface can easily verify whether the visitor has access to the corresponding information, and can flexibly build authorization policies based on the information contained in the requested context. At the same time, the behavior of the visitor is recorded, which can be used for subsequent analysis and audit.

### Runtime Data Confidentiality

Some confidential data, such as the token of third-party systems, the data connection information mentioned above, etc., usually requires good encryption and storage. Through the platform management module, this part of information can be safely stored in the confidential storage component, and through the zero-trust runtime function, such data can be safely removed for the target service.

## Product Value

### Security Challenges

In the construction of the ZeroData platform, there are many security problems and difficulties that need to be broken through:

- **The security vendor report shows that a large number of databases contain CVE vulnerabilities.**：In its research, Imperva, a network security company, shows that nearly half of the database it scans contains CVE vulnerabilities. Unauthorized access by malicious persons may cause data leakage and permanent loss.
- **Network location-based gateway and firewall security policies are not reliable.**：Network location does not mean trust. In this way, as long as the outermost barrier is broken, all data will lose the security barrier. And with the cloud native process, the network environment is becoming more and more complex. Therefore, verification must be carried out in a zero-trust manner.
- **Connection-based authorized access is too granular.**：Even if the initiator is verified before accepting the connection, ensure that it is a connection initiated by a legal user. There is still no guarantee that the resources it access does not exceed its due authorization. Therefore, it is necessary to adopt the principle of minimum privilege and separately evaluate the trust of the requester for each resource access.
- **It is difficult to reach the system security status assessment.**：There must be enough telemetry data records and analysis to support the security assessment of the current system. And provide visual panels or tools as much as possible to visualize the current security status of the system.
- **User authentication is usually dynamic.**：Permissions and policies are usually dynamically regulated and need to be strictly verified before access is allowed. This is a cycle of continuous access, scanning, threat assessment, updating policies, and continuous verification.

### Core Advantages

**Netfoundry** covers both ends of the database connection through agents and private structure agents. Strong identification, authentication and authorization can be completed without the help of the firewall.

Based on supporting zero trust and private structure agents, our solution can conveniently control and visualize the strategy through the platform.

**Oracle** proposes a zero-trust security model to protect user data from the perspective of attack prevention, detection of attack intention, intrusion remediation, time analysis, etc.

Our solution fully supports zero-trust functions and adapts to complex cloud native environments:

- **Identify security vulnerabilities** - Centralize security operations through the platform to improve visibility. Record and analyze data access behaviors, and provide risk warning and after-post analysis support.
- **Protection attack** - Privatization agents prevent database public network exposure; the data surface is fine-grained and authentication, and real-time perception of security policy changes is protected.
- **Data encryption protection** - Sensitive information is confidentially stored in confidential storage components, the platform provides policy control, and zero trust provides data security assurance.
- **Risk reduction** - Use safety first design principles to reduce the risk from persistent threats. The use of technologies such as minimum access can also help comply with compliance and privacy regulations. By managing good identities, organizations can better control user access, thus reducing the risk of internal and external violations.

### Sustainable Development

With the increasing use of cloud services, more security problems will be exposed. With security problems in urgent need of protection, there will also be more competitors thinking about database security access, and there will be more database access security methods. This requires us to put forward our own unique advantages, unique zero-trust database security in the general environment, and constantly innovate.

Organizations adjusted from a standard peripheral security method to a zero-trust model can take advantage of automation, security and governance to enhance their overall competitive advantage and business agility, thus improving their competitive advantage.

The following is our actual progress and the next road map, as well as continuous support for the development of Zero Data:

- 2022.10 Increase zero-trust PKI construction, including CA and OCSP services
- 2022.11 Increase the privatization agency structure and its control function
- 2022.12 The functions of authorization and verification are perfect, including data surface functions and control surface functions.
- 2023.02 Rich observability data collection and automated data analysis construction
- 2023.04 Open source the management platform and provide a panel for managing data.
- 2023.05 Data protection support for more database systems
- 2023.07 Perfect use and management functions of confidential information
- 2023.10 The zero-trust platform has rich continuous monitoring functions and establishes an early warning system for high-risk behaviors.
- 2023.12 Construction of functional modules for safety investigation, abnormal detection and compliance evidence

## Team Strengths

We are not fighting, but a group of people fighting for zero trust security, database security, and Zero Trust.

In the future, in accordance with our plan, we will continue to improve the development of database access security, community participation rules and advanced rules, improve developer documents, and lower the threshold for developer participation and increase the honor of developer participation. Create a runtime data confidentiality system based on zero trust in a mature cloud native environment.