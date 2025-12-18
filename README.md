# PowerBI-Showcase-III
Power BI Semantic Model Configuration
PL-300: Microsoft Power BI Data Analyst

Overview
This project focuses on designing and refining a semantic data model in Power BI Desktop. Key activities include establishing table relationships, configuring table and column properties for usability, creating analytical hierarchies and implementing quick measures for business metrics such as profit and profit margin. The lab also demonstrates how to configure a many-to-many relationship using a bridge (junction) table to support complex business logic—specifically, salesperson performance based on assigned sales territories.

Objectives
By completing this project, I have learned:

Creating and managing model relationships (including cardinality and cross-filter direction)
Configuring table and column metadata (display folders, descriptions, formatting, summarization)
Building hierarchies for intuitive drill-down analysis
Generating quick measures for common business calculations
Implementing and troubleshooting a many-to-many relationship
Disabling auto date/time to align with fiscal year requirements

Tool: Power BI Desktop
Starter File: Starter-Sales Analysis.pbix
Data Sources: Adventure Works–style sales data (embedded in .pbix)
Setup Instructions

Open Starter-Sales Analysis.pbix
Dismiss sign-in prompts by selecting Cancel
Choose Apply Later if prompted
Key Tasks & Implementation Summary
1. Model Relationships
Established the following active one-to-many relationships to enable proper filter propagation:

Product[ProductKey] → Sales[ProductKey]
Reseller[ResellerKey] → Sales[ResellerKey]
Region[SalesTerritoryKey] → Sales[SalesTerritoryKey]
Salesperson[EmployeeKey] → Sales[EmployeeKey]
Later, the direct Salesperson → Sales relationship was deactivated to enforce filter context through the bridge table for performance analysis.

2. Hierarchies
Created user-friendly drill paths for report authors:

Product Table: Products hierarchy (Category → Subcategory → Product)
Region Table: Regions hierarchy (Group → Country → Region)
Reseller Table:
Resellers (Business Type → Reseller)
Geography (Country-Region → State-Province → City → Reseller)
3. Table & Column Configuration
Enhanced model usability through metadata and formatting:

Display Folder:
Product table: Background Color Format and Font Color Format grouped under Formatting
Data Categories:
Region[Country] → Country/Region
Reseller[Country-Region] → Country/Region
Reseller[State-Province] → State or Province
Reseller[City] → City
Formatting & Summarization:
Sales[Quantity]: Enabled thousands separator
Sales[Unit Price]: Set decimal places = 2, Summarize By = Average
Financial columns (Standard Cost, Cost, Sales): 0 decimal places
Descriptions:
Sales[Cost]: “Based on standard cost”
4. Column Visibility
Hidden 13 technical or relationship-only columns (e.g., keys, UPN, order numbers) using bulk update of the Is Hidden property to declutter the report authoring experience.

5. Auto Date/Time
Disabled Auto Date/Time (via File > Options > Data Load > Time Intelligence) to prevent automatic date hierarchies that conflict with the organization’s July–June fiscal year.

6. Quick Measures
Created two business metrics using Power BI’s quick measure feature:

Profit = Sales – Cost
Profit Margin = Profit / Sales
Formatted as percentage with 2 decimal places
7. Many-to-Many Relationship
Implemented a performance-based sales analysis model using the SalespersonRegion bridge table:

Created relationships:
Salesperson[EmployeeKey] ↔ SalespersonRegion[EmployeeKey]
Region[SalesTerritoryKey] ↔ SalespersonRegion[SalesTerritoryKey]
Set cross-filter direction to Both on the Region ↔ SalespersonRegion relationship
Deactivated the direct Salesperson → Sales relationship to force filter context through territories
Renamed Salesperson table to Salesperson (Performance) to reflect its analytical purpose
8. Targets Integration
Linked performance to goals by creating a relationship:

Salesperson (Performance)[EmployeeID] → Targets[EmployeeID]
Added Targets[Target] to the report visual for side-by-side comparison
Final Model Structure
The semantic model now includes:

7 visible tables in Report view (1 hidden: SalespersonRegion)
4 hierarchies for intuitive navigation
2 quick measures for profitability analysis
1 many-to-many relationship path for territory-based sales attribution
Clean, business-friendly field names with contextual metadata
Notes
This model is designed to support two analytical contexts:
Transactional sales (via active relationships)
Salesperson performance by assigned territory (via bridge table and inactive relationship)
Further refinement, including DAX calculations to resolve ambiguous filter paths, will be addressed in subsequent labs.

Prepared by: Pang Kah Hwee
December 2025
