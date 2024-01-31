<p align="left"><img src="./images/GS1DE.jpeg" alt="GS1 Germany Logo" width="20%"></p>
<br>

# Green Paper: How GS1 Standards can help to meet the EU Deforestation Regulation

GS1 Germany Green Paper on how the requirements of the EUDR can be met with GS1 standards.

## Disclaimer

THIS DOCUMENT IS A GS1 GERMANY GREEN PAPER ONLY, NOT A RATIFIED APPLICATION STANDARD OR IMPLEMENTATION GUIDELINE APPROVED BY ANY GS1/GS1 GERMANY BOARD OR COMMITTEE. ITS PURPOSE IS TO STIMULATE DISCUSSION AND TO PAVE THE WAY FOR DEVELOPING A SOLUTION APPROACH FOR MEETING EUDR REQUIREMENTS USING GS1 STANDARDS. IT ALSO AIMS TO CONTRIBUTE TO FUTURE GS1 STANDARDISATION EFFORTS IN THIS AREA.

## Introduction

### Synopsis of the EUDR

The Regulation (EU) 2023/1115 targets deforestation and forest degradation, underscoring the value of forests and the urgency to address global deforestation. It recognises the EU's contribution to this issue through its consumption patterns and advocates for regulatory actions to minimise the EU's deforestation impact. The regulation mandates sustainable and deforestation-free production of commodities and products, including due diligence, risk assessment, and supply chain transparency. It also stipulates enforcement and penalties for non-compliance, and emphasises the EU's dedication to international collaboration for a global approach against deforestation.

### Affected commodities and products

The EU regulation on deforestation covers the following seven relevant commodities (see e.g. EU 2023, § 1.1):

1. Oil palm
2. Soya
3. Wood
4. Cocoa
5. Coffee
6. Cattle
7. Rubber

Products "...that contain, have been fed with or have been made using [the above mentioned] relevant commodities" (EU 2023, § 2.2) (i.e., derivates made from [the above mentioned]) fall under the legislation. Annex I of the regulation lists concrete details. Therefore, if a company, for instance,  imports cocoa butter, fat or oil into the EU or if it processes cocoa powder within the EU, it must comply with this regulation.

### In scope/out of scope

It is important to note that the EUDR specifies a number of responsibilities for companies importing the mentioned commodities into the EU market, most notably (no claim to completeness):

1. Ensure that products are not placed on the market or exported unless they are deforestation-free, produced in accordance with relevant legislation, and covered by a due diligence statement. (EU 2023, § 3)
2. Make available a due diligence statement to the competent authorities while keeping a record of these statements for five years (EU 2023, § 4.1 and § 4.2)
3. Perform due diligence for each affected supplier (EU 2023, § 8), including the collection of information, data and documents (EU 2023, § 9), risk assessments (EU 2023, § 10), and risk mitigation measures (EU 2023, § 11).
4. Make available traceability data needed for due diligence statement to downstream business partners

TO BE COMPLETED

**In scope:**
1. Data exchange solution candidate for transmitting dynamic data (e.g. quantity, country of production, geolocation) as required in EU (2023) § 9, including syntax, fields and values.
2. Data exchange solution candidate for transmitting static data (e.g. product name and description or name and postal address of operators) as required in EU (2023) § 9, including fields and values.

**Out of scope:**
1. Advice regarding the collection of information, data and documents as per EU (2023) § 9 as such.
2. Specification of upstream or downstream data structures (e.g. EPCIS events) that are able to convey data to support the obligations indicated under (A).
3. Advice regarding risk assessment as per EU (2023) § 10.
4. Procedures and measures for risk mitigation as per EU (2023) § 11.
5. Specification of the EU Due Diligence Statement message.
6. Mapping of the EPCIS Origin Declaration Event to the EU Due Diligence Statement.
7. Any other subject not explicily mentioned to be in scope.

## Potential solution approach

### Overview

