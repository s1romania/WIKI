---
layout: default
title: Credit Notes and Refunds
nav_order: 3
parent: Sales
---


# Average Price Evaluation in Soft1 ERP


The suggested method you can use in perpetual stock valuation in Soft1 ERP, is the average cost. This document answers to the recurrent questions for companies using that method to make their stock valuation: How will it work and how does a shipping returned to its supplier impact the average cost? This document is only for the specific use case of a perpetual valuation and in average price costing method (as opposed to standard of FIFO).

|Cost of Goods Sold <br>Commercial Document(Sales, Purchases etc)|Itelines.SALESCVAL|
| :- | :- |
|Accounting record field used|[MTL57] [Import-export cost (goods sold)]|


## Definition of average cost

The average cost method calculates the cost of ending inventory and cost of goods sold on the basis of weighted average cost per unit of inventory.

The weighted average cost per unit is calculated using the following formula:


![AVG Formula](/WIKI/assets/images/AVGFORMULA.jpg)

When new goods arrive in a warehouse, the new average cost is recomputed as:


The only time you would recalculate the unit cost in the average cost method is when you make an additional purchase.

Average Cost method is widely accepted by numerous accounting standards, including US GAAP and IFRS.. Using an average significantly simplifies the calculations and recordkeeping associated with maintaining the inventory and determining the Cost of Goods Sold. Both FIFO and LIFO require that individual items be tracked, which can be expensive and extremely time consuming for the users. 
Average Cost is superior to FIFO and LIFO, especially when the items are **indistinguishable** from one another or when tracking individual items would be highly inefficient. Average Cost can also effectively normalize **cost fluctuations and volatilities** and help **reduce the inappropriate manipulation of income**.  Each time there is a purchase that adds additional units into Inventory, the average cost is recalculated. This weighted-average ensures that both past and new purchases are incorporated into the cost, ensuring that Costs of Goods Sold is not overstated (which is an issue with LIFO) or understated (which is an issue with FIFO).




## Examples

```yaml
The scenario below was prepared on 01 October 2021 using Soft1 Series 5 version 521.11438
```


|1. *You will create a NEW ITEM without past transactions*
2. *You will keep the number straight so that the results are easily calculated*
3. *You will be posting transactions in 3 months*
4. *adjust the months described below to your current month-2 months <br> 
    You will post purchases in 2 past months, 1 sales last month and one return this month*
  5. *Your company is using Weighted avg. Cost for valuation method*|
| :- |

**Step 1.** Create a new item

Purchase use case

**Step 2.** Aug 2021àBuy 100 pieces for **1euro**. Annual weight price should be 1euro

**Step 3.** Sept 2021 buy 100pieces for **1,10euro**. Annual weighted price should be 1.05 euro

*Below is the financial data of the item in Soft1. Annual weighted price is 1.05euro*

In the next picture we see the item transactions


Weighted Average cost example explained **after 2 purchases**

|**Operation**|**Calculation**|**Inventory Value (IN-OUT)**|**Inventory Balance**|**Avg Cost**|
| :-: | :-: | :-: | :-: | :-: |
|||0|0|0|
|**Receive 100 Pieces at 1 euro**|+100\*1euro|100|100|1|
|**Receive 100 Pieces at 1.10 euro**|+100\*1.10 euro|100+110=210|100+100=200|1.05|



|** NOTE / Common mistake**|
|If you are going to run the batch operation “Cost Price Calculation” for more than one months always execute this operation
|for the CURRENT MONTH **LAST**.
|If you dont then the cost numbers will not be correct, since the application will use the last calculation as reference point.
|For instance if in my scenario i run the LAST cost operation for August (when i bought the item on 1euro price[note:September i bought it 1,10] 
|then the results will be like the ones below WRONG! )
|Instead, run the operation for the last time for the CURRENT Month and the results will be correct!|



## Sales use case

Now that we have a clear view of the balance cost and the weighted average cost lets move ahead.

**Step 4.** Sell this item in October. 2 pieces for 1.50euro(NET value)


Weighted Average cost example explained **after 1 sale**

|**Operation**|**Calculation**|**Inventory Value(IN-OUT)**|**Inventory Balance**|**Avg Cost**|
| :-: | :-: | :-: | :-: | :-: |
|||0|0|0|
|**Receive 100 Pieces at 1 euro**|+100\*1euro|100|100|1|
|**Receive 100 Pieces at 1.10 euro**|+100\*1.10 euro|100+110=210|100+100=200|1.05|
|**Deliver 2 pieces for 1.5 euro**|-2\*1.5euro|210-3=207|200-2=198|1.05|


