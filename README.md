










 	Functional Specification – Conversion

	Business Transformation Program 
	May 28, 2026











 
RICEFW ID	C-102  
RICEFW Summary	F.Spec for Portfolio Item
Project Name	Irving Oil Limited (IOL) - Business Transformation Program (BTP)  
Stream	D2B
Document Version	1.0
Document Status	<: Draft, In Progress, In Review, Completed> 
Date Released	2026-04-13

Document Control
Sprint	Requirement/ GAP/ CR ID	Version	Author	Description	Date
S1	C-102	0.1	Portfolio Items	Imane El-Amrani	Apr 13, 2026

Document Review
Organization	Role	Name / Email	Comment	Date
Deloitte	D2B Lead	Myat Lin		yyyy-mm-dd
Deloitte	Data Lead	Jaspreet Singh		yyyy-mm-dd
				

Review & Sign-Off
Organization	Role	Name / Email	Signature	Date
Irving Oil	D2B-EPPM Lead  	Peter Van Kessel		2026-04-20
				
				

Change Control
Version	Requirement/ GAP/ CR ID	Author	Description of change	Reviewed By	Approved By	Date
0.1	C-102	Imane El-Amrani	Initial			Apr 13, 2026


Table of Contents
1	Executive Summary	6
1.1	Requirement Overview	7
1.1.1	Key Decisions (Business Rules)	7
1.2	Impacted Systems	7
1.3	Dependencies	8
1.3.1	Environment / Configuration Dependencies	8
1.3.2	Development Dependencies	8
1.3.3	Run/Execution Dependencies	8
1.4	Open Items/Assumptions (Extract)	8
1.5	Open Items/Assumptions (Load)	9
2	Data Extraction Requirements	10
2.1	Source System Inventory	10
2.2	Scope, Selection Criteria & Filtering Requirement	12
2.3	Expected Extraction Volume	14
2.4	Data Construction Process	14
2.4.1	Manual construction Approach and Manual Template Location	14
2.5	Manual Template Location and File Format	14
2.6	Data cleansing Strategy	15
2.7	Delta Extraction	15
3	Data Transformation and Loading Requirements	16
3.1	Mapping, Validation and Transformation Rules	16
3.2	Selection Screen requirement for load program	17
3.3	Transaction Information	17
3.4	Transaction Code	17
3.5	Expected Load Volume	22
3.6	Error Handling, Correction and Recovery	22
3.7	Guidelines for partial processing of errors	23
3.8	Notification of Errors:	23
3.9	Error log/Audit log/Error Reports:	23
3.10	Re-run Requirements	24
4	Post Load Validation and Reconciliation	25
4.1	Post Load Data Validation	25
4.2	Reconciliation Requirements	25
5	Security and Controls	25
5.1	Security Requirements	26
6	Testing Requirements	26
6.1	Test Data	26
6.2	Test Cases	26
7	Additional Information	28

 
1	Executive Summary
This Functional Design Document outlines the requirements, scope, and initial design for the Portfolio Items conversion as part of the SAP S/4HANA implementation. It defines how existing portfolio items from the legacy portfolio management solutions will be converted and transitioned into SAP S/4HANA Portfolio and Project Management (PPM/EPPM), ensuring alignment with SAP’s standardized portfolio item model, governance framework, and financial planning capabilities.
In SAP S/4HANA, Portfolio Items represent planned or active ideas that carry scope, schedule, and financials. They are the backbone for investment categorization, prioritization, and executive decision making across portfolios and buckets. Converting legacy portfolio items—including their master data, hierarchical relationships, and key financial attributes—is a foundational prerequisite to ensure that projects are accurately classified, governed, and reported in the target system.
The conversion will also incorporate financial planning for each portfolio item, specifically migrating estimated costs and approved costs so that budget allocation, approvals, and expenditure tracking continue seamlessly in SAP S/4HANA. This includes mapping legacy financial fields to S/4HANA PPM structures and controls, enabling ongoing financial oversight and robust analysis within the portfolio management framework.
This document describes:
•	The business scenarios in which portfolio items are used including strategic investment planning, intake and prioritization, funding approval, and executive reporting.
•	The functional requirements for converting legacy portfolio item attributes into SAP S/4HANA PPM (e.g., identifiers, descriptions, statuses, categorizations, sponsors/owners, and structural relationships to portfolios/buckets).
•	The handling of portfolio hierarchies and relationships, including assignment of items to portfolios/buckets and linkages to downstream execution objects where applicable.
•	The migration and mapping of financials at the item level, including estimated and approved costs, to ensure accurate allocation, auditability, and ongoing budget tracking within SAP S/4HANA.
•	The high level mapping, transformation, validation, and reconciliation logic required to ensure data integrity, structural consistency, and compliance with SAP S/4HANA Portfolio Management standards.
The Portfolio Items conversion design ensures that:
•	All in scope portfolio items are available in SAP S/4HANA with correct portfolio/bucket assignment, classification, descriptive attributes, and status.
•	Existing prioritization and categorization logic is preserved to maintain continuity of reporting, governance, and decision making.
•	Financial attributes (notably estimated and approved costs) are migrated accurately with clear lineage, enabling consistent planning, approvals, and performance tracking post go live.
1.1	Requirement Overview
1.1.1	Key Decisions (Business Rules)
In Scope:
•	Migration of active Portfolio Items master data
•	Migration of portfolio item data
o	General Information
o	Decision Points & Active statuses
o	Portfolio Item active statuses
o	Relationships
o	Related Objects
•	Migration of portfolio item Financial Data
o	Portfolio Item financial data
o	Project Estimate (Project Ask)

