# TT2 - Database

_(Work-in-progress... please feel free to add your own thoughts, suggestions, ideas, etc...)_

This document provides further information as to the data and database schemas that Trophy Tracker 2 utilises. It also details the decisions/reasons/requirements regarding data and management thereof across the TT2 system.

## Database and Tables

SQLite will be used as the backend (BE) database, to store data in a relational model.

### Tables

#### Cars

The Cars table has a row for each vehicle.

| Field               | Type     | Description                                                          |
| :------------------ | :------- | :------------------------------------------------------------------- |
| \_id                | ObjectId | Id (auto-generated).                                                 |
| createdAt           | Date     | Entry creation date (in ISO string format).                          |
| updatedAt           | Date     | Entry updated date (in ISO string format).                           |
| trophyNumber        | Number   | The supposedly unique car number - 001-500 (UK), 01-50 (SWISS).      |
| numberOfViews       | Number   | The number of times that this car has been viewed.                   |
| targetMarket        | String   | The target market for this car, either "UK" or "SWISS".              |
| registrationDate    | Date     | Date of registration.                                                |
| colour              | String   | The car's main colour (standard is Capsicum Red).                    |
| vin                 | String   | Vehicle Identification Number (VIN).                                 |
| insuranceCategory   | String   | Insurance Category.                                                  |
| numberOfOwners      | Number   | Number of owners.                                                    |
| vrmOriginal         | String   | The original Vehicle Registration Mark (VRM/licence plate).          |
| vrmLastKnown        | String   | The last known Vehicle Registration Mark (VRM/licence plate).        |
| mileageRecorded     | Number   | The car's recorded (last known) mileage.                             |
| mileageRecordedDate | Date     | The date on which the car's recorded (last known) mileage was taken. |
| signatureItems      | Object   | The car's "signature items" (see SignatureItems object).             |
| hasBeenScrapped     | Boolean  | Whether or not this car has been scrapped.                           |
| scrappedDate        | Date     | Date on which the car was scrapped.                                  |

#### VRMChanges

The VRMChange object is used to record changes to the VRM (licence plate).

| Field      | Type     | Description                         |
| :--------- | :------- | :---------------------------------- |
| \_id       | ObjectId | Id (auto-generated).                |
| vehicleId  | ObjectId | Foreign key back into the Car table |
| changeDate | Date     | Date of VRM change.                 |
| vrmFrom    | String   | The ' changing from' VRM.           |
| vrmTo      | String   | The 'changing to' VRM.              |

#### SignatureItems

The SignatureItems object is used to record the presence of "signature items" for a vehicle. The signature items were items that set the Trophy apart from regular (non-Trophy) versions of the RS Clio. The Boolean type in MongoDB cannot store a null value (only true and false values) hence string values are used ("Y" = Yes, present), ("N" = No, missing), ("U" = Unknown). The notes field is provided for recording signature item specific notes.

| Field                   | Type     | Description                                                                 |
| :---------------------- | :------- | :-------------------------------------------------------------------------- |
| \_id                    | ObjectId | Id (auto-generated).                                                        |
| vehicleId               | ObjectId | Foreign key back into the Car table                                         |
| hasSachsDampers         | String   | Whether or not the car has the signature Sachs dampers.                     |
| hasRecaroTrendlineSeats | String   | Whether or not the car has the signature Recaro Trendline seats.            |
| hasV6Spoiler            | String   | Whether or not the car has the signature V6 roof spoiler.                   |
| hasTuriniWheels         | String   | Whether or not the car has the signature Trophy-spec Turini alloy wheels.   |
| notes                   | String   | General notes for recording signature item related information for the car. |

#### StoryHistory

The StoryHistoryEntry object is used to record a story (general update) at a point in time. Multiple stories can exist within a car's story history.

| Field     | Type     | Description                                                                        |
| :-------- | :------- | :--------------------------------------------------------------------------------- |
| \_id      | ObjectId | Id (auto-generated).                                                               |
| vehicleId | ObjectId | Foreign key back into the Car table                                                |
| date      | Date     | The date associated with this story.                                               |
| content   | String   | The story content. (Restrict to text-only or allow some basic styling, e.g. HTML?) |

#### LocationHistory

The LocationHistoryEntry object is used to record location information - e.g. country of residence, etc. TBC.

| Field     | Type     | Description                          |
| :-------- | :------- | :----------------------------------- |
| \_id      | ObjectId | Id (auto-generated).                 |
| vehicleId | ObjectId | Foreign key back into the Car table  |
| date      | Date     | The date associated with this entry. |

#### SaleHistory

The SaleHistoryEntry object is used to record sale (buying/selling) information.

| Field     | Type     | Description                          |
| :-------- | :------- | :----------------------------------- |
| \_id      | ObjectId | Id (auto-generated).                 |
| vehicleId | ObjectId | Foreign key back into the Car table  |
| date      | Date     | The date associated with this entry. |
| price     | Number   | Price at time of sale.               |
| mileage   | Number   | Mileage at time of sale.             |

#### ExternalLinks

The ExternalLinks object is used to capture links (URLs) to other sites that contain useful information related to a specific car. For example, links to car project threads on car sites, or links to online advertisements.

| Field       | Type     | Description                                                 |
| :---------- | :------- | :---------------------------------------------------------- |
| \_id        | ObjectId | Id (auto-generated).                                        |
| vehicleId   | ObjectId | Foreign key back into the Car table                         |
| title       | String   | A short title for the link.                                 |
| description | String   | A description of what can be found when following the link. |
| url         | String   | The website/resource URL.                                   |

## Entity Relationship Diagram (ERD)

```Mermaid
erDiagram
  CARS ||--o{ VRM_CHANGE : "should have"
  CARS ||--o{ SIGNATURE_ITEMS : "may have"
  CARS ||--o{ STORY_HISTORY : "may have"
  CARS ||--o{ LOCATION_HISTORY : "may have"
  CARS ||--o{ SALES_HISTORY : "may have"
  CARS ||--o{ EXTERNAL_LINKS : "may have"
  CARS ||--o{ IMAGES : "may have"
```
