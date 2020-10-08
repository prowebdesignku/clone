;==========================================================
; USB Smart Card Driver, AKCCID.inf
;==========================================================

[Version]
Signature="$WINDOWS NT$"
Class=SmartCardReader
ClassGuid={50DD5230-BA8A-11D1-BF5D-0000F805F530}
provider=%MFGNAME%
CatalogFile=AKCCID.cat
DriverVer=12/05/2017, 1.7.46.1307


[Manufacturer]
%MFGNAME%=DeviceList, NTamd64

[DeviceList.NTamd64]
"Alcor Micro USB Smart Card Reader"=DriverInstall, USB\VID_058F&PID_9520
"Alcor Micro USB Smart Card Reader"=DriverInstall, USB\VID_058F&PID_9540


;----------------------------------------------------------------------------
;   CopyFile Sections
;----------------------------------------------------------------------------
[SourceDisksNames]
1="Installation Disc for Alcor Micro USB Smart Card Reader"

[SourceDisksFiles]
AKCCID.sys=1
AlcGener2.sys=1

[DestinationDirs]
DriverCopyFiles  = 12


;------------------------------------------------------------------------------
;  Driver Installation
;------------------------------------------------------------------------------
[DriverInstall.NT]
AddReg=DriverAddReg
CopyFiles=DriverCopyFiles

[DriverAddReg]
HKLM, Software\Microsoft\Cryptography\Calais\Readers,,,
HKLM, System\CurrentControlSet\Services\SCardSvr,Start,0x00010001,2
HKLM, System\CurrentControlSet\Services\CertPropSvc,Start,0x00010001,2

[DriverCopyFiles]
AKCCID.sys
AlcGener2.sys

;----------------------------------------------------------------------------
; Hardware Key
;----------------------------------------------------------------------------
[DriverInstall.NT.HW]
AddReg = AU95XX_Config

;----------------------------------------------------------------------------
;   Configuration
;----------------------------------------------------------------------------
[AU95XX_Config]
HKR,,"uSsEnable"		, %REG_DWORD%	, 1
HKR,,"uWwEnable"      		, %REG_DWORD%	, 0
HKR,,"uCardOutResume"      	, %REG_DWORD%	, 1
HKR,,"uSsMs"      		, %REG_DWORD%	, 30000
HKR,,"uDevNameSel"      	, %REG_DWORD%	, 2

HKR,,"sVendorName"    		, %REG_SZ%, Alcor Micro
HKR,,"sProductName"    		, %REG_SZ%, USB Smart Card Reader


HKR,,"uDataRateSel"		, %REG_DWORD%	, 0
HKR,,"uPowerPage"	      	, %REG_DWORD%	, 0
HKR,,"uSpeedMode"       	, %REG_DWORD%	, 0
HKR,,"uRemovable"	      	, %REG_DWORD%	, 1
HKR,,"uSupriseRemovalOK"      	, %REG_DWORD%	, 1

HKR,,"uSetDevPwrMode"		, %REG_DWORD%	, 2
HKR,,"uShowAdvSetting"      	, %REG_DWORD%	, 1
HKR,,"uReaderMode"      	, %REG_DWORD%	, 0
HKR,,"uShowAdvPageForAdmOnly"   , %REG_DWORD%	, 1
HKR,,"uChkVerLaunchUtility"     , %REG_DWORD%	, 1


HKR,,"uCommandMode"		, %REG_DWORD%	, 0
HKR,,"uCMDDelayMilliSec"      	, %REG_DWORD%	, 40000
HKR,,"uMaxCWI"      		, %REG_DWORD%	, 800
HKR,,"uDecCWI"      		, %REG_DWORD%	, 2

HKR,,"uCardOutDelay"      	, %REG_DWORD%	, 200
HKR,,"uLoadSetupFW"      	, %REG_DWORD%	, 1
HKR,,"uBIEn"      		, %REG_DWORD%	, 1
;--------------------------------------------------------------
[DriverInstall.NT.Services]
Addservice = AKCCID, 2, DriverService

[DriverService]
DisplayName    = "AK USB SmartCard Reader Driver"
ServiceType    = 1                  ; SERVICE_KERNEL_DRIVER
StartType      = 3                  ; SERVICE_AUTO_START
ErrorControl   = 1                  ; SERVICE_ERROR_NORMAL
ServiceBinary  = %12%\AKCCID.sys


;------------------------------------------------------------------------------
;  String Definitions
;------------------------------------------------------------------------------
[Strings]
MFGNAME = "AlcorMicro"


REG_EXPAND_SZ          = 0x00020000
REG_DWORD              = 0x00010001
REG_MULTI_SZ           = 0x00010000
REG_BINARY             = 0x00000001
REG_SZ                 = 0x00000000

