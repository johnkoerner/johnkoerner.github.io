---
layout: post
status: publish
published: true
title: Windows Installer Error Codes
author: John Koerner
author_email: blog@johnkoerner.net
wordpress_id: 1589
wordpress_url: https://johnkoerner.com/?p=1589
disqus_identifier: "http://nickcraver.com/blog/?p=1"
date: '2016-04-07 02:06:50 -0400'
date_gmt: '2016-04-07 02:06:50 -0400'
categories:
- Install
tags: []
---
My team was recently working on our installer when we ran into a return code from one of our pre-requisites (specifically the Visual C++ 2015 Runtime). From the logs, we found the error code was 0x80070666 and the return code was 0x666 (a newer version of the runtime was installed). We could easily handle this scenario, but we were looking to find an extensive list of return codes for the C++ redistributables and could not easily find them. Eventually we ran across the list of [MsiExec.exe and InstMsi.exe Error Messages](https://msdn.microsoft.com/en-us/library/windows/desktop/aa376931(v=vs.85).aspx) and figured out why our searches were yielding no results. The error codes in the log files are all in hex and the error codes on the website are all in decimal. So, to help others with this in the future, here is a list of all of the error codes from that link with their hex equivalent.

| Error code | Value | Description | Hex | Error Code |
| --- | --- | --- | --- | --- |
| ERROR_SUCCESS | 0 | The action completed successfully. | 0x0 | 0x80070000 |
| ERROR_INVALID_DATA | 13 | The data is invalid. | 0xD | 0x8007000D |
| ERROR_INVALID_PARAMETER | 87 | One of the parameters was invalid. | 0x57 | 0x80070057 |
| ERROR_CALL_NOT_IMPLEMENTED | 120 | This value is returned when a custom action attempts to call a function that cannot be called from custom actions. The function returns the value ERROR_CALL_NOT_IMPLEMENTED. Available beginning with Windows Installer version 3.0. | 0x78 | 0x80070078 |
| ERROR_APPHELP_BLOCK | 1259 | If Windows Installer determines a product may be incompatible with the current operating system, it displays a dialog box informing the user and asking whether to try to install anyway. This error code is returned if the user chooses not to try the installation. | 0x4EB | 0x800704EB |
| ERROR_INSTALL_SERVICE_FAILURE | 1601 | The Windows Installer service could not be accessed. Contact your support personnel to verify that the Windows Installer service is properly registered. | 0x641 | 0x80070641 |
| ERROR_INSTALL_USEREXIT | 1602 | The user cancels installation. | 0x642 | 0x80070642 |
| ERROR_INSTALL_FAILURE | 1603 | A fatal error occurred during installation. | 0x643 | 0x80070643 |
| ERROR_INSTALL_SUSPEND | 1604 | Installation suspended, incomplete. | 0x644 | 0x80070644 |
| ERROR_UNKNOWN_PRODUCT | 1605 | This action is only valid for products that are currently installed. | 0x645 | 0x80070645 |
| ERROR_UNKNOWN_FEATURE | 1606 | The feature identifier is not registered. | 0x646 | 0x80070646 |
| ERROR_UNKNOWN_COMPONENT | 1607 | The component identifier is not registered. | 0x647 | 0x80070647 |
| ERROR_UNKNOWN_PROPERTY | 1608 | This is an unknown property. | 0x648 | 0x80070648 |
| ERROR_INVALID_HANDLE_STATE | 1609 | The handle is in an invalid state. | 0x649 | 0x80070649 |
| ERROR_BAD_CONFIGURATION | 1610 | The configuration data for this product is corrupt. Contact your support personnel. | 0x64A | 0x8007064A |
| ERROR_INDEX_ABSENT | 1611 | The component qualifier not present. | 0x64B | 0x8007064B |
| ERROR_INSTALL_SOURCE_ABSENT | 1612 | The installation source for this product is not available. Verify that the source exists and that you can access it. | 0x64C | 0x8007064C |
| ERROR_INSTALL_PACKAGE_VERSION | 1613 | This installation package cannot be installed by the Windows Installer service. You must install a Windows service pack that contains a newer version of the Windows Installer service. | 0x64D | 0x8007064D |
| ERROR_PRODUCT_UNINSTALLED | 1614 | The product is uninstalled. | 0x64E | 0x8007064E |
| ERROR_BAD_QUERY_SYNTAX | 1615 | The SQL query syntax is invalid or unsupported. | 0x64F | 0x8007064F |
| ERROR_INVALID_FIELD | 1616 | The record field does not exist. | 0x650 | 0x80070650 |
| ERROR_INSTALL_ALREADY_RUNNING | 1618 | Another installation is already in progress. Complete that installation before proceeding with this install. | 0x652 | 0x80070652 |
| ERROR_INSTALL_PACKAGE_OPEN_FAILED | 1619 | This installation package could not be opened. Verify that the package exists and is accessible, or contact the application vendor to verify that this is a valid Windows Installer package. | 0x653 | 0x80070653 |
| ERROR_INSTALL_PACKAGE_INVALID | 1620 | This installation package could not be opened. Contact the application vendor to verify that this is a valid Windows Installer package. | 0x654 | 0x80070654 |
| ERROR_INSTALL_UI_FAILURE | 1621 | There was an error starting the Windows Installer service user interface. Contact your support personnel. | 0x655 | 0x80070655 |
| ERROR_INSTALL_LOG_FAILURE | 1622 | There was an error opening installation log file. Verify that the specified log file location exists and is writable. | 0x656 | 0x80070656 |
| ERROR_INSTALL_LANGUAGE_UNSUPPORTED | 1623 | This language of this installation package is not supported by your system. | 0x657 | 0x80070657 |
| ERROR_INSTALL_TRANSFORM_FAILURE | 1624 | There was an error applying transforms. Verify that the specified transform paths are valid. | 0x658 | 0x80070658 |
| ERROR_INSTALL_PACKAGE_REJECTED | 1625 | This installation is forbidden by system policy. Contact your system administrator. | 0x659 | 0x80070659 |
| ERROR_FUNCTION_NOT_CALLED | 1626 | The function could not be executed. | 0x65A | 0x8007065A |
| ERROR_FUNCTION_FAILED | 1627 | The function failed during execution. | 0x65B | 0x8007065B |
| ERROR_INVALID_TABLE | 1628 | An invalid or unknown table was specified. | 0x65C | 0x8007065C |
| ERROR_DATATYPE_MISMATCH | 1629 | The data supplied is the wrong type. | 0x65D | 0x8007065D |
| ERROR_UNSUPPORTED_TYPE | 1630 | Data of this type is not supported. | 0x65E | 0x8007065E |
| ERROR_CREATE_FAILED | 1631 | The Windows Installer service failed to start. Contact your support personnel. | 0x65F | 0x8007065F |
| ERROR_INSTALL_TEMP_UNWRITABLE | 1632 | The Temp folder is either full or inaccessible. Verify that the Temp folder exists and that you can write to it. | 0x660 | 0x80070660 |
| ERROR_INSTALL_PLATFORM_UNSUPPORTED | 1633 | This installation package is not supported on this platform. Contact your application vendor. | 0x661 | 0x80070661 |
| ERROR_INSTALL_NOTUSED | 1634 | Component is not used on this machine. | 0x662 | 0x80070662 |
| ERROR_PATCH_PACKAGE_OPEN_FAILED | 1635 | This patch package could not be opened. Verify that the patch package exists and is accessible, or contact the application vendor to verify that this is a valid Windows Installer patch package. | 0x663 | 0x80070663 |
| ERROR_PATCH_PACKAGE_INVALID | 1636 | This patch package could not be opened. Contact the application vendor to verify that this is a valid Windows Installer patch package. | 0x664 | 0x80070664 |
| ERROR_PATCH_PACKAGE_UNSUPPORTED | 1637 | This patch package cannot be processed by the Windows Installer service. You must install a Windows service pack that contains a newer version of the Windows Installer service. | 0x665 | 0x80070665 |
| ERROR_PRODUCT_VERSION | 1638 | Another version of this product is already installed. Installation of this version cannot continue. To configure or remove the existing version of this product, use Add/Remove Programs in Control Panel. | 0x666 | 0x80070666 |
| ERROR_INVALID_COMMAND_LINE | 1639 | Invalid command line argument. Consult the Windows Installer SDK for detailed command-line help. | 0x667 | 0x80070667 |
| ERROR_INSTALL_REMOTE_DISALLOWED | 1640 | The current user is not permitted to perform installations from a client session of a server running the Terminal Server role service. | 0x668 | 0x80070668 |
| ERROR_SUCCESS_REBOOT_INITIATED | 1641 | The installer has initiated a restart. This message is indicative of a success. | 0x669 | 0x80070669 |
| ERROR_PATCH_TARGET_NOT_FOUND | 1642 | The installer cannot install the upgrade patch because the program being upgraded may be missing or the upgrade patch updates a different version of the program. Verify that the program to be upgraded exists on your computer and that you have the correct upgrade patch. | 0x66A | 0x8007066A |
| ERROR_PATCH_PACKAGE_REJECTED | 1643 | The patch package is not permitted by system policy. | 0x66B | 0x8007066B |
| ERROR_INSTALL_TRANSFORM_REJECTED | 1644 | One or more customizations are not permitted by system policy. | 0x66C | 0x8007066C |
| ERROR_INSTALL_REMOTE_PROHIBITED | 1645 | Windows Installer does not permit installation from a Remote Desktop Connection. | 0x66D | 0x8007066D |
| ERROR_PATCH_REMOVAL_UNSUPPORTED | 1646 | The patch package is not a removable patch package. Available beginning with Windows Installer version 3.0. | 0x66E | 0x8007066E |
| ERROR_UNKNOWN_PATCH | 1647 | The patch is not applied to this product. Available beginning with Windows Installer version 3.0. | 0x66F | 0x8007066F |
| ERROR_PATCH_NO_SEQUENCE | 1648 | No valid sequence could be found for the set of patches. Available beginning with Windows Installer version 3.0. | 0x670 | 0x80070670 |
| ERROR_PATCH_REMOVAL_DISALLOWED | 1649 | Patch removal was disallowed by policy. Available beginning with Windows Installer version 3.0. | 0x671 | 0x80070671 |
| ERROR_INVALID_PATCH_XML | 1650 | The XML patch data is invalid. Available beginning with Windows Installer version 3.0. | 0x672 | 0x80070672 |
| ERROR_PATCH_MANAGED _ADVERTISED_PRODUCT | 1651 | Administrative user failed to apply patch for a per-user managed or a per-machine application that is in advertise state. Available beginning with Windows Installer version 3.0. | 0x673 | 0x80070673 |
| ERROR_INSTALL_SERVICE_SAFEBOOT | 1652 | Windows Installer is not accessible when the computer is in Safe Mode. Exit Safe Mode and try again or try using System Restore to return your computer to a previous state. Available beginning with Windows Installer version 4.0. | 0x674 | 0x80070674 |
| ERROR_ROLLBACK_DISABLED | 1653 | Could not perform a multiple-package transaction because rollback has been disabled. Multiple-Package Installationscannot run if rollback is disabled. Available beginning with Windows Installer version 4.5. | 0x675 | 0x80070675 |
| ERROR_INSTALL_REJECTED | 1654 | The app that you are trying to run is not supported on this version of Windows. A Windows Installer package, patch, or transform that has not been signed by Microsoft cannot be installed on an ARM computer. | 0x676 | 0x80070676 |
| ERROR_SUCCESS_REBOOT_REQUIRED | 3010 | A restart is required to complete the install. This message is indicative of a success. This does not include installs where the ForceReboot action is run. | 0xBC2 | 0x80070BC2 |

Any installer that uses standard MSI technology will likely use these same error codes(i.e the Microsoft C++ redistributables (vcredist_x86.exe, vcredist_x64.exe)).