Out Of Scope:
•	Migration of inactive or obsolete Ideas

Business Rules (Functional):
•	The portfolio item represents the final level of the portfolio structure and serves as the connection between Project Portfolio Management (PPM) and Project System (PS).
•	For legacy portfolio items, projects will not be created automatically, they will be manually mapped to their respective projects migrated during the C-103 conversion.
Program Rules (Functional):
•	All portfolio items must be created in compliance with the configured portfolio items defined in SAP S/4HANA.
•	Each portfolio item must be assigned to a Bucket (Program) that exists in SAP S/4HANA prior to portfolio items creation.

1.2	Impacted Systems 
Impacted Systems 
Data Source (s):	Oracle Projects, OnePlan, Excel (SMO, Env. Projects), MS Accelerator, MS Access (PS Cost and TA Cost Database)
Data Target (s):	S/4HANA PPM Module
Other Tools: (e.g. staging tools etc.)  	Custom Program
1.3	Dependencies
1.3.1	Environment / Configuration Dependencies
A.	Portfolio Item Settings

o	Portfolio Item types
o	Portfolio item statuses
o	Portfolio decision point statuses
B.	Financial Planning Settings

o	Financial Views
o	Financial Categories
o	Financial Groups
o	Period Type
o	Front end setting for view Category and groups


1.3.2	Development Dependencies
List the configuration, development, and other work that must be considered during the development of this object.
Sprint	Requirement / Gap ID	Object Type	Details
0	E-015	Enhancement	Additional Management attributes 

1.3.3	Run/Execution Dependencies
Once in production, this development object may need to be executed before or after another system event.  List other system events that this development object should follow or precede.
Relationship	Requirement / Gap ID	Object Type	Details
Follow	C-101	Conversion	Conversion Program for Buckets 
Follow	C-103	Conversion	Conversion Program for Projects
1.4	Open Items/Assumptions (Extract)
List of assumptions on which this design is dependent.  This might also include a list of business factors which make creating this development a requirement. Update below table for Open items if applicable
Date Opened	Description	Assigned To	Due Date	Status
2026-04-03	Only active ideas from the legacy Oracle system are in scope; inactive or obsolete ideas are intentionally excluded.
	Peter Van Kessel	FUT	Open
2026-04-03	Legacy project ideas master data are complete, accurate, and business approved prior to extraction.
	Peter Van Kessel	FUT	Open
