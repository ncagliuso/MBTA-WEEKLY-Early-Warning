# MBTA-WEEKLY-Early-Warning

## Purpose

This project is produced every Monday for the Senior Director's Tuesday meeting with a Director from another department. It features data from incomplete projects in the Vehicle Maintenance and Vehicle Engineering departments, as well as specific projects in the Safety department. The Senior Director uses this data in conjuction with the data the fellow director brings to the meeting to decide which projects, and therefore requisitions, to prioritize on a weekly basis. 

### Data Requirements

#### `SLT_CPTL_EARLYWARNING.xlsx`

* This data is pulled from FMIS with the query name above

This excel file should contain the following columns:

| Columns                      | Definition/Use                                      |
| ---------------------------- | --------------------------------------------------- |
| Unit                         | Business Unit of each requisition                   |
| Req ID                       | Unique Identifier of each requisition               |
| Req_Created_Date             | Exact date that requisition was created             |
| Req Descr                    | Description of requisition                          |
| WO_Num                       | Bridge Identifier connecting CMS grants to FMIS Reqs|
| PO Num.                      | Unique Identifier of each Purchase Order            |
| Buyer                        | Buyer assigned to that requisition                  |
| Hold_Status                  | Shows if hold has been accepted or not              |
| Out-to bid                   | Shows if that PO has gone OTB; "Y" or "N"           |
| Req_Status                   | Self-explanatory                                    |
| Req_Approval_Date            | Exact date that requisiton was approved             |
| Req Total                    | Total Amount spent on that requisiton               |
| Req_Dflt_Tble_Buyer          | Buyer assigned to that requisition at header level  |
| PO Date                      | Exact date that Purchase Order was created          |
| Date                         | Exact date that Purchase Order was approved         |

#### `WO_Report_MMDDYYYY.xlxs`

* This data is emailed from someone in Capital Program Oversight every Monday

| Columns                      | Definition/Use                                      |
| ---------------------------- | --------------------------------------------------- |
| wo_nbr                       | Bridge Identifier connecting CMS grants to FMIS Reqs|
| Status                       | Unsure exactly, but will always be "A"              |
| Project_ID                   | Unique Identifier for each project                  |
| Project_Name                 | Self-explanatory                                    |
| Executing_Department         | Department under which each project falls           |
| Director                     | Capital Delivery data point; not relevant to P&L    |
| Project_Manager              | Capital Delivery data point; not relevant to P&L    |
| WO-date_approved             | Exact date that Work Order was approved             |
| wo_descr                     | Description of Work Order                           |
| cntrc_nbr                    | Capital Delivery data point; not relevant to P&L    |
| grant_id                     | Capital Delivery data pointl not relevant to P&L    |
| Req_Dflt_Tble_Buyer          | Buyer assigned to that requisition at header level  |
| PO Date                      | Exact date that Purchase Order was created          |
| Date                         | Exact date that Purchase Order was approved         |

### Project Creation

These two dataframes are joined by Work Order and filtered by the "Vehicle Maintenance" (VM) and "Vehicle Engineering" (VE) Executing Departments in order to create the final product, and the columns listed below are included in the following order:

**Note:** The fields are named slightly differently than above, as they are relabeled in MS Access to be easier to read.

* Executing Department
* Project ID
* Project Name
* Director
* Project Manager
* WO#
* Req ID
* Req_Created_Date
* Approval Date
* PO No#
* PO_Created_Date
* PO_Approved_Date
* Req Descr
* Buyer
* Unit
* HOLD_STATUS
* Out-to-bid
* Status
* Req_Header

In addition, the columns "Next_Steps" and "Duration" are added, which are an area for comments to be made and the time between today and Approval Date, respectively.

There is a much smaller dataframe tacked on to the bottom of the report, which is the joined table of `WO_Report_MMDDYYYY.xlsx` and the first joined table ("Composite"), where included rows are those Project ID's that *are* in `WO_Report_MMDDYYYY.xlsx` and simultaneously *are not* in Composite.

On top of the VM and VE WO's, there are specific WO#'s that must be manually searched for in Composite. They are as follows:

**Note:** These WO#'s come from a PDF sent by the Senior Director in March 2019. Certain WO#'s were highlighted and he wanted these specifically included in the report.

* 301572
* 301574
* 301598
* 301869
* 301595
* 301596
* 301597
* 301870
* 301874
* 301580
* 301871
* 301599
* 301600
* 301575
* 301576
* 301579
* 300070

Some of these will already be in the report as they fall under VM or VE, so nothing needs to be done. Any under the executing department "Safety" should be added, and the rest will simply not show up in Composite. These should still be added with a comment that they were not featured in Composite.

### Output File(s)

Ultimately, these steps culminate in two worksheets featuring the same fields listed above in "Project Creation," where one sheet is Projects With PO's and the other is Projects Without PO's. 