The suggested solution approach aims at making it as easy and efficient for affected companies to meet the EUDR. In a nutshell, growers of the above-mentioned commodities only need to capture one concise electronic message ('EPCIS Origin Declaration Event'), which in turn can be transformed into a corresponding due diligence message (thereby e.g. enriched with appropriate master data according to the EU's requirements) and sent to the API endpoint which will be specified by the EU. As many growers already share their traceability data via data exchange platforms, this data processing step can be performed by their respective platform providers.

The beauty of this approach consists in the fact that this 'EPCIS Origin Declaration Event' is only a derivate of already existing visibility (e.g. harvesting, transformation) events. Further, if providers of traceability platforms take care of transmitting the due diligence statements to the EU in a consolidated manner, growers need to indicate their product/location/party master data only once rather than repeating the latter in each and every message. Thus, they can focus on providing just the few additional dynamic properties (e.g. acreage polygons) as required by the regulation. In addition, the respective platform providers can check whether the provided data is complete as well as fulfils the legal requirements.

The following, simplified picture illustrates the solution approach, taking the example of a manufacturer of a product for which the latter uses commodities provided by various suppliers.

![Solution approach illustration](./images/EUDR_SolutionApproachDrawing.jpg "Solution approach illustration")
*Figure 1: Simplified illustration of solution candidate scope*

### Due Diligence Statement

![Due Diligence Statement](./images/DueDiligenceStatement.png "Due Diligence Statement, EU 2023, Annex II")
*Figure 2: Due Diligence Statement as per EU (2023), Annex II*

### Master data vs. event data

Explain that the above DDS consists of:
- Product, organisation and location master data (static)
- Visibility data (dynamic)

### Master Data

IDEE: Drei Tabellen mit geforderten Infos gemäß EUDR
a. Product Master Data
b. Location Master Data
c. Party Master Data

#### Product master data

eudr:hsCode

eudr:commodityDescription

eudr:scientificName

eudr:commonName

TBD: GS1 Web Voc format (+ Bsp.)?

#### Location master data

TBD: In this section, we COULD indicate that if a given field has a defined polygon, a master data service (e.g. the GS1 Registry) could store/provide this polygon and further ease data provision.

#### Party master data

§9: 
"(e) the name, postal address and email address of any business or person from whom they have been supplied with the relevant products;
(f) the name, postal address and email address of any business, operator or trader to whom the relevant products have been supplied;


### Event data

#### Preliminary remark

Note that none of the specified EPCIS user extension fields are standardised yet. This is why the latter are declared under the `example` namespace.

Once the EPCIS event message structures are  standardised, e.g. in a GS1 application standard, the respective sections should be updated accordingly.

#### Design considerations

- e.g. each EPCIS event is related to (one?) specific product (TBD) 

#### EPCIS 2.0 XML example

```xml
<epcis:EPCISDocument xmlns:epcis="urn:epcglobal:epcis:xsd:2" schemaVersion="2.0" creationDate="2024-01-20T03:00:00.000+02:00" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="urn:epcglobal:epcis:xsd:2 EPCglobal-epcis-2_0.xsd" xmlns:eudr="https://ns.eudr.example.com">
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

#### EPCIS 2.0 JSON/JSON-LD example

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
  "creationDate": "2024-01-20T03:00:00.000+02:00",
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

## Contributors

| Name                   | Affiliation              | Job Title              |
| ---------------------- | ------------------------ | ---------------------- |
| Dr Ralph Troeger       | GS1 Germany              | Senior Manager AIDC    |
| TBC: Elisabeth Kikidis | GS1 Germany              | Senior Manager AIDC    |
| TBC: Sabine Klaeser    | GS1 Germany              | Senior Manager AIDC    |
| TBC: Frank Kuhlmann    | GS1 Germany              | Lead AIDC              |

## References

- EU (2023). *REGULATION (EU) 2023/1115 OF THE EUROPEAN PARLIAMENT AND OF THE COUNCIL
of 31 May 2023 on the making available on the Union market and the export from the Union of certain commodities and products associated with deforestation and forest degradation and repealing Regulation (EU) No 995/2010, Official Journal of the European Union, June 2023*. Retrieved from [https://eur-lex.europa.eu/legal-content/EN/TXT/PDF/?uri=CELEX:32023R1115](https://eur-lex.europa.eu/legal-content/EN/TXT/PDF/?uri=CELEX:32023R1115)
- GS1 (2022). *Core Business Vocabulary (CBV) Standard, Release 2.0, Ratified, Jun 2022*. Retrieved from [https://ref.gs1.org/standards/cbv/](https://ref.gs1.org/standards/cbv/)
- GS1 (2022). *EPCIS Standard, Release 2.0, Ratified, Jun 2022*. Retrieved from [https://ref.gs1.org/standards/epcis/](https://ref.gs1.org/standards/epcis/)
- EU observatory on deforestation and forest degradation (?) [(https://forest-observatory.ec.europa.eu/forest/)](https://forest-observatory.ec.europa.eu/forest/)  
- ...