2026-04-03	Historical project financial planning data will be reviewed and validated by business stakeholders prior to migration to SAP S/4HANA PPM.	Peter Van Kessel	FUT	Open
2026-04-16	The data conversion approach (autonomous legacy data or manual conversion) is subject to final decision by Business
 	Peter Van Kessel	2026-04-20	Closed
1.5	Open Items/Assumptions (Load)
List of assumptions on which design is dependent.  This might also include a list of business factors which make creating this development a requirement. Update the table below for Open items if applicable.
Date and time of data extraction from the source system will be coordinated with source IT and Business Owners.
•	Post load data validation is the responsibility of the D2B stream.
•	For any new data, the mutually compatible data present at the time of the data freeze that is to be copied or loaded onto SAP S/4 HANA will be taken as it stands at that point in time. Data cleansing activities are currently performed in advance of this date at the discretion of the functional teams.
•	Before the data is loaded, D2B must approve the preload validation.

Date Opened	Description	Assigned To	Due Date	Status
2026-04-03	Portfolio item and financial planning configuration are fully configured and validated in SAP S/4HANA PPM prior to load execution.
	Imane El-Amrani	2026-06-30	Open
2026-04-03	Ideas naming conventions and classifications are finalized and approved by the business before load.
	Peter Van Kessel	2026-06-30	Open
2026-04-03	Legacy descriptions must be reviewed and adjusted to ensure they comply with SAP S/4HANA's character limit requirements.	Imane El-Amrani	2026-06-30	Open
2026-04-03	Financial planning data for all ideas will be available and validated in the required format prior to data load activities.	Peter Van Kessel	2026-06-30	Open
2026-04-14	Project conversion should be completed prior to portfolio item conversion, and IDs must be aligned to ensure a proper link between the two.	Imane El-Amrani	2026-06-30	Open

2	Data Extraction Requirements 
The following sections outline the data extraction and staging requirements for the conversion object. 
Define Data Migration Scope
•	The extraction design shall identify the project ideas to be migrated.
•	Extract the relevant master from Oracle Portfolio.
•	And combine them with approved supplemental Excel, OneSource and Excel sources. 
•	Extraction outputs must preserve record lineage, extract timestamp, source system indicator, and key business identifiers to support reconciliation and reprocessing. 
Perform Data Cleansing Before Extraction
Comprehensive data quality checks must be completed on legacy project ideas data prior to extraction to ensure accurate and controlled migration into SAP S/4HANA. The following cleansing activities are required: 
•	Identify and remove duplicate or redundant project ideas master records. 
•	Correct missing, invalid, or inconsistent attributes (e.g., ID responsible, Start date). 
•	Review and exclude inactive project ideas that are out of scope, unless required for statutory, audit, or reporting purposes. 

2.1	Source System Inventory
List the source applications, and if possible, related screens, transactions, and if you know, the computer system that it runs on.
Source System	Name	Functionality	Business Organization Usage
Oracle Projects	Legacy Project Management System
 	Serves as the system of record for project structure management and financial activities, supporting the day-to-day operations of the Project Management and Finance teams.
 	Used by Irving Oil (Enterprise) Project Management and Finance teams to manage project lifecycles, oversee financial transactions, track progress, and ensure proper governance of projects throughout the organization.
 
Oneplan	Legacy Growth Project Management System 
 	Serves as the system of record for Corporate Growth projects. 	Intake new project ideas, route them for approval, plan project budgets, manage forecasts, record actuals, generate governance reporting, and record benefits.  Reflects (manually) data from Oracle Projects, Primavera P6, and stand-alone spreadsheets.  It also uses Power BI to generate reports.
Excel (SMO)	Legacy Network Development Project Management System	Serves as the system of record for Sales and Marketing Network Development Projects.	Define project level budgets, update forecasts, record actuals, and report against project progress.  Contains simple schedules.  Reflects (manually) data from Oracle Projects.
 
