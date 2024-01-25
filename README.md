<p align="left"><img src="GS1DE.jpeg" alt="GS1 Germany Logo" width="20%"></p>
<br>

# EU Deforestation Regulation White Paper

GS1 Germany White Paper on how to meet the EUDR's requirements with GS1 standards.

## Disclaimer

THIS DOCUMENT IS A GS1 WHITE PAPER ONLY, NOT A RATIFIED APPLICATION STANDARD OR IMPLEMENTATION GUIDELINE APPROVED BY ANY GS1/GS1 GERMANY BOARD OR COMMITTEE. ITS PURPOSE IS TO OFFER A POTENTIAL 'BEST GUESS' SOLUTION FOR MEETING EUDR REQUIREMENTS USING GS1 STANDARDS. IT AIMS TO CONTRIBUTE TO FUTURE GS1 STANDARDISATION EFFORTS IN THIS AREA.

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

It is important to note that the EUDR 

This document 

In scope is 

Out of scope: risk assessment, 
"information to ensure the transparency of the supply chain of relevant products"

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

## Master data file example


## EPCIS message examples





### EPCIS 2.0 XML Example

```xml
<xml>
    <test1>
    </test1>

</xml>
```

### EPCIS 2.0 JSON/JSON-LD Example

```json
{
  
}
```


## References

- EU (2023). *REGULATION (EU) 2023/1115 OF THE EUROPEAN PARLIAMENT AND OF THE COUNCIL
of 31 May 2023 on the making available on the Union market and the export from the Union of certain commodities and products associated with deforestation and forest degradation and repealing Regulation (EU) No 995/2010, Official Journal of the European Union, June 2023*. Retrieved from [https://eur-lex.europa.eu/legal-content/EN/TXT/PDF/?uri=CELEX:32023R1115](https://eur-lex.europa.eu/legal-content/EN/TXT/PDF/?uri=CELEX:32023R1115)
- GS1 (2022). *Core Business Vocabulary (CBV) Standard, Release 2.0, Ratified, Jun 2022*. Retrieved from [https://ref.gs1.org/standards/cbv/](https://ref.gs1.org/standards/cbv/)
- GS1 (2022). *EPCIS Standard, Release 2.0, Ratified, Jun 2022*. Retrieved from [https://ref.gs1.org/standards/epcis/](https://ref.gs1.org/standards/epcis/)
- ...
