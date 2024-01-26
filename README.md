<p align="left"><img src="GS1DE.jpeg" alt="GS1 Germany Logo" width="20%"></p>
<br>

# EU Deforestation Regulation Green Paper

GS1 Germany Green Paper on how to meet the EUDR's requirements with GS1 standards.

## Disclaimer

THIS DOCUMENT IS A GS1 GREEN PAPER ONLY, NOT A RATIFIED APPLICATION STANDARD OR IMPLEMENTATION GUIDELINE APPROVED BY ANY GS1/GS1 GERMANY BOARD OR COMMITTEE. ITS PURPOSE IS TO OFFER A POTENTIAL 'BEST GUESS' SOLUTION FOR MEETING EUDR REQUIREMENTS USING GS1 STANDARDS. IT AIMS TO CONTRIBUTE TO FUTURE GS1 STANDARDISATION EFFORTS IN THIS AREA.

IT WAS DEVELOPED DILIGENTLY AND IN COLLABORATION WITH OSAPIENS, A GS1 GERMANY SOLUTION PARTNER, LEADING A USER GROUP FOCUSING ON THIS TOPIC.

## Introduction

### Synopsis of the EUDR

The Regulation (EU) 2023/1115 targets deforestation and forest degradation, underscoring the value of forests and the urgency to address global deforestation. It recognizes the EU's contribution to this issue through its consumption patterns and advocates for regulatory actions to minimize the EU's deforestation impact. The regulation mandates sustainable and deforestation-free production of commodities and products, including due diligence, risk assessment, and supply chain transparency. It also stipulates enforcement and penalties for non-compliance, and emphasizes the EU's dedication to international collaboration for a global approach against deforestation.

### Affected commodities and products

The EU regulation on deforestation covers the following seven relevant commodities (see e.g. EU 2023, § 1.1):

1. Oil palm
2. Soya
3. Wood
4. Cocoa
5. Coffee
6. Cattle
7. Rubber

Products "...that contain, have been fed with or have been made using [the above mentioned] relevant commodities" (EU 2023, §2.2) fall under the legislation. Annex I of the regulation lists concrete exampels. Therefore, if a company, for instance,  imports cocoa butter, fat or oil into the EU, it must comply with this regulation.

## In scope/out of scope

It is important to note that the EUDR specifies a number of responsibilities for companies importing the mentioned commodities into the EU market, most notably (no claim to completeness):

1. Ensure that products are not placed on the market or exported unless they are deforestation-free, produced in accordance with relevant legislation, and covered by a due diligence statement. (EU 2023, §3)
2. Make available a due diligence statement to the competent authorities while keeping a record of these statements for five years (EU 2023, §4.1 and §4.2)



This document 


In scope is 

Out of scope: risk assessment, 
"information to ensure the transparency of the supply chain of relevant products",
any further upstream or downstream EPCIS events 

## Data sharing requirements

<IDEE: Solution concept illustration>
- Economic Operator - Platform/SP - EU (=> genaune Bezeichnungen gem. EUDR)
- Product, organisation and location master data (static)
- Visibility data (dynamic)

### Mapping of required fields with EPCIS event fields

Table 
eoid => GS1 DL URI, AI 417


## Master Data vs. Event Data 


## EPCIS event message specification

### Preliminary remark

Note that none of the specified EPCIS user extension fields are standardised yet. This is why the latter are declared under the `example` namespace.

Once the EPCIS event message structures are  standardised, e.g. in a GS1 application standard, the respective sections should be updated accordingly.

### Product master data

eudr:hsCode
eudr:commodityDescription
eudr:scientificName
eudr:commonName


## EPCIS message examples





### EPCIS 2.0 XML Example