Excel (Env. Projects)	Legacy Environmental Project Management System	Serves as the system of record for Environmental Remediation Projects	Track vendor costs against project budgets and scopes of work.
MS Accelerator	Legacy IT Project Management System  	Serves as the current system of record for IT Projects. 	Intake new project ideas, plan project budgets, manage forecasts, record actuals, and generate governance reporting.  Reflects (manually) data from Oracle Projects.  Provides a view fo schedule in MS Planner via Power BI. 
MS Access (TA Cost Database)	Legacy Turnaround Cost Management System	Serves as the system of record for Saint John Refinery Turnaround Projects and maintenance work.	Decomposes budgets into lower-level control accounts.  Provides forecast and change management functionality.  Used to generate cost reports (monthly).  Reflects (manually) data from Oracle Projects.  
MS Access (PS COST)	Legacy Sustaining Capital Cost Management System	Serves as the system of record for Saint John Refinery Sustaining Capital Projects.	Decomposes budgets into lower-level control accounts.  Provides forecast and change management functionality.  Used to generate cost reports (monthly).  Reflects (manually) data from Oracle Projects and Primavera P6.  
Table 1 – Source System Purpose, Functionality and Business Units Usage

Source System	Data Owner Contact Info	Data Owner Contact Info	IT Representative Contact Info
Oracle Project Management
& MS Access	Saint John Refinery Capital Projects
Rob Roy	Rob.roy@irvingoil.com
Mary Ryan
MS Access	Saint John Refinery Turnaround Projects
Brian Bruno	Brian.bruno@irvingoil.com
Mary Ryan

Oneplan	Corporate Growth Projects
Lee-Ann Wicks	Lee-ann.wicks@irvingoil.com
Mary Ryan

Excel	Sales and Marketing, Network Development Projects
Tracy Mitchell	Tracy.mitchell@irvingoil.com
Mary Ryan

MS Accelerator	Information Technology Projects
Paula Brinston	Paula.brinston@irvingoil.com
Mary Ryan

Excel	Real Estate
Melissa McLeod	Melissa.macleod@irvingoil.com 
Mary Ryan

Table 2 - Source System Contacts
2.2	Scope, Selection Criteria & Filtering Requirement
The approved PMC decision document defining the standard conversion scope and selection criteria for WBS (Work Breakdown Structure) master and transactional data objects shall be referenced and attached. Any deviations from the standard PMC-approved scope must be explicitly documented in this section.
The approved PMC decision document defining the standard conversion scope and selection criteria for portfolio item master and financial data. Any deviations from the standard PMC-approved scope must be explicitly documented in this section.
Scope of Portfolio Item Conversion
•	Portfolio Item Master Data
•	Portfolio Item Status Information
•	Portfolio Item Relationship
•	Portfolio Item Financial Data
•	Portfolio Item Related Objects
Portfolio Item Categories Included in Scope
The following portfolio item categories are included in the migration scope:
•	Active portfolio items
•	Portfolio items linked to ongoing projects
•	Portfolio items with open financial transactions (Estimate or approved cost)
•	Portfolio items with activity within the defined legacy period (2 years)
Portfolio Item Selection Criteria
Portfolio item master records will be selected for migration based on predefined business rules.
•	Portfolio items assigned to active programs
•	Portfolio items required for compliance or statutory reporting
These criteria ensure that only relevant and operational portfolio item data is migrated to the target system.
Data Filtering Rules
Data filtering will be applied during the extraction phase to remove unnecessary records.
•	Exclude portfolio items with no activity in the last defined period 
•	Exclude portfolio items flagged as deleted or blocked in the legacy system unless required
•	Exclude duplicate or redundant portfolio item records identified during data cleansing
•	Exclude portfolio items assigned to inactive or obsolete programs
•	Exclude portfolio items with incomplete mandatory master data fields
Mandatory Data Validation Requirements
Before migration, the following fields must be validated to ensure successful loading into the target system:
•	Portfolio item ID
•	Portfolio item description
•	Status (active, released, closed)
•	Responsible person/owner
•	Project association
Records failing validation checks will be corrected before migration.
Data Cleansing and Harmonization
Prior to migration, portfolio item master data will undergo cleansing and standardization activities including:
•	Removal of duplicate portfolio item records
•	Standardization of portfolio item codes and descriptions
•	Standardization of portfolio item status and classifications
•	Correction of incomplete or inconsistent master data fields
This ensures data consistency and quality in the target system.
2.3	Expected Extraction Volume
Specify the data volume that extraction programs will have to work with
Source System	Data Volume  
Oracle Projects	2000 projects x 2 years
Oneplan	50 projects x 2 years
Excel (SMO)	600 projects x 2 years
Excel (Env. Projects)	100 projects x 2 years
MS Accelerator	20 projects x 2 years
MS Access (PS COST)	300 projects x 2 years
MS Access (TA Cost Database)	600 projects x 2 years
2.4	Data Construction Process
2.4.1	Manual construction Approach and Manual Template Location
Data construction will be manual   (instead of source extraction) as there are multiple source systems currently and there needs to be transformation of data to standardize across the business unit. Data in the TUT and FUT can be reflective of a sample size of the full set of data that will be covered in the Mock Data Conversion process.



