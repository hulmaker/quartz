# Vocabulary

It is important that everybody involved on project use same words for same things. Let's start with putting used terms on one place and then let's unite them.

| iC Cloud                  | Monitoring     | Footfall                                      | Sales             | Technicians | Description                                                                                                           |
| ------------------------- | -------------- | --------------------------------------------- | ----------------- | ----------- | --------------------------------------------------------------------------------------------------------------------- |
| Customer (formerly Owner) | Customer/Group |                                               | Customer          |             | Name of the mother company name. For example 'Ahold' or 'OC Nisa'.                                                    |
| Property                  | Building       |                                               | Property/Building |             | Identification of one specific place. For example 'Albert Blansko' or 'OC Nisa'.                                      |
| Sensor                    | Device         |                                               | Sensor            |             | Physical HW device covering one concrete area of interest.                                                            |
| Device                    |                |                                               | Device            |             | Physical HW device used by a user to access iC Cloud app.                                                             |
|                           | Area           | area=AreaDefinition(...)/camera_mask (type 1) |                   |             | An area in the scene where a detection can occur                                                                      |
| Entrance                  | Entrance       | Entrance/camera_mask (type 2)                 | Zona              |             | Physical place of interest as is a concrete entrance 'door' into a concrete shop.                                     |
| Entrance Groups           |                |                                               | Entrance Groups   |             | Group of several entrances covering logical entity. For example 2 entrances to a concrete shop.                       |
|                           | Config         | Camera config                                 |                   |             | Yaml configuration file necessary to run FF that descibes the sceen in which the sensor is situated                   |
| User                      | User           |                                               | User              |             | Real person identified by his/her email. In combination with password garant access to application(s).                |
| Role & Right              | Role           |                                               |                   |             | Access of a user to particular parts of application(s) is defined by role and rights. Each role has different rights. |
|                           | Placement      |                                               |                   |             | A virtual sensor that can be linked to a physical sensor. It is a bag of data / plans / designs for installation.     |


# Remarks
 * The term "Entrance group" does not accurately represent a collection of entrances forming a logical entity. Instead, it refers to an aggregation of footfall measurements associated with multiple entrances in specified directions. Therefore, we suggest renaming this concept to **FF Aggregation group** for clarity.
 * The term Entrance does not accurately represent the concept. I propose area
