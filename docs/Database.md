# TT2 - Database

_(Work-in-progress... please feel free to add your own thoughts, suggestions, ideas, etc...)_

This document provides further information as to the data and database schemas that Trophy Tracker 2 utilises. It also details the decisions/reasons/requirements regarding data and dataa management across the TT2 system.

## Database and Collections

MongoDB will be used as the backend (BE) database, the database name being "tt2".

### Collections

TT2 has the following collections:

| Name  | Description                                                              |
| :---- | :----------------------------------------------------------------------- |
| cars  | This collection stores per vehicle data.                                 |
| users | This collection stores users and their privileges (admin, editors, etc). |

### Collection - cars

#### CarSchema

The CarSchema represents a single vehicle.

| Field               | Type     | Description                                                                              |
| :------------------ | :------- | :--------------------------------------------------------------------------------------- |
| \_id                | ObjectId | Id (auto-generated).                                                                     |
| createdAt           | Date     | Document creation date (auto-generated via Mongoose schema #timestamps option).          |
| updatedAt           | Date     | Document updated date (auto-generated via Mongoose schema #timestamps option).           |
| trophyNumber        | Number   | The supposedly unique car number - 001-500 (UK), 01-50 (SWISS).                          |
| numberOfViews       | Number   | The number of times that this car has been viewed.                                       |
| targetMarket        | String   | The target market for this car, either "UK" or "SWISS".                                  |
| registrationDate    | Date     | Date of registration.                                                                    |
| colour              | String   | The car's main colour (standard is Capsicum Red).                                        |
| vin                 | String   | Vehicle Identification Number (VIN).                                                     |
| vrmOriginal         | String   | The original Vehicle Registration Mark (VRM/licence plate).                              |
| vrmLastKnown        | String   | The last known Vehicle Registration Mark (VRM/licence plate).                            |
| vrmHistory          | Array    | The car's VRM history (see VRMChange object).                                            |
| mileageRecorded     | Number   | The car's recorded (last known) mileage.                                                 |
| mileageRecordedDate | Date     | The date on which the car's recorded (last known) mileage was taken.                     |
| signatureItems      | Array    | The car's "signature items" (see SignatureItems object).                                 |
| hasBeenScrapped     | Boolean  | Whether or not this car has been scrapped.                                               |
| scrappedDate        | Date     | Date on which the car was scrapped.                                                      |
| images              | Array    | Images of the car (String array, specified as relative/local URL?).                      |
| storyHistory        | Array    | General updates (stories) for this car (see StoryHistoryEntry object).                   |
| locationHistory     | Array    | Location information for this car (see LocationHistoryEntry object).                     |
| saleHistory         | Array    | Sale (buying/selling) information for this car (see SaleHistoryEntry object).            |
| externalLinks       | Array    | External links (URLs) for additional information for this car (see ExternalLink object). |

#### VRMChange Object

The VRMChange object is used to record changes to the VRM (licence plate).

| Field      | Type   | Description               |
| :--------- | :----- | :------------------------ |
| changeDate | Date   | Date of VRM change.       |
| vrmFrom    | String | The ' changing from' VRM. |
| vrmTo      | String | The 'changing to' VRM.    |

#### SignatureItems Object

The SignatureItems object is used to record the presence of "signature items" for a vehicle. The signature items were items that set the Trophy apart from regular (non-Trophy) versions of the RS Clio. The Boolean type in MongoDB cannot store a null value (only true and false values) hence string values are used ("Y" = Yes, present), ("N" = No, missing), ("U" = Unknown). The notes field is provided for recording signature item specific notes.

| Field                   | Type   | Description                                                                 |
| :---------------------- | :----- | :-------------------------------------------------------------------------- |
| hasSachsDampers         | String | Whether or not the car has the signature Sachs dampers.                     |
| hasRecaroTrendlineSeats | String | Whether or not the car has the signature Recaro Trendline seats.            |
| hasV6Spoiler            | String | Whether or not the car has the signature V6 roof spoiler.                   |
| hasTuriniWheels         | String | Whether or not the car has the signature Trophy-spec Turini alloy wheels.   |
| notes                   | String | General notes for recording signature item related information for the car. |

#### StoryHistoryEntry Object

The StoryHistoryEntry object is used to record a story (general update) at a point in time. Multiple stories can exist within a car's story history.

| Field   | Type   | Description                                                                        |
| :------ | :----- | :--------------------------------------------------------------------------------- |
| date    | Date   | The date associated with this story.                                               |
| content | String | The story content. (Restrict to text-only or allow some basic styling, e.g. HTML?) |

#### LocationHistoryEntry Object

The LocationHistoryEntry object is used to record location information - e.g. country of residence, etc. TBC.

| Field | Type | Description                          |
| :---- | :--- | :----------------------------------- |
| date  | Date | The date associated with this entry. |

#### SaleHistoryEntry Object

The SaleHistoryEntry object is used to record sale (buying/selling) information.

| Field | Type | Description                          |
| :---- | :--- | :----------------------------------- |
| date  | Date | The date associated with this entry. |

#### ExternalLinks Object

The ExternalLinks object is used to capture links (URLs) to other sites that contain useful information related to a specific car. For example, links to car project threads on car sites, or links to online advertisements.

| Field       | Type   | Description                                                 |
| :---------- | :----- | :---------------------------------------------------------- |
| title       | String | A short title for the link.                                 |
| description | String | A description of what can be found when following the link. |
| url         | String | The website/resource URL.                                   |

### Collection - users

TBD.