BU/ Country	Own data quality review, approve supplemental records, sign off on exceptions 
Build	
Design	
Data Quality	Profile data, identify duplicates/invalid attributes, manage cleansing tracker 
Project Team	Prepare mapping, coordinate extracts, execute mock loads, manage issue log 
Solution Build	Prepare staging logic, load files/programs, logs, and reconciliation outputs
2.5	Manual Template Location and File Format
This Functional Spec will create the conversion program to data for the projects into S/4HANA while the S/4-load-ready file will be prepared by the D2B functional team.
Below is the load template file for Portfolio items:
C-102_Portfolio Items_Load_Template.xlsx    

Note:
•	The load template file should be enhanced     to accommodate the custom fields for the Portfolio Items. 
•	All the date fields in the template should be in the given format (YYYYMMDD).


2.6	Data cleansing Strategy
Source data cleansing to be carried out by business  , with the data profiling rules outlined in previous communication as this will be a manual construction instead of a direct source-to-target extract.
2.7	Delta Extraction
The recommended approach is an initial full load of all Portfolio Items master data, which may be executed through multiple processing runs and re runs to address validation errors and data corrections. Records failing validation will be logged, corrected by the business, and reprocessed in subsequent runs until the full data set is successfully loaded.
 
3	Data Transformation and Loading Requirements
A custom program is to be developed to create projects and update the attributes of Portfolio Items in S/4 HANA. RPM_DX_ITEM can be enhanced for developing the custom program for Portfolio Items migration.
3.1	Mapping, Validation and Transformation Rules

Portfolio Item Mapping Sheet Conversion.xlsx 
Sample inbound conversion file (if available)
☐Yes	 (Embed attachment here) 		☒No
N/A as the mapping rules are not needed for this functional specification. There will be parallel activity by functional team to map out source/legacy to target fields in the same load template linked above.
The Business will be responsible for identifying source systems, extracting, mapping, and cleansing the source data. The Functional team will be responsible for populating the load file generated by this custom load program, using business prepared data, and will follow the steps below:
1.	Source systems are identified by the Business (Section 2.1)
2.	Data is extracted from the source systems by the Business
3.	Source to target mapping and data cleansing are performed by the Business, including: 
o	Ensuring source data complies with SAP constraints (e.g. source ID description mapped to a target SAP field with a 40 character limit)
4.	The Functional team validates and applies the business provided mappings to the SAP target structure
5.	The Functional team generates the final load file output for handoff to the Data team


3.2	Selection Screen requirement for load program
Selection screen should be as per the conversion strategy. If yes, please mention the same. If not, then please mention the selection screen requirements below. To be filled up if load option as per conversion strategy is ABAP Load.
Field Title/Screen Label	Type	Size	Mandatory	Range Required	Reference Field Name	Validation Criteria
Execution Mode	CHAR	1	Yes	No	–	Allowed values: T (Test Run) / L (Live Run).
Input File Path	Path	255	Yes	No	–	Path must exist on application server and be readable by SAP.
Execute
	PUSHBUTTON
	–	Yes	No	–	Triggers program execution based on selected parameters after validation.


3.3	Transaction Information 
N/A
3.4	Transaction Code 