```xml
<epcis:EPCISDocument xmlns:epcis="urn:epcglobal:epcis:xsd:2" schemaVersion="2.0" creationDate="2019-11-28T14:59:02.000+01:00" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="urn:epcglobal:epcis:xsd:2 EPCglobal-epcis-2_0.xsd" xmlns:eudr="https://ns.eudr.example.com">
	<EPCISBody>
		<EventList>
			<ObjectEvent>
				<!-- Date and time when declaration was made. Should be equal or lower than harvestEndDate -->
				<eventTime>2024-01-20T03:00:00.000+02:00</eventTime>
				<eventTimeZoneOffset>+02:00</eventTimeZoneOffset>
				<action>OBSERVE</action>
				<bizStep>https://example.com/bizStep/declaring_origin</bizStep>
				<!-- Identifies the supplier's place of business (e.g. headquarters). Usually corresponds with operator's Party GLN, see eudr:operatorID -->
				<readPoint>
					<id>https://id.gs1.org/414/4000001100002</id>
				</readPoint>
				<bizTransactionList>
					<!-- TBD: most suitable URI notation. URN-based URI vs. HTTPS URIs, CBV 2.0, 8.5.3 vs. 8.5.5 -->
					<bizTransaction type="https://example.com/btt/dueDiligenceStatementNumber">https://epcis.example.com/user/vocab/bt/DDS.123</bizTransaction>
					<!-- (Optional) Business transaction reference(s) e.g., purchase order number for later mapping -->
					<bizTransaction type="https://ref.gs1.org/cbv/BTT-po">urn:epcglobal:cbv:bt:4000001000005:PO12345</bizTransaction>
				</bizTransactionList>
				<!-- Identification of the supplied product via GTIN (and batch) and its quantity -->
				<quantityList>
					<quantityElement>
						<epcClass>https://id.gs1.org/01/04000044001236/10/BATCH123</epcClass>
						<quantity>50</quantity>
						<uom>KGM</uom>
					</quantityElement>
				</quantityList>
				<!-- TBD: Use GS1 Web Voc (if applicable) or proceed with eudr user extensions for the time being? -->
				<eudr:harvestDateStart>2024-01-20</eudr:harvestDateStart>
				<eudr:harvestDateEnd>2024-01-18</eudr:harvestDateEnd>
				<!-- Own EORI (Economic Operators Registration and Identification) number -->
				<eudr:eoriNumber>DE12345678912345</eudr:eoriNumber>
				<!-- (Optional) Party GLN identifying operator who makes the statement -->
				<eudr:partyGLN>https://id.gs1.org/417/4000001000005</eudr:partyGLN>
				<!-- (Optional) List of countries of origin where the geolocations of the producers are located -->
				<eudr:countryList>
					<!-- 1 or more occurrences, ISO 3166-1 Alpha-2, 2-letter country codes -->
					<eudr:country>CO</eudr:country>
				</eudr:countryList>
				<!-- Origin information -->
				<eudr:originList>
					<!-- 1 or more occurrences (one container = one geolocation or polygon) -->
					<eudr:originDetails>
						<!-- Identification of the plot of land via polygon -->
						<!-- See also: https://ref.gs1.org/standards/cbv/#page=118 -->
						<eudr:geofence>[[6.898247,50.942499], [6.898292,50.942275], [6.898094,50.942263], [6.898126,50.942106], [6.898526,50.942130], [6.898451,50.942512], [6.898247,50.942499]]</eudr:geofence>
						<!-- Optional area size -->
						<eudr:areaSize>
							<eudr:value>100</eudr:value>
							<eudr:unitCode>HAR</eudr:unitCode>
						</eudr:areaSize>
						<!-- Optional producer/farmer information -->
						<eudr:producerIdentification>
							<!-- TBD: really freetext or proper ID? -->
							<eudr:producer>Farmer ABC</eudr:producer>
						</eudr:producerIdentification>
					</eudr:originDetails>
					<eudr:originDetails>
						<!-- Identification of the plot of land via geolocation -->
						<eudr:geolocation>geo:50.942499,6.898247</eudr:geolocation>
						<eudr:areaSize>
							<eudr:value>2.5</eudr:value>
							<eudr:unitCode>HAR</eudr:unitCode>
						</eudr:areaSize>
						<eudr:producerIdentification>
							<eudr:producer>Farmer DEF</eudr:producer>
						</eudr:producerIdentification>
					</eudr:originDetails>
				</eudr:originList>
			</ObjectEvent>
		</EventList>
	</EPCISBody>
</epcis:EPCISDocument>
```

### EPCIS 2.0 JSON/JSON-LD Example