**Step 5.** Run Cost Price Calculation batch operation (if it is not defined in the settings of the app) and check the option like below. This will calculate the Cost of Good sold for the sale document we posted in the previous step.

|In the calculation of cost prices participate all the warehouse movements that in Doc type design affect invoiced quantities and import / export values.|




|Cost of Goods Sold in this document and in summary reportsInside the sales document, you can drag and drop the column  
COST (itelines.SALESCVAL)Numerous reports can help you find the information you need.
 **Item Statements(MAT\_STM)**As well as a simple browser list can provide you the information you need|







## Sales return use case

**Step 6.** A customer returns 1 piece of the item he bought. Convert your sales invoice into a credit note-Delivery Note


**Step 7.** If the cost price is not calculated run the Cost price Calculation for this item again in the current month. Make sure that the cost column in the transaction is filled(ITELINES.SALECVAL).


Lets run the reports again



Item Statement Report

Stock Ledger(MAT\_BOOK)
*Make sure you run the report for the current month*


Weighted Average cost example explained **after 1 return from customer**

|**Operation**|**Calculation**|**Inventory Value(IN-OUT)**|**Inventory Balance**|**Avg Cost**|
| :-: | :-: | :-: | :-: | :-: |
|||0|0|0|
|**Receive 100 Pieces at 1 euro**|+100\*1euro|100|100|1|
|**Receive 100 Pieces at 1.10 euro**|+100\*1.10 euro|100+110=210|100+100=200|1.05|
|**Deliver 2 pieces for 1.5 euro**|-2\*1.5euro|210-3=207|200-2=198|1.05|
|**Return 1 piece from customer**|+1\*1.5euro|207+1.5euro=208.5|198+1=**199**|1.05|



Purchase return use case

The supplier refund will be made using the original purchase price. 

There are 2 alternative flows you can follow depending on your internal processes.

**Flow 1**



**Step 8.1** Our company has to dispatch the goods back to the supplier with a **Delivery/Return Note**. This transaction as we see below does not affect any cost in the inventory.


Weighted Average cost example explained **after 1 Del. Note to Supplier**

|**Operation**|**Calculation**|**Inventory Value(IN-OUT)**|**Inventory Balance**|**Avg Cost**|
| :-: | :-: | :-: | :-: | :-: |
|||0|0|0|
|**Receive 100 Pieces at 1 euro**|+100\*1euro|100|100|1|
|**Receive 100 Pieces at 1.10 euro**|+100\*1.10 euro|100+110=210|100+100=200|1.05|
|**Deliver 2 pieces for 1.5 euro**|-2\*1.5euro|210-3=207|200-2=198|1.05|
|**Return 1 piece from customer**|+1\*1.5euro|207+1.5euro=208.5|198+1=**199**|1.05|
|**Deliver 3 pieces to Supplier**|-10\*0|208.5|199-10=189|1.05|


**Item Statement report**

The stock ledger is shaped as follows:





**Step 8.2** Our company receives from the supplier the credit note for the items we returned- in the original purchase price. This is how your item transaction should be setup 

And below you see the document which will be posted

Weighted Average cost example explained **after 1 Credit Note from Supplier**

|**Operation**|**Calculation**|**Inventory Value(IN-OUT)**|**Inventory Balance**|**Avg Cost**|
| :-: | :-: | :-: | :-: | :-: |
|||0|0|0|
|**Receive 100 Pieces at 1 euro**|+100\*1euro|100|100|1|
|**Receive 100 Pieces at 1.10 euro**|+100\*1.10 euro|100+110=210|100+100=200|1.05|
|**Deliver 2 pieces for 1.5 euro**|-2\*1.5euro|210-3=207|200-2=198|1.05|
|**Return 1 piece from customer**|+1\*1.5euro|207+1.5euro=208.5|198+1=**199**|1.05|
|**Deliver 3 pieces to Supplier**|-10\*0|208.5|199-10=189|1.05|
|**Credit Note from Supplier**|-10\*1.10euro|208.5-11euro=198.45|189-0=189|1.05|

**Item Statement report**






**Flow 2. Alternative Flow for returns to supplier** 