Select the bucket and Item type as shown in the below screen
 

Transaction Code: 	
Name of Transaction: 	Portfolio Items
Name of First Screen: 	General Information Screen
Fill the necessary information
 
Save the details
 

First screen fields details
Field Description	SAP Field Name	Technical Field Name	Table (if known)	Type	Example Value
Name			/RPM/ITEM_D	Text	
Portoflio Item ID	ID	EXTERNAL_ID	/RPM/ITEM_D	Alpha-Numeric	CX-1000007
Status	Status	STATUS 	/RPM/ITEM_D	Text	Active 
Type 	Type	ITEM_TYPE 	/RPM/ITEM_D	Text 	Capital Project 
Priority	Priority	PRIORITY_GROUP	/RPM/ITEM_D	Selection	High
Forecast Start and Finish Dates	PORTFOLIO_ITEM_FORECAST_DATES 	FORECAST_START, FORECAST_FINISH	/RPM/ITEM_D	Date 	04/01/2026 - 09/30/2026 
Planned Start and Finish Dates	PORTFOLIO_ITEM_PLANNED_DATES 	PLANNED_START, PLANNED_FINISH 	/RPM/ITEM_D	Date 	03/01/2026 - 08/31/2026 
Project Manager 	Project Manager 		/RPM/ITEM_D	Numeric 	
Project Controller 	Project Controller 		/RPM/ITEM_D	Numeric 	
Portfolio Manager 	Portfolio Manager 		/RPM/ITEM_D	Numeric 	
Project Sponsor 	Project Sponsor 		/RPM/ITEM_D	Numeric 	

Name of Second Screen: 	Phases and Decisions 

This phase is the formal mechanism by which the project approval is granted, enabling the item to advance within the project management process. 

 
Field Description	SAP Field Name	Technical Field Name	Table (if known)	Type	Example Value
Name	Name	DECISION_NAME 	/RPM/DECISION	Text 	
ID	ID	DECISION_ID	/RPM/DECISION	Numeric	00001
Status	Status	STATUS	/RPM/DECISION	Text	Active 
Forecast Start and Finish Dates	Forecastd Start,Forecast Finish 	FORECAST_START, FORECAST_FINISH 	/RPM/DECISION	Date 	04/01/2026 - 09/30/2026 
Actual Start & Finish Dates	Actual Start, Actual Finish	ACTUAL_START, ACTUAL_FINISH	/RPM/DECISION	Date 	
Planned Start & Finish Dates	Planned Start, Planned Finish 	PLAN_START, PLAN_FINISH	/RPM/DECISION	Date 	
Forecast Decision Date	Forecaste DecisionDt	DECISION_DATE	/RPM/DECISION	Date 	
Planned Decision Date	Planned DecisionDate	PLANNED_DEC_DATE	/RPM/DECISION	Date 	
Actual Decision Date	Actual Decision Date	ACTUAL_DEC_DATE	/RPM/DECISION	Date	
 
Name of Third Screen: 	Relationship

The Relationship screen allows us to establish links between multiple portfolio items, creating dependencies or associations as needed. By connecting these items, we can better coordinate project timelines, resource allocations, and decision points, ensuring that changes in one portfolio item are reflected and managed across related items. 
 

Third screen fields details 
Field Description	SAP Field Name	Technical Field Name	Table (if known)	Type	Example Value
Dependency ID	Dependency ID			Text 	10001 
Dependency Name	Dependency Name			Numeric	TA Dependency 0001 
Determining Item ID	Determining Item ID			Numeric	20002 
Determining Item Name	Determining Item Name			Text	20003 
Planned start	Planned start			Date 	2026-04-14 
Planned finish	Planned finish			Date 	2026-06-30 
Dependency Type	Type			Text	Finish-to-Start 
Risk	Risk			Text 	
Risk Status	Risk Status			Text	
 


Name of Fourth Screen: 	Financial Information

 

Update Estimate (Project Ask)
 
Update Estimate (Project Ask)

 
Data saved
 
