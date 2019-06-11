# CBD - Global Bounded Contexts

Core Banking Design (CBD) commonly used schema definitions. Please raise a support ticket in [APIGW JIRA project](https://jira.dss.ext.national.com.au/projects/APIGW/) to add more models

 Alternatively you can always create a pull request as this is just a markdown file.

<a name="home"/>

##### Table of Contents  
[applicant](#applicant)  
[financialProfile](#financialProfile)  
[facility](#facility)  
[property](#property)  
  

---
<a name="applicant"/>

[up](#home) 

![applicant](applicant.png)


# Applicant Models 
## address

```yaml
type: object
properties:
  type:
    type: string
    description: type of address.
    pattern: '^[a-zA-Z_ ]*$'
  startDate:
    description: Start Date of address residence. Type requires format of YYYY-MM-DD.
    allOf:
      - $ref: 'ISODate.yaml'
  endDate:
    description: End Date of address residence. Type requires format of YYYY-MM-DD.
    allOf:
      - $ref: 'ISODate.yaml'
  purpose:
    type: string
    description: Purpose of address (eg. Work)
  occupancyType:
    type: string
    description: Occupancy Type of address (eg. Boarding, Company Owned, Owner Mortgage).
    pattern: '^[a-zA-Z_ ]*$'
  propertyName:
    type: string
    description: Building Name.
  unitType:
    type: string
    description: Building Type (eg. APT).
    pattern: '^[a-zA-Z_ ]*$'
  lotNumber:
    type: string
    description: Lot Number.
  unitNumber:
    type: string
    description: Unit Number.
  levelNumber:
    type: string
    description: Floor Number.
  streetNumber:
    type: string
    description: Address Number in street.
  streetName:
    type: string
    description: Street Name
  streetType:
    type: string
    description: Type of street (eg. RD, ST).
    pattern: '^[a-zA-Z_ ]*$'
  streetTypeSuffix:
    type: string
    description: Street Type Suffix (eg. CN).
    pattern: '^[a-zA-Z_ ]*$'
  townSuburb:
    type: string
    description: City.
  postcode:
    type: string
    description: Postcode.
  poBoxNumber:
    type: string
    description: Post Office Box Number.
  poBoxDeliveryType:
    type: string
    description: Post Office Box Delivery Type.
    pattern: '^[a-zA-Z_ ]*$'
  state:
    type: string
    description: State Code (eg. VIC).
    pattern: '^[a-zA-Z_ ]*$'
  country:
    $ref: 'ISOCountryCode.yaml'
```
## ~~applicantOwnership~~

```yaml
type: object
properties:
  applicantId:
    type: string
    description: >-
      Id of applica	nt who has part/full ownership. Must match an id entered for one of the applicants in the Submission.
  ownershipPercentage:
    $ref: 'PositivePercentage.yaml'
```

## attestations
```yaml
type: object
properties:
  isAmlAttested:
    type: boolean
    description: >-
      True if the applicant has fulfilled their AML attestation requirements.
  isUsTaxObligationCompleted:
    type: boolean
  isOtherTaxObligationCompleted:
    type: boolean
```

## customerId
```yaml
type: object
required:
  - idType
  - value
properties:
  idType:
    type: string
    description: Type of customer id
    enum:
      - MEID
  value:
    type: string
    description: >-
      Actual customer id matching the defined idType. At least one character is required.
    pattern: '^[0-9]*$'
```

## email
```yaml
type: object
properties:
  address:
    type: string
    description: Email address 
```

## employment 
```yaml
type: object
properties:
  industryClassificationCode:
    type: string
    description: occupation status (e.g 30 for Employment, 28 for Students, 29 for Not in Workfoce)
    pattern: '^[0-9]*$'
  type:
    type: string
    description: Employment type (e.g Salaried, Self employed, Others)
    pattern: '^[a-zA-Z_ ]*$'
  startDate:
    description: Employment start date in YYYY-MM-DD format.
    allOf:
      - $ref: 'ISODate.yaml'
  status:
    type: string
    description: Employment status (e.g Full time, Part time, Casual, etc.)
    pattern: '^[a-zA-Z_ ]*$'
  endDate:
    description: Employment end date in YYYY-MM-DD format.
    allOf:
      - $ref: 'ISODate.yaml'
  occupationClassificationCode:
    type: string
    description: Occupation code (e.g O3493, O221, O2293, etc)
    pattern: '^O[0-9]*$'
  organisationName:
    type: string
    description: Organisation name
  jobTitle:
    type: string
    description: Job title
  isPrimary:
    type: boolean
    description: Indicates if it is the primary employment. When applicant has multiple employments, only one employment can be flagged as primary.
  address:
    $ref: 'Address.yaml'
```

## identification
```yaml
type: object
properties:
  type:
    type: string
    description: Type of identification (eg. DRIVERS_LICENCE).
    pattern: '^[a-zA-Z_ ]*$'
  idNumber:
    type: string
    description: ID Number for identification.
    pattern: '^[0-9a-zA-Z]*$'
  issuedState:
    type: string
    description: State Code of where identification was issued (eg.VIC).
    pattern: '^[a-zA-Z_ ]*$' 
```

## phone
```yaml
type: object
properties:
  type:
    type: string
    description: Phone Type
    enum:
      - HOME
      - WORK
      - MOBILE
      - INTERNATIONAL
  countryCode:
    type: string
    description: Country Code of phone number (eg. 61).
    pattern: '^[0-9]*$'
  areaCode:
    type: string
    description: Area Code of phone number (eg. 03).
    pattern: '^[0-9]*$'
  phoneNumber:
    type: string
    description: Actual phone number without any country or area code prefixes if
      applicable (eg. 95551234).
    pattern: '^[0-9]*$'
  isPrimary:
    type: boolean
    description: Indicator for whether this phone number is the preferred point of
      contact.
```

## taxObligation
```yaml
type: object
properties:
  taxCountry:
    type: string
    description: Country Code (eg. AU).
    pattern: '^[A-Z]{2}$'
  noTinReasonCode:
    type: string
    description: No TIN reason code (eg. A, B, C) 
    pattern: '^[A-Z]*$'
  noTinReasonExplanation:
    type: string
    description: No TIN explanation
    maxLength: 500
  taxResidencyBankNotifiedEndDate:
    description: Tax residency bank notified end date in YYYY-MN-DD format.
    allOf:
      - $ref: 'ISODate.yaml'
  taxIdNumber:
    type: string
    description: Tax identification number 
```

## verificationDocument
```yaml
type: object
properties:
  kycDocumentNo:
    type: string
    pattern: '^[0-9a-zA-Z\+\-\@\ \$\!\%\&\(\)\*\.\/\#\=\:\;\?\,\''\[\]\^\_]*$'
    maxLength: 50
  kycDocumentType:
    type: string
    enum:
      - PASSPORT
      - MEDICARE
      - DRIVERS_LICENCE
      - RESIDENCY_VISA
  kycCountryOfIssue:
    type: string
    description: Applicable for Residency Visa only.
    pattern: '^[0-9a-zA-Z\+\-\@\ \$\!\%\&\(\)\*\.\/\#\=\:\;\?\,\''\[\]\^\_]*$'
    maxLength: 3
  kycDocumentStateOfIssue:
    type: string
    description: Applicable for Drivers License document only.
    enum:
      - NSW
      - VIC
      - WA
      - QLD
      - TAS
      - ACT
      - NT
  kycDocumentCardColour:
    type: string
    description: Medicare Card Colour. Applicable for Medicare document only.
    enum:
      - B
      - G
      - Y
  kycDocumentIndividualRefNo:
    type: string
    description: >-
      Individual reference number on their Medicare card. (1 - 9).
      Applicable for Medicare document only.
    pattern: '^[1-9]$'
  kycDocumentIssueDate:
    type: string
    pattern: '^[0-9a-zA-Z\+\-\@\ \$\!\%\&\(\)\*\.\/\#\=\:\;\?\,\''\[\]\^\_]*$'
    maxLength: 50
    description: Document Issue Date
  kycDocumentExpiryDate:
    type: string
    pattern: '^[0-9a-zA-Z\+\-\@\ \$\!\%\&\(\)\*\.\/\#\=\:\;\?\,\''\[\]\^\_]*$'
    maxLength: 50
    description: >-
      Document Expiry Date. Passport - DD/MM/YYYY. Medicare - The expected format for regular green Medicare cards is MM/YYYY, and for blue and yellow Medicare cards, the expected format is DD/MM/YYYY.
```
---

<a name="financialProfile"/>

[up](#home) 

# financialProfile 
## asset
```yaml
type: object
properties:
  type:
    type: string
    description: Asset Type code (e.g 1016 = Car, 1001 = Home Contents, etc)
    pattern: '[A-Za-z0-9]*$'
  typeDescription:
    type: string
    description: Asset type description (e.g Car, Home Contents, etc)
  value:
    $ref: 'PositiveAmount.yaml'
  ownershipPercentage:
    $ref: 'PositivePercentage.yaml'
  serialNumber:
    type: integer
    maximum: 999
    minimum: 0
    description: TODO - what is this for?.
  carMake:
    type: string
    description: Make of car. Should only use if asset is of type Car.
  carModel:
    type: string
    description: Model of car. Should only use if asset is of type Car.
  carYearOfManufacture:
    type: string
    pattern: '^[1-2][0-9]{3}$'
    description: Year of manufacture of car. Should only use if asset is of type Car.
  additionalDetails:
    type: string
    description: Freeform text of any additional details related to this asset.
```

## consent
```yaml
type: object
properties:
  level:
    type: string
    description: >-
      Level of consent (eg. APPLICANT, CONTINUE_APPLICATION_ONLINE,
      GUARANTOR, CREDIT_ASSESSMENT, PRODUCT_TERMS, BUREAUCONSENT).
    pattern: '^[A-Z_ ]*$'
  type:
    type: string
    description: 'Type of consent (eg. ONLINE, WRITTEN, VERBAL).'
    pattern: '^[A-Z_ ]*$'
  isAvailable:
    type: boolean
    description: A flag to indicate if the consent is available.
```

## currentPositionAsset
```yaml
type: object
properties:
  type:
    type: string
    description: Asset Type code (e.g 42001 = NAB Saving Accounts).
    pattern: '[A-Za-z0-9]*$'
  typeDescription:
    type: string
    description: Type description of asset (eg. NAB Savings Account).
  value:
    $ref: 'Amount.yaml'
  ownershipPercentage:
    $ref: 'PositivePercentage.yaml' 
  serialNumber:
    type: integer
    maximum: 999
    minimum: 0
    description: TODO - what is this for?
  isExisting:
    type: boolean
    description: True if this asset currently exists.
  accountNumber:
    type: string
    description: Account number of asset.
  financialInstitutionName:
    type: string
    description: Name of bank/financial institution of the asset. 
```

## currentPositionLiability
```yaml
type: object
properties:
  type:
    type: string
    description: Liability Type code (eg. 42004).
    pattern: '[A-Za-z0-9]*$'
  typeDescription:
    type: string
    description: Type description of liability (eg. NAB  Credit Card).
  originalAmount:
    $ref: 'PositiveAmount.yaml'
  outstandingBalance:
    $ref: 'Amount.yaml'
  ownershipPercentage:
    $ref: 'PositivePercentage.yaml'
  serialNumber:
    type: integer
    maximum: 999
    minimum: 0
    description: TODO - what is this for?
  isExisting:
    type: boolean
    description: True if this liability currently exists.
  accountNumber:
    type: string
    description: Account number of the liability.
  financialInstitutionName:
    type: string
    description: Name of bank/financial institution of the liability.
  newLimit:
    $ref: 'PositiveAmount.yaml'
  newRepayment:
    $ref: 'PositiveAmount.yaml'
  currentRepayment:
    $ref: 'PositiveAmount.yaml'
  repaymentFrequency:
    type: string
    description: Repayment frequency of the liability (eg. Monthly).
    pattern: '^[a-zA-Z_ ]*$'
  repaymentType:
    type: string
    description: Repayment type of the liability (eg. Interest only).
    pattern: '^[a-zA-Z_ ]*$'
  interestRate:
    $ref: 'PositivePercentage.yaml'
  loanEndDate:
    description: >-
      Loan end date of the liability. As per type, must be in YYYY-MM-DD
      format.
    allOf:
      - $ref: 'ISODate.yaml'
  futureAction:
    type: string
    description: Future action for this liability (eg. Limit increase).
  additionalDetails:
    type: string
    description: Freeform text of any additional details related to this liability.
  interestOnlyEndDate:
    description: >-
      End date for the interest only component of the liability. As per
      type, must be in YYYY-MM-DD format.
    allOf:
      - $ref: 'ISODate.yaml'
```

## declaration
```yaml
type: object
properties:
  type:
    type: string
    description: >-
      Declaration type. Current allowed values
      * DIFFICULTY_IN_PAST_REPAYMENTS
      * FORESEE_CIRCUMSTANCES_CHANGE
      * PAST_BANKRUPTCY
      * PAST_LEGAL_PROCEEDINGS
    pattern: '^[A-Z_]*$'
  status:
    type: string
    description: Declaration status (true, false, or NA)
  comments:
    type: string
    description: Additional comments 
```

## expense
```yaml
type: object
properties:
  type:
    type: string
    description: Expense type code (e.g 9017 = General Living Expense, 1111 = Food, etc)
    pattern: '[A-Za-z0-9]*$'
  typeDescription:
    type: string
    description: Expense type description (e.g General Living Expense, Food, etc)
  amount:
    $ref: 'PositiveAmount.yaml'
  frequency:
    type: string
    description: Frequency of which expense is incurred (e.g. Monthly).
    pattern: '^[a-zA-Z_ ]*$'
  ownershipPercentage:
    $ref: 'PositivePercentage.yaml'
  serialNumber:
    type: integer
    maximum: 999
    minimum: 0
    description: TODO - what is this for?.
 
```

## income
```yaml
type: object
properties:
  type:
    type: string
    description: Income type code (e.g 3001 = Bonus, 3002 = Government Benefits, etc)
    pattern: '[A-Za-z0-9]*$'
  typeDescription:
    type: string
    description: Income type description, (e.g Bonus, Government Benefits, etc)
  grossAmount:
    $ref: 'PositiveAmount.yaml'
  netAmount:
    $ref: 'PositiveAmount.yaml'
  frequency:
    type: string
    description: Income frequency (e.g Daily, Weekly, Fortnightly, etc)
    pattern: '^[a-zA-Z_ ]*$'
  ownershipPercentage:
    $ref: 'PositivePercentage.yaml'
  serialNumber:
    type: integer
    maximum: 999
    minimum: 0
    description: TODO - what is this for?.
```
---

<a name="facility"/>

[up](#home) 

# Facility 

## funding
```yaml
type: object
properties:
  lvr:
    $ref: 'PositivePercentage.yaml'
  lmi:
    $ref: 'PositiveAmount.yaml'
  governmentCharges:
    type: array
    description: Array of all government charges that apply to this facility.
    items:
      type: object
	  properties:
		  type:
		    type: string
		    description: 'Enum type of government charges (e.g Stamp Duty, Title Search Fee)'
		    pattern: '^[a-zA-Z_ ]*$'
  amountCharged:
    $ref: 'PositiveAmount.yaml'
  customerContributions:
    type: array
    description: Array of all customer contributions that apply to this facility.
    items:
    type: object
	properties:
	  type:
	    type: string
	    description: 'Enum type of customer contribution (e.g Deposit, Savings, Other)'
	    pattern: '^[a-zA-Z_ ]*$'
  amountContributed:
    $ref: 'PositiveAmount.yaml'
```

## limitIncrease
```yaml
type: object
properties:
  collateralId:
    type: string
    description: Collateral Id of system of record (e.g OBP)
  accountDetails:
    type: object
    properties:
      bsb:
        type: string
        pattern: '^[0-9]{6}$'
      accountNumber:
        type: string
        pattern: '^(\d*[1-9]\d*)$'
  limitIncreasePurposeType:
    type: string
  limitIncreasePurposeCode:
    type: string
```

## offer
```yaml
type: object
properties:
  productCode:
    type: string
    description: Product Code for offer (eg. NHL001).
  relatedApplicants:
    type: object
    properties:
      applicantId:
        type: string
        description: >-
          Id of applicant who is associated with this offer. Must match an id
          entered for one of the applicants Submission.
  isPrimaryApplicant:
    type: boolean
    description: >-
      True if the related applicant is the primary applicant for the offer in the Submission.
  relatedPurchaseProperties:
    type: object
    description: Product Code for offer (eg. NHL001).
    properties:
      purchasePropertyId:
        type: string
        description: >-
          Id of purchase property that is associated with this offer. Must match
          an id entered for one of the purchase properties in the Submission.
  repaymentScheduleDetails:
    type: object
    properties:
      scheduleCode:
        type: string
        description: Determines the stages of repayment requested by the user
      stageDetails:
        type: object
        properties:
          repaymentType:
            type: string
            description: Options on how the refinance is done. i.e. interest + principal only
          stageTermYears:
            type: integer
            minimum: 0
            description: How many years the users wants to refinance for that particular type
          stageTermMonths:
            type: integer
            minimum: 0
            maximum: 11
            description: >-
              How many months on top of year the users wants to refinance for that
              particular type
          frequency:
            type: string
            description: Frequency of repayment requested
      fixedTermRate:
        type: object
        properties:
          numberOfYears:
            type: integer
            minimum: 0
            description: 'fixed rate term, years requested'
          numberOfMonths:
            type: integer
            minimum: 0
            maximum: 11
            description: 'fixed rate term, months requested on top of years'
```

## loanDetail
```yaml
type: object
properties:
  loanPurposeType:
    type: string
    description: Loan Purpose Type for facility (eg. PURCHASE_INVESTMENT).
    pattern: '^[A-Z_]*$'
  loanPurposeCode:
    type: string
    description: Loan Purpose Code for facility (eg. 039).
    pattern: '^[0-9]*$'
  loanAmount:
    $ref: 'PositiveAmount.yaml'
  loanTermYears:
    type: integer
    minimum: 0
    description: >-
      Number of years of requested loan term. NB. Integer type, not
      IntegerString. No fractions.
  loanTermMonths:
    type: integer
    minimum: 0
    maximum: 11
    description: >-
      Number of months of requested loan term. 
      Must be a whole number between 0 and 11 inclusive (eg.
      12 months should be expressed as 0 in this field and 1 in loanTermYears). 
```

## variant
```yaml
type: object
properties:
  type:
    type: string
    description: >-
      Enum type of loan variant that may or may not apply to facility (eg. Rural, Defence).
  value:
    type: boolean
    description: True if this loan variant applies to the facility.
```
---
<a name="property"/>

[up](#home) 

# Property 

## collateral
```yaml
type: object
properties:
  subCategoryCode:
    type: string
    description: 'Type of asset (eg. Apartment, Townhouse, Term Deposit).'
    pattern: '^[a-zA-Z_ ]*$'
  description:
    type: string
  contractOfSaleValue:
    $ref: 'PositiveAmount.yaml'
  ownerEstimatedValue:
    $ref: 'PositiveAmount.yaml'
  occupancyType:
    type: string
    description: Occupancy type of property collateral (e.g Boarding, Company, Owned, etc).
    pattern: '^[a-zA-Z_ ]*$'
  isPrimaryResidence:
    type: boolean
    description: True if property collateral is used as primary residence.
  numBedrooms:
    type: integer
    minimum: 0
    description: Number of bedrooms in the property
  numBathrooms:
    type: integer
    minimum: 0
    description: Number of bathroom in the property
  applicantOwnerships:
    type: object
    description: Array of all applicant ownership levels for specfic collateral.
    properties:
      applicantId:
        type: string
        description: >-
          Id of appliacnt who has part/full ownership. Must match an id entered
          for one of the applicants in the Submission.
      ownershipPercentage:
        $ref: 'PositivePercentage.yaml'
  address:
    $ref: 'Address.yaml'
```

## purchaseProperty
```yaml
type: object
required:
  - id
properties:
  id:
    type: string
    description: >-
      Unique (in request) arbitrary ID of purchase property for referential
      purposes (ie. other objects in request will use this id to link to
      this property).
  isPrimaryResidence:
    type: boolean
    description: True if this property is to be the primary residence.
  purchasePrice:
    $ref: 'PositiveAmount.yaml'
  description:
    type: string
    description: Free-form text description of property.
  address:
    $ref: 'Address.yaml'
```