**In this scenario you DO NOT use a delivery/return note to your supplier.**

If you wish you can post a single transaction for your credit notes(a transaction which affects values+quantities ) 

The result is going to be the same as the previous flow, but in one single transaction



## **BASIC Troubleshooting**

1. Every transaction TYPE (it doesn’t matter which object it is) in SoftOne has the following option:

This defines HOW the transaction will update the item history. Read more on wiki at the threads:
`             `“Design Inventory transactions” and

` `“Inventory - Cost Prices”. 

A wrong setup on your transactions might lead in to wrong results.

1. Make sure you run the Item Costing Operation when necessary and in the sequence described below. Wrong use of the operation may lead to wrong data. 
1. Are you sure your sales transactions have COST (itelines.salescval)? Simply design an indexlist displaying this column. Every transaction which generates export value should have this column filled.
1. In the calculation of cost prices participate all the warehouse movements that in the params design affect **invoiced quantities and import / export values**. Is this your setup?
1. Make sure in ParametersàCommercialàStock ManagementàParameters the option “OnLine cost calculation” is checked.
1. If you wish the system to automatically calculate the cost of goods sold(and avoid running the Cost Price Calculation every time), then inside the settings of every SALES document type make sure the following option is checked.




*NOTE: Only for ROMANIAN version of Soft1 and onlye for 521 version and beyond*


1. Investigate if your users have posted transactions using other operational entities of Soft1 ERP like 
- Inventory Transactions
- Composition Documents
- Production Documents
- Consumption and Production Notes
1. You have done everything, but still don’t see correct numbers. Try running the reupdate process for inventory. More info on this are available on WIKI at the thread “REUPDATES” 




## **APPENDIX**

**What Is Inventory Valuation?**
Inventory valuation is the accounting process of assigning value to a company’s inventory. Inventory typically represents a large portion of the assets of any company that sells physical items, so it’s important to measure its value in a consistent manner. A clear understanding of inventory valuation can help maximize profitability. It also ensures the company can accurately represent the value of inventory on its financial statements.

**Inventory Valuation Explained**

There are several methods for calculating inventory value. For example, the First In, First Out (FIFO) method values inventory as though the first inventory items purchased are the first to be sold. The Weighted Average Cost (WAC) supported by Soft1 ERP method is based on the average cost of items purchased.

The inventory valuation method a company chooses can affect its gross profit during an accounting period. Note that the choice of inventory valuation method is an accounting decision and not necessarily related to the way a company actually uses its inventory. For example, if a company uses FIFO valuation, it is not obliged to move the oldest inventory first.

**Why Is Inventory Valuation Important for Businesses?**

The way a company values its inventory directly affects its cost of goods sold (COGS), gross income and the monetary value of inventory remaining at the end of each period. Therefore, inventory valuation affects the profitability of a company and its potential value, as presented in its financial statements.

**What Are the Objectives of Inventory Valuation?**

The overall objective of inventory valuation is to help create an accurate picture of a company’s gross profitability and financial position. To calculate the gross profit listed on the company’s income statement, a company must subtract the cost of goods sold (COGS) from net sales (total sales — returns and discounts and any other income not related to sales).

**The pros of the weighted average method**

The benefit is that it’s much easier to track than specific costing because you don’t need to know exactly which batch a sold unit was part of, which is especially helpful when you have many identical units



## **Resources**

Soft1 WIKI àInventory Configuration [link here](https://wiki.soft1.eu/display/SS4EN/Inventory+Configuration)

Soft1 WIKI à Inventory Cost Prices Methods   [link here](https://wiki.soft1.eu/display/SS4EN/Inventory+-+Cost+Prices)

Soft1 WIKIà Design Inventory Transactions [link here](https://wiki.soft1.eu/display/SS4EN/Design+Inventory+transactions)

MS Excel àExamples of inventory results in every cost evaluation algorithm [link here](https://s1product.blob.core.windows.net/wiki/ATTACHED%20FILES/%CE%A4%CE%B9%CE%BC%CE%AD%CF%82%20%CE%BA%CF%8C%CF%83%CF%84%CE%BF%CF%85%CF%82_%CF%80%CE%B1%CF%81%CE%B1%CE%B4%CE%B5%CE%AF%CE%B3%CE%BC%CE%B1%CF%84%CE%B1_ver.09.1113.xls)

