# MH-Vendor-Management-System
Vendor Management
Flow:
The project begins by designing the database. Based on the requirements, the Entity-RelationshipDiagram (ERD) is created to visualize all the entities, attributes, and their relationships. The focus hereisto ensure a normalized database structure to avoid redundancy while maintaining referential integrity. Once the ERD is finalized, it is translated into a relational schema, outlining the tables, their columns, primary keys, and foreign key constraints. Each table is meticulously designed to ensure it aligns withtheproject's needs. Following the design phase, the database implementation is carried out using MySQL. ADDLscript iswritten to create the tables, with all necessary constraints such as primary keys to uniquely identifyrecords and foreign keys to establish relationships between related tables. This step ensures that thedatabase adheres to all integrity constraints from the outset. Additionally, stored procedures are writtentohandle frequently executed operations, such as inserting and updating records, while triggers areimplemented to automate specific database behaviors, like logging changes or enforcing business rules. The backend development phase involves setting up a Node.js server using the Express framework. Thebackend is connected to the MySQL database using a MySQL library such as mysql2. Routes andcontrollers are defined to handle API endpoints, allowing data to be inserted into or retrieved fromthedatabase. CRUD operations are implemented through these endpoints, and error handling is includedtoensure robust functionality. The project’s frontend is developed with a focus on user experience. Pages are created using HTML, JavaScript, and Bootstrap for responsive design, with additional visualizations created using SVGandD3.js for interactivity. Inline CSS is used for minor customizations, ensuring a balance between styleandperformance. Forms are designed for data input, allowing users to interact seamlessly. Finally, the integration and deployment phase ensures that all components work together smoothly. TheNode.js server communicates effectively with the MySQL database, while the frontend interfaces providean intuitive user experience. The application is thoroughly tested for bugs and performance issues. Thisstructured workflow ensures a robust, efficient, and user-friendly application, integrating a database witha dynamic web interface.

