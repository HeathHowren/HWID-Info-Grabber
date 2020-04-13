# HWID Info Grabber

## Introduction

This project is an example of how computer components have hardware identifiers that can be used by developers to lock applications to specific computers. <br />
This code is from a [video](https://www.youtube.com/watch?v=78JToBCejdU) where I explain how to control distribution of applications and prevent piracy.

## Code Samples

Retrieving HDD information, the HDD serial is most commonly used for locking applications.
```cpp
	TCHAR volumeName[MAX_PATH + 1] = { 0 };
	TCHAR fileSystemName[MAX_PATH + 1] = { 0 };
	DWORD serialNumber = 0;
	DWORD maxComponentLen = 0;
	DWORD fileSystemFlags = 0;
	if (GetVolumeInformation(
		_T("C:\\"),
		volumeName,
		ARRAYSIZE(volumeName),
		&serialNumber,
		&maxComponentLen,
		&fileSystemFlags,
		fileSystemName,
		ARRAYSIZE(fileSystemName)))
	{
		std::cout << "Volume Name: " << volumeName << std::endl;
		std::cout << "HDD Serial: " << serialNumber << std::endl; 
		std::cout << "File System Type: " << fileSystemName << std::endl;
		std::cout << "Max Component Length: " << maxComponentLen << std::endl;
	}
```
Retrieving the computer name, this is easily changeable by the user.
```cpp
    	TCHAR computerName[MAX_COMPUTERNAME_LENGTH + 1];
	DWORD size = sizeof(computerName) / sizeof(computerName[0]);
	if (GetComputerName(
		computerName,
		&size))
	{
		std::cout << "Computer Name: " << computerName << std::endl;
	}
```
Retrieving the CPU hash.
```cpp
    int cpuinfo[4] = { 0, 0, 0, 0 }; //EAX, EBX, ECX, EDX
    __cpuid(cpuinfo, 0);
    char16_t hash = 0;
    char16_t* ptr = (char16_t*)(&cpuinfo[0]);
    for (char32_t i = 0; i < 8; i++)
    hash += ptr[i];
    std::cout << "CPU Hash: " << hash << std::endl;
```
