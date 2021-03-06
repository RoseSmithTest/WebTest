# Example StifleR Rules Definition

The following XML can be pasted into a text file and should be named StifleRulez.xml and placed on a server that is accessible to you clients via a virtual folder in IIS.

```markup
<StifleRData xmlns="http://schemas.microsoft.com/win/2004/08/events/event">
<VersionInfo>
<Issuer>2Pint Software</Issuer>
<Version>1.5</Version>
<Date>04/10/2017</Date>
</VersionInfo>
<TypeData>
<Type TypeID="1" Match="Contains">Push Notification Platform Job</Type>
<Type TypeID="2" Match="Equals">WU Client Download</Type>
<Type TypeID="100" Match="Equals">Windows Store</Type>
<Type TypeID="101" Match="Equals">OM Updates Client Download</Type>
<Type TypeID="102" Match="Equals">UpdateBinary</Type>
<Type TypeID="103" Match="URLContains" Internet="1">syntaro.com</Type>
<Type TypeID="3" Match="Equals">SkypeUpdate</Type>
<Type TypeID="4" Match="Equals">Setup Installer</Type>
<Type TypeID="5" Match="Equals">Font Download</Type>
<Type TypeID="6" Match="Contains">DMRCBitsJob</Type>
<Type TypeID="7" Match="Contains">Microsoft Outlook Offline Address Book</Type>
<Type TypeID="9" Match="Equals">Silverlight Updater</Type>
<Type TypeID="10" Match="Contains">.crx</Type>
<Type TypeID="10" Match="Contains">chrome</Type>
<Type TypeID="11" Match="URLContains" Internet="1">adobe.com</Type>
<Type TypeID="12" Match="Contains">AdbeRdr</Type>
<Type TypeID="13" Match="Contains">CCMSETUP DOWNLOAD</Type> <!--ConfigMgr Auto upgrade client job-->
<Type TypeID="14" Match="URLContains">SCCM_BranchCache$</Type> <!--All types of PeerCache transfers-->
<Type TypeID="21" Match="URLContains">SMS_MP</Type> <!-- All ConfigMgr MP Traffic-->
<Type TypeID="26" Match="Equals" UserInitiated="1" CCMDTSType="4" WinPE="1">CCMDTS Job</Type> <!--WinPE Initiated by user, typically OS deployments started by techies-->

<Type TypeID="25" Match="Equals" UserInitiated="0" CCMDTSType="4" WinPE="1">CCMDTS Job</Type> <!--WinPE Initiated Not started by user, typically OS deployments with required deployment-->

<Type TypeID="22" Match="Equals" UserInitiated="1" DownloadOnDemand="1" CCMDTSType="4">CCMDTS Job</Type> <!--User in full OS Initiated TS set to Download on Demand, typically OS deployments started by user from SW center-->

<Type TypeID="22" Match="Equals" UserInitiated="0" DownloadOnDemand="1" CCMDTSType="4">CCMDTS Job</Type> <!--TS pushed in full OS set to Download on Demand, typically pushed from Server as required deployment-->

<Type TypeID="22" Match="Equals" UserInitiated="1" CCMDTSType="8">CCMDTS Job</Type> <!--User in full OS Initiated Application/Virtual deployment started by user from SW center-->

<Type TypeID="26" Match="Equals" UserInitiated="1" CCMDTSType="4">CCMDTS Job</Type> <!--User in full OS Initiated TS with download all content before starting TS-->

<Type TypeID="26" Match="Equals" UserInitiated="0" CCMDTSType="4">CCMDTS Job</Type> <!--Required TS in full OS Initiated by a mandatory/required deployment-->

<Type TypeID="27" Match="Equals" UserInitiated="1" CCMDTSType="0">CCMDTS Job</Type> <!--User initiated Pkg/Programs started from SW center-->

<Type TypeID="23" Match="Equals" CCMDTSType="5">CCMDTS Job</Type> <!--All types of updates from ConfigMgr-->
<Type TypeID="24" Match="Equals">CCMDTS Job</Type> <!--All other types of ConfigMgr downloads-->

<Type TypeID="70" Match="SmallerThan" Internet="0">32768</Type>
<Type TypeID="71" Match="LargerThan" Internet="0">1073741824</Type>
<Type TypeID="72" Match="SmallerThan" Internet="1">32768</Type>
<Type TypeID="73" Match="LargerThan" Internet="1">1073741824</Type>
<Type TypeID="80" BranchCache="1" Internet="1" />
<Type TypeID="81" BranchCache="1" Internet="0" />
<Type TypeID="82" BranchCache="0" Internet="1" />
<Type TypeID="83" BranchCache="0" Internet="0" />
<!--<Type TypeID="0" Match="Unknown">Unknown</Type>-->
<!--
//Prioriry Cheat Sheet
ForeGround = 0,
High = 1,
Normal = 2,
Low = 3,

//Rulez matching cheat sheet
"Match" == "Contains", C# operation:: DisplayName.Contains()
"Match" == "StartsWith", C# operation:: DisplayName.StartsWith()
"Match" == "Equals", C# operation:: node.Value == job.DisplayName
"Match" == "URLContains", C# operation:: url.Contains()
"Match" == "SmallerThan", C# operation:: node.Value < job.Progress.BytesTotal
"Match" == "LargerThan", C# operation: node.Value > job.Progress.BytesTotal
-->

</TypeData>
<DownloadTypes>
<Download TypeID="0" Priority="3" Name="Unknown Job"/>
<Download TypeID="1" Priority="1" Name="Windows Platform"/>
<Download TypeID="2" Priority="1" Name="Windows Update"/>

<Download TypeID="3" Priority="3" Name="Skype"/>
<Download TypeID="4" Priority="3" Name="Windows Setup Installer"/>
<Download TypeID="5" Priority="3" Name="Office Font Download" />
<Download TypeID="6" Priority="3" Name="Windows Device Management"/>
<Download TypeID="7" Priority="3" Name="Microsoft Outlook OAB" />
<Download TypeID="9" Priority="3" Name="Silverlight Updater"/>
<Download TypeID="10" Priority="3" Name="Google Chrome" />
<Download TypeID="11" Priority="3" Name="Adobe"/>
<Download TypeID="12" Priority="3" Name="Adobe" Bandwidth="256"/>
<Download TypeID="14" Priority="0" Name="ConfigMgr PeerCache" />

<Download TypeID="20" Priority="2" Name="ConfigMgr Client Upgrade"/>
<Download TypeID="21" Priority="0" Name="SCCM Policy" />
<Download TypeID="22" Priority="1" StifleRPriority="1" Name="ConfigMgr User App" Bandwidth="512" />
<Download TypeID="25" Priority="1" StifleRPriority="1" Name="ConfigMgr TS" Bandwidth="512" />
<Download TypeID="26" Priority="1" StifleRPriority="1" Name="ConfigMgr User TS" Bandwidth="512" />
<Download TypeID="27" Priority="1" StifleRPriority="1" Name="ConfigMgr User Pkg/Prg" Bandwidth="512" />
<Download TypeID="23" Priority="2" StifleRPriority="2" Name="ConfigMgr Software Updates" />
<Download TypeID="24" Priority="3" StifleRPriority="3" Name="ConfigMgr Generic" />
<Download TypeID="25" Priority="0" Name="ConfigMgr PeerCache" />
<Download TypeID="70" Priority="2" Name="Small Internal Prio 2" Bandwidth="64" />
<Download TypeID="71" Priority="3" Name="Large Internal Prio 3" Bandwidth="2" />
<Download TypeID="72" Priority="2" Name="Small Internet Prio 2" Bandwidth="128" />
<Download TypeID="73" Priority="3" Name="Large Internet Prio 3" Bandwidth="256" />

<Download TypeID="80" Priority="2" Name="BranchCache External" Bandwidth="64" />
<Download TypeID="81" Priority="2" Name="BranchCache Internal" Bandwidth="2" />
<Download TypeID="82" Priority="3" Name="Non BranchCache External" Bandwidth="128" />
<Download TypeID="83" Priority="3" Name="Non BranchCache Internal" Bandwidth="256" />
<Download TypeID="100" Priority="2" Name="Windows Store"/>
<Download TypeID="101" Priority="2" Name="Microsoft Intune"/>
<Download TypeID="102" Priority="3" Name="MS OneDrive Updater"/>
<Download TypeID="103" Priority="2" Name="Syntaro Content"/>
</DownloadTypes>
</StifleRData>
```