Constraint:
Vendors Table:
1. Primary Key: VendorID ensures each vendor has a unique identifier. 2. Not Null: VendorName and Email cannot be left blank. 3. Data Type Lengths:
1. VendorName: Maximum of 255 characters. 2. Email: Maximum of 255 characters. 3. Phone: Maximum of 20 characters. Contracts Table:
1. Primary Key: ContractID ensures each contract is unique. 2. Foreign Key: VendorID references Vendors(VendorID):
1. On Delete Cascade: Automatically deletes related contracts if a vendor isremoved. 3. Not Null:
1. StartDate and EndDate must have valid dates. 2. Status must always have a value. PurchaseOrders Table:
4. Primary Key: PurchaseOrderID ensures each purchase order is unique. 5. Foreign Keys:
1. DepartmentID references Departments(DepartmentID):
1. On Delete Cascade: Deletes related purchase orders if a department isremoved. 2. VendorID references Vendors(VendorID):
1. On Delete Cascade: Deletes related purchase orders if a vendor isremoved. 6. Not Null:
1. ItemDetails, Quantity, TotalCost, and Status are required. 7. Data Range Check:
1. TotalCost: Must be a positive value greater than or equal to 0. Roles Table:
8. Primary Key: RoleID ensures each role is unique. 9. Unique Constraint: RoleName prevents duplicate role names. 10. Not Null: RoleName cannot be blank. Departments Table:
11. Primary Key: DepartmentID ensures each department is unique. 12. Foreign Key: RoleID references Roles(RoleID):
1. On Delete Cascade: Deletes departments if the associated role is removed. 13. Not Null: DepartmentName is mandatory. Budgets Table:
14. Primary Key: BudgetID ensures each budget entry is unique. 15. Foreign Key: DepartmentID references Departments(DepartmentID):
1. On Delete Cascade: Deletes budgets if the associated department is removed. 16. Not Null: AllocatedBudget and UsedBudget are required. 17. Data Range Check:
1. AllocatedBudget and UsedBudget: Must be positive values greater than or equal
to 0. Users Table:
18. Primary Key: UserID ensures each user is unique. 19. Unique Constraint: Username prevents duplicate usernames. 20. Not Null:
1. Username, Password, Role, and DepartmentID are required. 21. Foreign Key: DepartmentID references Departments(DepartmentID):
1. On Delete Cascade: Deletes users if the associated department is removed. VendorPerformance Table:
22. Primary Key: PerformanceID ensures each performance record is unique. 23. Foreign Key: VendorID references Vendors(VendorID):
1. On Delete Cascade: Deletes performance records if a vendor is removed. 24. Not Null:
1. Rating and EvaluationDate are mandatory. 25. Data Range Check:
1. Rating: Must be between 0 and 5 (inclusive). Notifications Table:
26. Primary Key: NotificationID ensures each notification is unique. 27. Foreign Keys:
1. UserID references Users(UserID):
1. On Delete Cascade: Deletes notifications if a user is removed. 2. ContractID references Contracts(ContractID):
1. On Delete Cascade: Deletes notifications if a contract is removed. 28. Not Null:
1. Message and Date are required. BudgetMessages Table:
29. Primary Key: MessageID ensures each message is unique. 30. Foreign Key: ContractID references Contracts(ContractID):
1. No Action: Does not delete messages if a contract is removed. 31. Default Values:
1. CreatedAt: Defaults to the current timestamp if not explicitly provided. 32. Data Range Check:
1. TotalCost and BudgetRemaining: Must be positive values greater than or equal to0. Assumptions:
In the design and implementation of the vendor management system, we made several
assumptions to ensure its functionality and alignment with organizational requirements. Theseassumptions shaped the database structure, system functionality, and the role of the administrator:
Administrator's Role and Authority
Single Administrator Oversight: We assumed the system would be managed bya singleadministrator who will have unrestricted access to all functionalities and operations of thesystem. 1. The administrator will oversee vendor management, contract renewals, department budgets, and purchase orders. 2. They will have the authority to modify the database, including addingnewvendors, updating vendor details, and renewing or terminating contracts. Comprehensive Access and Analytics: The administrator will have access to detailedanalytics and performance metrics to:
1. Evaluate vendor performance. 2. Monitor contract statuses. 3. Ensure efficient resource allocation and compliance with budgets. Centralized Management: The centralized role of the administrator ensures the integrityof the system and allows for quick adaptation to changes, such as updating termsorresolving conflicts. Database Assumptions and Structure
Key Database Entities: The system is built around the following key entities:
1. Vendors: Contains vendor details such as contact information, service categories, certifications, and performance metrics. 2. Contracts: Stores contract details including terms, vendor associations, andstatuses.
3. Departments: Represents organizational departments with associatedbudgetsand roles. 4. Purchase Orders: Tracks transactions between departments and vendors. 5. Budgets: Maintains allocated and used budgets for departments. 6. Users: Stores login credentials and roles of system users. 7. Vendor Performance: Captures performance ratings and feedback for vendors. 8. Notifications: Sends automated alerts, such as contract renewal reminders. 9. Budget Messages: Provides alerts when a department exceeds its allocatedbudget. Foreign Key Dependencies:
1. Vendors are linked to contracts and purchase orders to ensure vendor-specificdata integrity. 2. Departments are linked to budgets and users to maintain a structuredrelationship between roles, budgets, and departmental activities. 3. Notifications and messages are tied to specific contracts, users, and departmentsto provide targeted insights. Triggers and Automation:
1. A trigger alerts users when a contract's end date is approaching. 2. A trigger monitors department budgets and sends warnings if they are exceeded. Stored Procedures:
1. RegisterVendor: Adds a new vendor to the system. 2. UpdateContractStatus: Updates the status of a contract. 3. EvaluateVendorPerformance: Records performance ratings and feedbackfor
vendors.

Overall Design Philosophy
The design aims to centralize and streamline vendor management while enabling flexibilityinupdates and modifications. By granting the administrator comprehensive control, we ensurethat
the system operates efficiently while providing insights and alerts to preempt potential issues. This setup supports scalability and adaptability, making the system robust for dynamic businessenvironments.
