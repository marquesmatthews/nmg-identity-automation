# NMG Identity Automation With Powershell

PowerShell tooling for identity lifecycle management, built for
Northstar Medical Group.

## The Problem
Northstar did not have an automated way to track accounts belonging to former employees.
One employee was responsible for notifying IT whenever someone left the company. 
Once she retired, those notifications stopped, and some accounts went unnoticed for 102 days

A manual review found 23 inactive accounts and took 11 hours over four days. 
The process also could not identify accounts belonging to employees who left without being reported, 
contractors who were never added to payroll, or service accounts that were not assigned to actual employees.

## The Approach

Instead of relying on payroll records or employee paperwork, I used PowerShell to query Active Directory directly. 
I checked the last time each account authenticated with the domain controller. 
This gave me a way to identify accounts that had not been used recently without depending on employee records being updated or names matching across different systems.

## Tools

### Find-StaleAccounts.ps1

Identifies enabled accounts that have not authenticated within a given
number of days, including accounts that have never authenticated.
Exports a timestamped CSV plus a summary recording the exact query used.

    .\Find-StaleAccounts.ps1
    .\Find-StaleAccounts.ps1 -Days 30
    .\Find-StaleAccounts.ps1 -Days 180 -IncludeDisabled

| Parameter | Type | Default | Description |
|---|---|---|---|
| `-Days` | int | 90 | Days without authentication before an account is considered stale |
| `-ReportPath` | string | C:\Reports | Where reports are written |
| `-IncludeDisabled` | switch | off | Include disabled accounts in results |

**Output:** a timestamped CSV of findings, and a summary file recording
the question that produced them so the report can be reproduced.

## Repository Structure

    Scripts/        PowerShell tools
    Documentation/  Runbooks and process documentation
    Evidence/       Sample output and verification screenshots
    Logs/           Execution logs

## Environment

Windows Server with Active Directory Domain Services.
Requires the ActiveDirectory PowerShell module.

## About

Built during the TotalThreat 30-Day Challenge in a simulated
healthcare environment. Northstar Medical Group is fictional.

Author:Marques Matthews