Field Description	SAP Field Name	Technical Field Name	Table (if known)	Type	Example Value
Financial view	Financial view	PLAN_TYPE	/RPM/V_FIN_PLAN	Text	Estimates (Project Ask)

Financial Category	Financial Category	CATEGORY	/RPM/ FIN_CATG	Text	
Financial Group	Financial Group		/RPM/ FIN_CATG	Text	Amount
Currency	Currency	CURRENCY	/RPM/V_FIN_PLAN	Text	CAD
Amount	Amount	AMOUNT	/RPM/V_FIN_PLAN	Numeric	60000


Name of Fifth Screen: 	Related Objects

 
Field Description	SAP Field Name	Technical Field Name	Table (if known)	Type	Example Value
Type of related Object	Group			Text	Project Definition

Object Description	Object Name			Text	Turnaround Project 000001
Object ID	Object Number			Text	TA.0000001

3.5	Expected Load Volume
Source System	Data Volume 
Oracle Projects	2000 projects x 2 years
Oneplan	50 projects x 2 years
Excel (SMO)	600 projects x 2 years
Excel (Env. Projects)	100 projects x 2 years
MS Accelerator	20 projects x 2 years
MS Access (PS COST)	300 projects x 2 years
MS Access (TA Cost Database)	600 projects x 2 years
3.6	Error Handling, Correction and Recovery
•	Each run must generate a control report showing total input records, successfully loaded records, rejected records, and any document numbers created. 
•	Errors shall be classified as master-data errors, mapping/configuration errors, file/format errors, or system/technical errors. 
•	Rejected records must include sufficient detail to enable correction (source file, row number, legacy asset number, company code, error text, and failed validation rule). 
•	No manual edits are permitted directly in the staged load files after technical run start; corrections must be made in the controlled source/staging file and reloaded through the approved process. 
•	Recovery steps must preserve audit trail and clearly distinguish original run ID versus rerun ID. 

3.7	Guidelines for partial processing of errors
Allow partial entries		 	☐Yes			☒No
Allow partial run 			☒Yes			☐No
There will be no partial creation of Portfolio Items. However, partial processing runs will be allowed in the event errors are encountered, in order to avoid blocking the overall process. Records with incorrect or invalid values will be skipped and reported to the business for correction, while valid records will continue to be processed. 
This will be dependent on the Technical Specifications and finalized based on recommendations during build of program.  
 Link to the KDD for Data Refresh Approach:
IOL BTP KDD_RAID-822- Data Refresh Approach for mock cycles.docx

3.8	Notification of Errors:
•	Master data errors: notify conversion lead, data quality lead, and relevant business data owner with run ID, source record, and error detail. 
•	Configuration/data validation errors: notify D2B functional lead and technical lead for resolution of mapping/configuration or control-table issues. 
•	System/technical errors: notify SAP technical/support team immediately with log reference, background job details, and file/run context. 
•	Escalation should follow project cutover governance if unresolved within the agreed window for the dress rehearsal or production run. 

3.9	Error log/Audit log/Error Reports:
•	Pre-load validation report: duplicates, missing mandatory fields, invalid mappings, and control-total variances. 
•	Load execution report counts by company code/source/run ID, successful loads, rejected loads, and created Portfolio Items numbers.
•	Post-load reconciliation report: source Portfolio Item target totals by bucket. 
•	Audit report: source file version, load date-time, executor, run ID, and retained legacy key mapping. 

