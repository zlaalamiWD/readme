---
title: Fill Request fields
deprecated: false
hidden: true
metadata:
  robots: index
---
## Fill Request Message

<br />

| Field         | Type     | CharacterLimit | Required/Optional | Notes                                    |
| :------------ | :------- | :------------- | :---------------- | :--------------------------------------- |
| MessageId     | String   | 1015           | R                 | Unique id in partner system              |
| OrderNumber   | String   | 25             | R                 | Order Number value in the partner system |
| Pharmacy      | Object   |                | R                 |                                          |
| Patient       | Object   |                | R                 |                                          |
| Prescriptions | Object   |                | R                 | Array – 1 or more prescriptions          |
| Shipping      | Object   |                | R                 |                                          |
| CustomData    | KeyValue |                | O                 | Array – 1 or more Key Values pairs       |

### Pharmacy

| Field   | Type   | CharacterLimit | Required/Optional | Notes                                  |
| :------ | :----- | :------------- | :---------------- | :------------------------------------- |
| Name    | String | 100            | R                 | Name of the originating pharmacy       |
| NPI     | String | 10             | R                 | NPI value for the originating pharmacy |
| Address | Object |                | R                 |                                        |

### Patient

<Table align={["left","left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Type
      </th>

      <th>
        CharacterLimit
      </th>

      <th>
        Required/Optional
      </th>

      <th>
        Notes
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Id
      </td>

      <td>
        String
      </td>

      <td>
        25
      </td>

      <td>
        R
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        AccountNumber
      </td>

      <td>
        String
      </td>

      <td>
        25
      </td>

      <td>
        O
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        FirstName
      </td>

      <td>
        String
      </td>

      <td>
        50
      </td>

      <td>
        R
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        LastName
      </td>

      <td>
        String
      </td>

      <td>
        50
      </td>

      <td>
        R
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        preferredLanguage
      </td>

      <td>
        String
      </td>

      <td>
        3
      </td>

      <td>
        R
      </td>

      <td>
        Only Valid list of ISO-3digit language codes are accepted:                              ENG English                                           SPA Spanish                                         RUS Russian

        SOM SomaliARA ArabicZHO Chinese(Simplified)VIE Vietnamese
        FAS Farsi
        FRA French
        DEU German
        HMN Hmong
        KOR Korean
        RON Romanian
        SWA Swahili
        MYA Burmese
        NEP Nepali
        AMH Amharic
        PST Pashto
      </td>
    </tr>
  </tbody>
</Table>

### Prescription

| Field            | Type     | CharacterLimit | Required/Optional | Notes                                                                        |
| :--------------- | :------- | :------------- | :---------------- | :--------------------------------------------------------------------------- |
| RxNumber         | String   | 20             | R                 |                                                                              |
| Drug             | Object   |                | R                 |                                                                              |
| Quantity         | Decimal  | 9,3            | R                 | Quantity of the drug to dispense with a decimalin the thousandth’s position. |
| VialLabel        | Object   |                | R                 |                                                                              |
| Refill           | Object   |                | R                 |                                                                              |
| Prescriber       | Object   |                | R                 |                                                                              |
| Pharmacist       | Object   |                | R                 |                                                                              |
| dispenseDrugName | String   | 50             | R                 | The name of the drug being dispensed.                                        |
| writtenDrugName  | String   | 50             | R                 | The name of the drug prescribed by the provider.                             |
| WrittenDate      | Date     |                | R                 | Written date of the prescription                                             |
| DispensedDate    | Date     |                | R                 | Prescription’s expiration date                                               |
| ExpirationDate   | Date     |                | R                 |                                                                              |
| UnitPrice        | Decimal  | 8,2            | R                 |                                                                              |
| CopayAmount      | Decimal  | 8,2            | O                 |                                                                              |
| CustomData       | KeyValue |                | O                 | Array – 1 or more Key Values pairs                                           |

### Address (for Pharmacy Object)

| Field    | Type   | CharacterLimit | Required/Optional | Notes                      |
| :------- | :----- | :------------- | :---------------- | :------------------------- |
| Address1 | String | 50             | R                 |                            |
| Address2 | String | 50             | O                 |                            |
| City     | String | 50             | R                 |                            |
| Phone    | String | 15             | R                 | Format NNNNNNNNNN          |
| State    | String | 2              | R                 | US State Abbreviation Code |
| Zip      | String | 9              | R                 | Format NNNNN, NNNNNNNNN    |

### Shipping

| Field                | Type             | CharacterLimit | Required/Optional | Notes                                                                                                                                                                                                                      |
| :------------------- | :--------------- | :------------- | :---------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ShippingCode         | String           | 50             | R                 |                                                                                                                                                                                                                            |
| SignatureRequired    | Boolean          |                | O                 |                                                                                                                                                                                                                            |
| saturdayDelivery     | Boolean          |                | O                 | Saturday Delivery is an option for certain shipping codes depending on the carrier. To have an order delivered on a Saturday, select the correct Shipping Code from list of shipping codes and then set this flag to true. |
| Address              | Object (Address) |                | R                 | This is the address for the patient and where the order will be delivered unless there is an address specified in the hold address then the order will bedelivered to the hold address                                     |
| DeliveryInstructions | String           | 35             | O                 | Optional carrier delivery instructions to be printed on the shipping label.                                                                                                                                                |
| HoldAddress          | Object (Address) |                | O                 | Optional “hold location” address where the orderwill be delivered to instead of the patient address listed in the shipping address.                                                                                        |
| NotificationEmail    | String           | 100            | O                 | Optional email address to receive delivery updates from the carrier. If an email address is provided, it needs to be a valid email address with an ‘@’ and a‘.’. Required when specifying a HoldAddress.                   |

### Address (for shipping/hold address)

| Field    | Type   | CharacterLimit | Required/Optional | Notes                                                             |
| :------- | :----- | :------------- | :---------------- | :---------------------------------------------------------------- |
| Address1 | String | 50             | R                 |                                                                   |
| Address2 | String | 50             | O                 |                                                                   |
| City     | String | 50             | R                 |                                                                   |
| Phone    | String | 15             | R                 | Format NNNNNNNNNN                                                 |
| State    | String | 2              | R                 | US State Abbreviation Code                                        |
| Zip      | String | 9              | R                 | Format NNNNN, NNNNNNNNN                                           |
| Name     | String | 100            | R                 | For business address shipments. (E.g. John Smith c/o WellDyneRx). |
| ClinicId | String | 36             | O                 |                                                                   |

### Drug

| Field         | Type   | CharacterLimit | Required/Optional | Notes              |
| :------------ | :----- | :------------- | :---------------- | :----------------- |
| Ndc           | String | 11             | R                 | Format NNNNNNNNNNN |
| Manufacturer  | String | 50             | O                 |                    |
| Name          | String | 50             | R                 |                    |
| UnitOfMeasure | String | 10             | R                 |                    |

### Refill

| Field             | Type | CharacterLimit | Required/Optional | Notes                                                                                                                                                                                    |
| :---------------- | :--- | :------------- | :---------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| FillNumber        | Int  | 999            | R                 |                                                                                                                                                                                          |
| NextRefillDate    | Date |                | R                 | Prescription’s next available refill date                                                                                                                                                |
| RefillsPrescribed | Int  | 999            | R                 | The total number of refills prescribed.                                                                                                                                                  |
| RefillsDispensed  | Int  | 999            | R                 | The inclusive number of refills dispensed. If it is a new Rx, this will be 0 the first time HealthDyneRx receives that Rx. The 2nd fill will be the 1st refill, so this value would be 1 |
| FillNumber        | Int  | 999            | R                 | The exclusive number of refills remaining. The total number of refills on a prescription should equal the sum of RefillsDispensed and RefillsRemaining                                   |

### Prescriber

| Field     | Type   | CharacterLimit | Required/Optional | Notes                                            |
| :-------- | :----- | :------------- | :---------------- | :----------------------------------------------- |
| DeaNumber | String | 9              | O                 | The DEA Number for the prescription’s prescriber |
| FirstName | String | 50             | R                 |                                                  |
| LastName  | String | 50             | R                 |                                                  |

### Pharmacist

| Field     | Type   | CharacterLimit | Required/Optional | Notes                                                                                                                          |
| :-------- | :----- | :------------- | :---------------- | :----------------------------------------------------------------------------------------------------------------------------- |
| initials  | String | 50             | R                 | The initials or signature for the pharmacist that approved the prescription. Doctor John Doe Smith would have the initials JDS |
| FirstName | String | 50             | R                 |                                                                                                                                |
| LastName  | String | 50             | R                 |                                                                                                                                |

### VialLabel

| Field         | Type    | CharacterLimit | Required/Optional | Notes                                                                                                             |
| :------------ | :------ | :------------- | :---------------- | :---------------------------------------------------------------------------------------------------------------- |
| sig           | String  | 500            | R                 | Prescription usage. Also commonly referred to as the Sig or Signature. This must be populated in English language |
| AdditionalSig | String  | 500            | O                 | Prescription usage in translated language. This must be populated in language other than English.                 |
| Braille       | Boolean |                | O                 |                                                                                                                   |
| LargePrint    | Boolean |                | O                 |                                                                                                                   |
| AudioLabel    | Boolean |                | O                 |                                                                                                                   |