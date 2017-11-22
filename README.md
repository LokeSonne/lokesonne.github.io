## Create order POST /api/seek/v1/orders

Creates order, and optionally, shares order with JobAG. Once an order is shared it can never be unshared. Similarly, any non-shared order can never become a shared order.

Level | Seek | JobAG | Data type | Gets value from | Required | comment
---|---|---|---|---|---|---
1 | Id | CompanyRecruitmentIdentifier | guid | server | yes |
1 | Title | CompanyRecruitmentTitle | string (1-100) | client | yes |
1 | OrderTitleTypeId | OccupationId | string (1-100) | server | no | If Title matches an OrderTitleType where OrderTitleType.DiscoAM08 is not null, then use OrderTitleType.Id
1 | Description | CompanyRecruitmentJobDescription | string (1-2000) | client | yes |
1 | OrderTypeId | CompanyRecruitmentTypeIdentifier | int | client | yes | If isShared = true, then this must always be = 1. Is stored in Seek as int, but sent to JobAG as string
1 | OrderStatusTypeId | CompanyRecruitmentStatusTypeIdentifier | int | server | yes | On create is always = 1 (Open)
1 | StartDate | CompanyRecruitmentStartDate | Date | client | yes | default = Created
1 | EndDate | N/A | Date | client | no |
1 | N/A | CompanyRecruitmentPeriod | int | server | no | Calculated as EndDate - StartDate (both included)
1 | Deadline | CompanyRecruitmentValidToDate | Date | client | no |
1 | OrderResponseTypeId | CompanyRecruitmentRespondTypeIdentifier | int | client | no | 
1 | MaxNumberOfCandidates | MaximumNumberOfResponses | int | client | no |
1 | N/A | WeeklyWorkTimeTypeIdentifier | int | server | no | if MaxHoursPerWeek = 37 then 1 else 2
1 | MinHoursPerWeek | N/A | int | client | yes |
1 | MaxHoursPerWeek | HoursPerWeek | int | client | yes |
2 | CompanyId | N/A | int | client | yes | client provides ProductionUnitIdentifier
1 | Company | CompanyRecruitmentProvider | object | server | yes | from CompanyId 
2 | N/A | CVRnumberIdentifier | string (8) | client | yes | from CompanyId 
2 | N/A | ProductionUnitIdentifier | string (10) | client | yes | from CompanyId 
1 | WorkLocation | CompanyRecruitmentLocationAddress | string (10) | client | no |
2 | BuildingName | MailDeliverySublocationIdentifier | string (1-34) | client | no |
2 | StreetName | StreetName | string (1-40) | client | yes |
2 | HouseNumber | StreetBuildingIdentifier | string | client | yes |
2 | Floor | FloorIdentifier | string | client | no |
2 | Suite | SuiteIdentifier | string (1-4) | client | no |
2 | AreaCode | PostCodeIdentifier | string [0-9]{4} | client | yes |
2 | City | DistrictName | string (1-20) | client | yes |
2 | CountryTypeId | N/A | int | client | yes |
2 | N/A | CountryIdentificationCode | string (1-20) | client | yes | mapped from CountryType
2 | N/A | BaseType | string (1-20) | client | yes | Always 'ISO 3166 standard, alpha 2' on create
1 | Contact | ContactInformation | object | client | no | Contact is saved as text - no link to Contact table
2 | FirstName | PersonGivenName | string (1-34) | client | yes |
2 | LastName | PersonSurnameName | string (1-34) | client | yes |
2 | Telephone | TelephoneNumberIdentifier | string (1-34) | client | no |
2 | Email | EmailAddressIdentifier | string (1-34) | client | no |
1 | OrganizationId | N/A | int | server | yes | User's organization. If order is from JobAG, then organizationId = 31 (external)
1 | ResponsibleJobcenterCode | ResponsibleJobcenterCode | int | server | yes | From organization table
1 | IsCreatedByCompany | IsCreatedByCompany | boolean | server | no | always = false on create
1 | JobAdId | JobAdId | int | client | no |
1 | CompanyWantsEmailNotification | WantsEmailNotification | boolean | client | no |
1 | Owner | RecruitmentCaseWorker | object | client | yes |
2 | AuthorityStructure | AuthorityStructure | object | client | yes |
3 | AuthorityCode | AuthorityCode | string | client | yes |
3 | OrganisationTypeIdentifier | OrganisationTypeIdentifier | string | client | yes |
2 | CaseWorker | CaseWorker | object | client | yes |
3 | FirstName | CaseWorkerGivenName | string (1-40) | client | yes |
3 | LastName | CaseWorkerSurname | string (1-34) | client | yes |
3 | Email | EmailAddressIdentifier | string (1-255) | client | yes |
3 | identifier | CaseWorkerIdentifier | string | client | yes |
1 | RecruitmentCaseWorkerAllowed | RecruitmentCaseWorkerAllowed | Boolean | client | yes |

JobAG fields and objects not used

Level | Seek | JobAG | Data type | Gets value from | Required | comment
---|---|---|---|---|---|---
1 | N/A | CompanyRecruitmentLocationName | string (1-500) | client | no |
2 | N/A | DistrictSubdivisionIdentifier | string (1-34) | client | no |
2 | N/A | PostOfficeBoxIdentifier | int | client | no |
2 | N/A | PersonMiddleName | string (1-40) | client | no |
3 | N/A | CaseWorkerMiddleName | string (1-40) | client | no |
1 | N/A | InternalAuthorityComment | string (1-2000) | client | no |
1 | N/A | PrimaryRecruitmentAuthorities | object | client | no |