```json
{
  "@context": [
    "https://ref.gs1.org/standards/epcis/2.0.0/epcis-context.jsonld",
    {
      "eudr": "https://ns.eudr.example.com"
    }
  ],
  "type": "EPCISDocument",
  "schemaVersion": "2.0",
  "creationDate": "2019-11-28T14:59:02.000+01:00",
  "epcisBody": {
    "eventList": [
      {
        "type": "ObjectEvent",
        "eventTime": "2024-01-20T03:00:00+02:00",
        "eventTimeZoneOffset": "+02:00",
        "action": "OBSERVE",
        "bizStep": "https://example.com/bizStep/declaring_origin",
        "readPoint": {
          "id": "https://id.gs1.org/414/4000001100002"
        },
        "bizTransactionList": [
          {
            "type": "https://example.com/btt/dueDiligenceStatementNumber",
            "bizTransaction": "https://epcis.example.com/user/vocab/bt/DDS.123"
          },
          {
            "type": "po",
            "bizTransaction": "urn:epcglobal:cbv:bt:4000001000005:PO12345"
          }
        ],
        "quantityList": [
          {
            "epcClass": "https://id.gs1.org/01/04000044001236/10/BATCH123",
            "quantity": 50,
            "uom": "KGM"
          }
        ],
        "eudr:countryList": {
          "eudr:country": "CO"
        },
        "eudr:eoriNumber": "DE12345678912345",
        "eudr:originList": {
          "eudr:originDetails": [
            {
              "eudr:areaSize": {
                "eudr:value": "100",
                "eudr:unitCode": "HAR"
              },
              "eudr:producerIdentification": {
                "eudr:producer": "Farmer ABC"
              },
              "eudr:geofence": "[[6.898247,50.942499], [6.898292,50.942275], [6.898094,50.942263], [6.898126,50.942106], [6.898526,50.942130], [6.898451,50.942512], [6.898247,50.942499]]"
            },
            {
              "eudr:geolocation": "geo:50.942499,6.898247",
              "eudr:areaSize": {
                "eudr:value": "2.5",
                "eudr:unitCode": "HAR"
              },
              "eudr:producerIdentification": {
                "eudr:producer": "Farmer DEF"
              }
            }
          ]
        },
        "eudr:harvestDateStart": "2024-01-20",
        "eudr:harvestDateEnd": "2024-01-18",
        "eudr:partyGLN": "https://id.gs1.org/417/4000001000005"
      }
    ]
  }
}
```

## Authors

| Name                   | Affiliation              | Job Title              |
| ---------------------- | ------------------------ | ---------------------- |
| Dr Ralph Troeger       | GS1 Germany              | Senior Manager AIDC    |
| TBC: Patrik Rothe      | OSAPIENS                 | ...                    |
| TBC: Elisabeth Kikidis | GS1 Germany              | Senior Manager AIDC    |
| TBC: Sabine Klaeser    | GS1 Germany              | Senior Manager AIDC    |
| TBC: Frank Kuhlmann    | GS1 Germany              | Lead AIDC              |
| TBC: Carsten Mohr      | OSAPIENS                 |                        |

## References

- EU (2023). *REGULATION (EU) 2023/1115 OF THE EUROPEAN PARLIAMENT AND OF THE COUNCIL
of 31 May 2023 on the making available on the Union market and the export from the Union of certain commodities and products associated with deforestation and forest degradation and repealing Regulation (EU) No 995/2010, Official Journal of the European Union, June 2023*. Retrieved from [https://eur-lex.europa.eu/legal-content/EN/TXT/PDF/?uri=CELEX:32023R1115](https://eur-lex.europa.eu/legal-content/EN/TXT/PDF/?uri=CELEX:32023R1115)
- GS1 (2022). *Core Business Vocabulary (CBV) Standard, Release 2.0, Ratified, Jun 2022*. Retrieved from [https://ref.gs1.org/standards/cbv/](https://ref.gs1.org/standards/cbv/)
- GS1 (2022). *EPCIS Standard, Release 2.0, Ratified, Jun 2022*. Retrieved from [https://ref.gs1.org/standards/epcis/](https://ref.gs1.org/standards/epcis/)
- ...
