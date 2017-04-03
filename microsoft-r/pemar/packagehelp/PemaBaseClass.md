--- 
 
# required metadata 
title: " Generator for a PemaBaseClass reference class object " 
description: " Generator for a PemaBaseClass reference class object to be used with pemaCompute. " 
keywords: "RevoPemaR, PemaBaseClass,  models " 
author: "richcalaway" 
manager: "jhubbard" 
ms.date: "03/23/2017" 
ms.topic: "reference" 
ms.prod: "microsoft-r" 
ms.service: "" 
ms.assetid: "" 
 
# optional metadata 
ROBOTS: "" 
audience: "" 
ms.devlang: "" 
ms.reviewer: "" 
ms.suite: "" 
ms.tgt_pltfrm: "" 
ms.technology: "r-server" 
ms.custom: "" 
 
--- 
 
 
 #`PemaBaseClass`:  Generator for a PemaBaseClass reference class object 

 Applies to version 8.0.3 of package RevoPemaR.
 
 ##Description
 
Generator for a PemaBaseClass reference class object to be used with pemaCompute.
 
 
 ##Usage

```   
  PemaBaseClass(...)
 
```
 
 
 ##Arguments

   
    
 ### ` ...`
  Arguments used in the constructor. Not used by the `PemaBaseClass` base class.  
  
 
 
 ##Details
 
This is a base reference class for the construction of reference classes
to be used for parallel external memory algorithms for use in
[pemaCompute](pemaCompute.md). See [PemaMean](PemaMean.md) for a simple
example.
 
 
 ##Value
 
A `PemaBaseClass` reference class object.
 
 
 ##Author(s)
 Microsoft Corporation [mrspack@microsoft.com](mrspack@microsoft.com)
 
 
 
 
 ##See Also
 
setRefClass,
[setPemaClass](setPemaClass.md),
[pemaCompute](pemaCompute.md),
[PemaMean](PemaMean.md)
   
 
 ##Examples

 ```
   
  
  # Show help for methods
  PemaBaseClass$help(initialize)
  PemaBaseClass$help(processData)
  PemaBaseClass$help(updateResults)
  PemaBaseClass$help(processResults)
  
 
```
 
 
 
 