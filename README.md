Target												Source System			Conversion Rules
Description	Screen Name	Technical Field Name	Table Name (if known)	Data Type	Length	View or Grouping	Input Type	Dropdown Values	Check Table	Field Configurable Y/N	Mandatory?	Description	Table/Field Name	Table-Field	"Conversion Details - Mapping Rules for Developer
(Suggested Values - Should be tweaked according to project)"
Enter  field name from the data object. Extract a list of fields from S/4HANA. 	Screen name in the SAP View	Enter the technical S/4HANA field name 	Enter the technical name of the S/4HANA table the field is stored in	S/4HANA data type	Length of the field in S/4HANA	Enter the view or grouping in S/4HANA to enter the field	Indicate the type of input here Ex: Drop-down, Free form text, Checkbox, etc.,	Indicate if the field will have a drop down list to select from or not	Check Table Name	Field Configurable Y/N	Y/N	Enter in the field name from the data object. Extract a list of fields from SAP. 	Source table or file name	Table-Field	Mapping/Transformation Rules
Portfolio Item ID	General Information	EXTERNAL_ID	/RPM/ITEM_D	Text		General Information	Free Form Text	N		N	N				
Portfolio Item Name			/RPM/ITEM_D	Text		General Information	Free Form Text	N		N	Y				
Item Type		ITEM_TYPE	/RPM/ITEM_D	Alphanumeric		General Information	Dropdown	Y	/RPM/V_ITEM_TYPE	Y	Y				
Bucket			/RPM/ITEM_D	Text		General Information	Dropdown	Y		N	Y				
Status		STATUS	/RPM/ITEM_D	Text		General Information	Dropdown	Y	/RPM/V_ITEM_STAT	Y	N				
Forecast Start Date		FORECAST_START	/RPM/ITEM_D	Date		General Information	Date Picker	Y		N	N				
Forecast End Date		FORECAST_FINISH	/RPM/ITEM_D	Date		General Information	Date Picker	Y		N	N				
Planned Start Date		PLANNED_START	/RPM/ITEM_D	Date		General Information	Date Picker	Y		N	N				
Planned End Date		PLANNED_FINISH	/RPM/ITEM_D	Date		General Information	Date Picker	Y		N	N				
Priority		PRIORITY_GROUP	/RPM/ITEM_D			General Information	Dropdown	Y		N	N				
Project Manager			/RPM/ITEM_D	Text		General Information	Dropdown	Y		N	N				
Project Sponsor			/RPM/ITEM_D	Text		General Information	Dropdown	Y		N	N				
Project Controller			/RPM/ITEM_D	Text		General Information	Dropdown	Y		N	N				
Portfolio Manager			/RPM/ITEM_D	Text		General Information	Dropdown	Y		N	N				
Description			/RPM/ITEM_D	Text		General Information	Free Form Text	N		N	N				
Decision Point ID	Phases & Decisions	DECISION_ID	/RPM/DECISION	Text		Phases & Decisions	Free Form Text	N		N	N				
Decision Point Name		DECISION_NAME	/RPM/DECISION	Text		Phases & Decisions	Free Form Text	N		N	Y				
Status		STATUS	/RPM/DECISION	Text		Phases & Decisions	Dropdown	Y		N	N				
Forecast Start Date		FORECAST_START	/RPM/DECISION	Date		Phases & Decisions	Date Picker	Y		N	N				
Forecast Finish Date		FORECAST_FINISH	/RPM/DECISION	Date		Phases & Decisions	Date Picker	Y		N	N				
Planned Start Date		PLAN_START	/RPM/DECISION	Date		Phases & Decisions	Date Picker	Y		N	N				
Planned Finish Date		PLAN_FINISH	/RPM/DECISION	Date		Phases & Decisions	Date Picker	Y		N	N				
Actual Start Date		ACTUAL_START	/RPM/DECISION	Date		Phases & Decisions	Date Picker	Y		N	N				
Actual Finish Date		ACTUAL_FINISH	/RPM/DECISION	Date		Phases & Decisions	Date Picker	Y		N	N				
Forecast Decision Date		DECISION_DATE	/RPM/DECISION	Date		Phases & Decisions	Date Picker	Y		N	N				
Planned Decision Date		PLANNED_DEC_DATE	/RPM/DECISION	Date		Phases & Decisions	Date Picker	Y		N	N				
Actual Decision Date		ACTUAL_DEC_DATE	/RPM/DECISION	Date		Phases & Decisions	Date Picker	Y		N	N				
Dependency ID	Relationship			Alphanumeric		Relationship	Free Form Text	N		N	Y				
Dependency Name				Text		Relationship	Free Form Text	N		N	Y				
Determining Item ID				Alphanumeric		Relationship	Free Form Text	N		N	N				
Determining Item Name				Text		Relationship	Free Form Text	N		N	N				
Planned Start				Date		Relationship	Date Picker	Y		N	N				
Planned Finish				Date		Relationship	Date Picker	Y		N	N				
Type				Text		Relationship	Dropdown	Y		N	N				
Risk						Relationship		N		N	N				
Risk Status				Text		Relationship	Dropdown	Y		N	N				
Group	Related Objects			Text		Related Objects	Dropdown	Y		N	N				
Object Name				Text		Related Objects	Dropdown	Y		N	N				
Object Number				Numeric		Related Objects	Dropdown	Y		N	N				
Currency	Financial Planning	CURRENCY 		Text		Financial Planning	Dropdown	Y	/RPM/V_CURRENCY	Y	N				
Financial Category		CATEGORY    		Alphanumeric		Financial Planning	Dropdown	Y	/RPM/V_FIN_CATG	Y	N				
Financial View		FIN_VIEW    		Alphanumeric		Financial Planning	Dropdown	Y	/RPM/V_FIN_VIEW	Y	N				
Financial group		GROUP_ID   		Alphanumeric		Financial Planning	Dropdown	Y	/RPM/V_FINGROUPS	Y	N				
Amount		AMOUNT   		Numeric		Financial Planning	Free Form Text	N		N	N				