3.10	Re-run Requirements
Re-run should normally process only rejected/unprocessed records after corrections, using the same approved source baseline and a new run ID, unless business and technical teams determine that a full rollback and full-file rerun is required. The rerun approach must preserve traceability between the original and subsequent runs. 
4	Post Load Validation and Reconciliation
4.1	Post Load Data Validation
After Actual Loading in S/4HANA, comparison between pre-load signed-off data fields and S/4HANA extracted fields to be done. Pre-load signed-off data is expected to match field by field to loaded data.
Post-load Report consists of the following:
•	Post load file: Comparison of Pre-load table fields and S/4HANA loaded table fields and Match columns which will determine if the two tables/fields are matching (YES/NO – based on Match/Mismatch). This file will have the same structure/fields as the mapping sheet.
•	Post load error report: Error report explaining the reason for invalid records during the load process.
•	Post load Summary: Summary count such as total number of extracted data, transformed data, and loaded data including number of successful records.
Business Post load validation in S/4HANA:
The following are the recommended SAP transactions, tables and/or SAP reports that can be used to validate the load of this data in S/4HANA (GUI and/or FIORI):
Transaction Code/Fiori APP	SAP Table	Description	Logic
Portfolio Items	/RPM/ITEM_D	Operational item persisted data	
Portfolio Items	/RPM/V_FIN_PLAN	Financial Planning	
Portfolio Items	/RPM/DECISION	Decision Point Object Data	

Business post load validation signoff criteria:
The following are recommended steps to be performed to confirm that the loaded data aligns with target state design. In addition to this, business can perform checks as required.
1.	In the table /RPM/ITEM_D, Validate the portfolio items count is matching with the mapping file count. Validate correctness of different fields. 
2.	Check if number of records loaded in the Post-Load Report is equal to the number of records in the Pre-Load Report.
4.2	Reconciliation Requirements
The report will have source column, target column and comparison column for each of the fields which will be loaded from the load file populated by business. The details of the reconciliation report will be described in technical specifications. 
5	Security and Controls
5.1	Security Requirements 
•	Conversion files must be stored in a secured directory/repository with role-based access and change control. Only authorized project/system IDs should be able to upload, modify, or execute load files. 
•	Access to migration apps, load programs, staging tables, and validation transactions must be restricted to approved project roles and logged for audit. 
•	Where legacy files contain sensitive information, masking/redaction should be considered for non-production environments consistent with project policy. 


Object Type	Name	Transaction Code/ Fiori App	Authorization Group	Level of Security
Migration App/ Program 	Portfolio Items Conversion Load 	Project-approved migration object/app 	To be defined by Security 	Restricted – Conversion Team only 
Display / Validation 	Portoflio Item Display / Reporting 	Portoflio Items 	To be defined by Security 	Controlled – Business + Support 
File Repository 	Secured Conversion Folder 	N/A 	Project repository security group 	Restricted – Need-to-know 
<Complete the table below to reflect the security requirements outlined above> 
Role	Transaction Code(s)	Level of Security 
Conversion Technical Role 	Project migration app/program, logs, secured directory access 	Execute / Maintain within project controls 
D2B Functional Validation Role 	Portfolio Items	Display / Validate 
Business Approver Role 	Reporting / display access only 	Approve / Review 

6	Testing Requirements
Provide the necessary information to enable the technical team to carry out complete unit testing of the object.
6.1	Test Data  
Test data should include representative legacy portfolio items, across key portfolio types and lifecycle statuses (e.g., Created, Approved); portfolio items categorized as inactive, closed, or on hold should be excluded, and exception records with intentionally invalid or inconsistent attribute values to validate validation rules, rejection handling, and error reporting during migration.

6.2	Test Cases
List all the test cases which must be executed to validate that the business requirement is met. Provide both positive and negative test cases which check for programming accuracy. Be sure to provide at least one test case for every business requirement. This section should answer the question “What is the expected result for each requirement?”
Step No	Scenario Title	Steps Performed	Expected Results	Actual Results	Run
1
	Create the portfolio item	Update the Load file with the required values	- Verify the Portfolio Item is created in the Portfolio Item app via FIORI. 
- Verify the Portfolio Item is created under the correct Bucket. 
- Check that all relevant attributes are populated correctly.	Positive	Initials
2	Pre-validation of data	Provide valid and invalid records in the load file	Check the count of Valid records and invalid records	Positive	
3	Post validation of data	Check the count of records.
Validate the field level data	Count should match with Loaded records,
Field level match with the Load file.	Positive
	
4	Tables and logic	Review the SE16N table /RPM/ITEM_D for accuracy and the associated logic with this table 	SE16N table structure and values are as expected.	Positive	

 
7	Additional Information
Enter any additional information that could be helpful in developing this conversion.  

