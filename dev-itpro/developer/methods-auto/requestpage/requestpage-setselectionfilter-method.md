---
title: "SetSelectionFilter Method"
ms.author: solsen
ms.custom: na
ms.date: 05/28/2019
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.service: "dynamics365-business-central"
author: solsen
---
[//]: # (START>DO_NOT_EDIT)
[//]: # (IMPORTANT:Do not edit any of the content between here and the END>DO_NOT_EDIT.)
[//]: # (Any modifications should be made in the .xml files in the ModernDev repo.)
# SetSelectionFilter Method



## Syntax
```
 RequestPage.SetSelectionFilter(var Record: Record)
```
## Parameters
*RequestPage*  
&emsp;Type: [RequestPage](requestpage-data-type.md)  
An instance of the [RequestPage](requestpage-data-type.md) data type.  

*Record*  
&emsp;Type: [Record](../record/record-data-type.md)  
  



[//]: # (IMPORTANT: END>DO_NOT_EDIT)

## Remarks  
If all records are selected, marks will not be used.  
  
If only the current record is selected on the page, then SetSelectionFilter does the following:  
  
- Sets the current filter group to 0 on the destination record  
  
- Adds filters on the primary key fields that point to the current record of the page  
  
If more than one record is selected on the page, then SetSelectionFilter does the following:  
  
- Copies the current key from the page source table to the destination record  
  
- Copies the current sort order from the table to the destination record  
  
- Copies the current filters that are set in all filter groups  
  
- Copies the current filter group  
  
- Marks the selected records and sets the "marked only" filter  
  
## See Also
[RequestPage Data Type](requestpage-data-type.md)  
[Getting Started with AL](../../devenv-get-started.md)  
[Developing Extensions](../../devenv-dev-overview.md)