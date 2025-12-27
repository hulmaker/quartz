# Roles

Application consist of several roles. Roles can be distinguished to customer and internal.

Check for usage made 28.2.2024 directly in production DB.

| Name                | Type      | Description                                                | Used      |
| ------------------- | ----      | ---------------------------------------------------------- | --------- |
| Property Manager    | Customer  | Allows customers to see data about their property.         | Yes  (45) |
| Property Marketing  | Customer  | Same as Property Manager with ability to write to CLV.     | Yes (158) |
| Property technicial | Customer  | Limited to sensor, entrance groups and owner mngmt.        | Yes   (9) |
| ic Administration   | Internal  | Administration access to all owners, properties and users. | Yes  (13) |
| Retail data only    | Internal  | ?? Somehow connected to "ruzovy slon" only                 | Yes   (3) |
| Helpdesk owner      | Internal  | ??                                                         | No        |

# Role & Rights

Each role has own description of defined rights.

TODO: Check and fill empty descriptions

| Name        | Description                                                    |
| ----------- | -------------------------------------------------------------- |
| ADMIN       |  Access to application administration.                         |
| USER        |  Access to operation over an user (add, edit, remove).         |
| PROP        |  Access to operation over a property (add, edit, remove).      |
| OWNER       |  Access to operation over an owner (add, edit, remove).        |
| SENSOR      |  Access to operation over a sensor (add, edit, remove).        |
| USER_PROP   |  ?? Acces to assigning user to a property.                     |
| SENSOR_DATA |  ??                                                            |
| REPORT      |  ??                                                            |
| ENTGRP      |  Access to operation over a entrance group (add, edit, remove).|
| OWNER_MGMT  |  ??                                                            |
| CLV         |  Access to operation over a city light (add, edit, remove).    |


| Role/Right          | ADMIN | USER | PROP | OWNER | SENSOR | USER_PROP | SENSOR_DATA | REPORT | ENTGRP | OWNER_MGMT | CLV |
| ------------------- | ----  | ---- | ---- | ----- | ------ | --------- | ----------- | ------ | ------ | ---------- | --- |
| Property Manager    | - | R | R | R | R | R | R | R | R | - | - |
| Property Marketing  | - | R | R | R | R | R | R | R | R | - | W |
| Property technicial | - | - | - | - | R | - | R | - | R | R | - |
| ic Administration   | W | W | W | W | W | W | R | R | W | W | W |
| Retail Data Only    | - | - | R | R | R | R | R | R | R | - | - | 
| Helpdesk owner      | - | - | - | - | R | - | - | - | - | R | - |

Where:
- R - read
- W - read + write
- '-' none

# Direct assigment

## User - Property

Application allows users with admin role assigne a property to an user.

## User - Report

Application allows users with admin role assigne a report to an user.

## User - Entrance Group

Application allows users with admin role assigne a entrance group to an user.