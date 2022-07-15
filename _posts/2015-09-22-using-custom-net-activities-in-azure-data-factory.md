---
id: 1161
title: 'Using custom .NET activities in Azure Data Factory'
date: '2015-09-22T14:30:57+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=1161'
permalink: /using-custom-net-activities-in-azure-data-factory/
categories:
    - Azure
    - 'Big Data'
tags:
    - .NET
    - 'Azure Batch'
    - 'Azure Data Factory'
    - HDInsight
---

Azure Data Factory provides a great number of data processing activities out of the box (for example running Hive or Pig scripts on Hadoop / HDInsight).

In many case though, you just need to run an activity that you already have built or know how to build in .NET. So, how would you go about that? Would you need to convert all those items to Hive scripts?

Actually, no. Enter Custom .NET activities. Using this you can run a .NET library on Azure Batch or HDInsight (whatever you like) and make it part of your Data Factory pipeline. Regardless of whether you use Batch or HDInsight you can just run your .NET code on it. I prefer using Batch since it provides more auto-scaling options, is cheaper and makes more sense to me in general; I mean, why run .NET code on a HDInsight service that runs Hive and Pig? It feels weird. However, if you already have HDInsight running and prefer to minimize the number of components to manage, choosing HDInsight might make more sense than using Batch.

So, how would you do this? First of all, you would need a custom activity. For this you will need to .NET class library and need to extend IDotNetActivity interface. Please refer to <a href="https://azure.microsoft.com/en-us/documentation/articles/data-factory-use-custom-activities/">https://azure.microsoft.com/en-us/documentation/articles/data-factory-use-custom-activities/</a> for details. Trust me, it is not hard; I have done it.

Next, once you have a zip file as indicated on the page above, make sure to upload it to a Azure Blob store you can use later. The pipeline will need to know what assembly to load from where later on.

You will need to create an Azure Batch account and pool if you use that. If you decide to use HDInsight either let ADF spin one up on demand or make sure you have your HDInsight cluster ready.

You will need to create input and output tables in Azure Data Factory, as well as linked services to Storage and Batch or HDInsight. Your pipeline will look a bit like this:
<pre class="lang:js decode:true crayon-selected">{
"name": "ADFTutorialPipelineCustom",
"properties": {
"description": "Use custom activity",
"activities": [
{
"Name": "MyDotNetActivity",
"Type": "DotNetActivity",
"Inputs": [
 {
"Name": "EmpTableFromBlob"
 }
],
"Outputs": [
 {
"Name": "OutputTableForCustom"
 }
 ],
"LinkedServiceName": "AzureBatchLinkedService1",
"typeProperties": {
"AssemblyName": "AzureDataFactoryCustomActivity.dll",
"EntryPoint": "AzureDataFactoryCustomActivityNS.AzureDataFactoryCustomActivity",
"PackageLinkedService": "AzureStorageLinkedService1",
"PackageFile": "adfcustomactivity/customactivitycontainer/AzureDataFactoryCustomActivity.zip",
"extendedProperties": {
"SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
 }
 },
"Policy": {
"Concurrency": 1,
"ExecutionPriorityOrder": "OldestFirst",
"Retry": 3,
"Timeout": "00:30:00",
"Delay": "00:00:00"
 }
 }
 ],
"start": "2015-09-07T14:00:00Z",
"end": "2015-09-07T18:00:00Z",
"isPaused": false
 }
}
</pre>
&nbsp;

Switching from Batch to HDInsight means to changing the LinkedServiceName for the activity to point to your HDInsight or HDInsight on demand cluster.

Tables are passed to the .NET activity using a connection string, so essentially if you have both input and output tables defined as blob storage items, your custom assembly will get a connection string to the blob storage items, read the input files, do its processing and write the output files before passing on the control to ADF.

Using this framework the sky is the limit: anything you can run in .NET can now be part of your ADF processing pipeline…pretty cool!