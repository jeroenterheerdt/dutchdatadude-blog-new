---
id: 407
title: 'Working with Azure and HDInsight from SSIS'
date: '2013-11-05T10:00:57+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=407'
permalink: /working-with-azure-and-hdinsight-from-ssis/
categories:
    - Azure
    - 'Big Data'
    - 'Business Intelligence'
tags:
    - azure
    - 'big data'
    - Hadoop
    - HDInsight
    - ssis
---

A while ago a <a href="http://download.microsoft.com/download/D/2/0/D20E1C5F-72EA-4505-9F26-FEF9550EFD44/Leveraging%20a%20Hadoop%20cluster%20from%20SQL%20Server%20Integration%20Services.docx">whitepaper was published on how to work with Azure and HDInsight (Hadoop on Azure) from SSIS</a>. In that whitepaper some code samples were given. That code is also available here (including some components): <a href="http://code.msdn.microsoft.com/SSIS-Packages-Sample-for-2ffd9c32">http://code.msdn.microsoft.com/SSIS-Packages-Sample-for-2ffd9c32</a> . After you have downloaded the zip make sure you have Visual Studio installed, start the Developer Command for Visual Studio as Administrator and run the 'deploy_SSIS_packages_and_components.bat' file which is included in the zip. This will install some of the DLLs included into the GAC. Then, you can open the solution in Visual Studio.

The solution includes the following sample SSIS packages:
<ul>
	<li>PigSqoopPackage: shows how to work with Pig and SQOOP tasks</li>
	<li>HadoopJobAutomation: shows how to start jobs on Hadoop and how to consume results</li>
	<li>ComplexSourceDestination: shows how to get data from Azure Blog Storage and save the results into various targets, including Azure Blob Storage.</li>
	<li>BlobSourceTestPackage: sample package showing how to read data from Azure Blob Storage.</li>
	<li>BlobDestinationTestPackage: sample package showing how to write data to Azure Blob Storage.</li>
</ul>
The first two packages essentially contain some script tasks with complete samples on how to work with Piq, SQOOP and Hadoop jobs respectively. The other packages use the components provided and provide a quick start on getting data from Azure Blob Storage and getting data into Azure Blog Storage using SSIS.