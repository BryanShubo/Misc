1 Web Service
```
Consumer application ==>provider application via SOAP, XML, JSON
Consumer application <==>provider application via http

Interoperability
Loosely Coupled
Extensibility
Mashups

Platform independent
Focussed developer roles
Resusability
Scalability
Cost reduction
Availability
```

2 Two Protocols 
```
SOAP (JAX-WS)
XML  HTTP POST

RESTful (JAX-RS): HTTP all methods

Multiple data fomats
```

3 SOA (Service Oriented Architecture) standard
```
what:
Architectureal Principles: services / loosely coupled

who:  W3C / OASIS

service:
```

4 XML 
```
1) Configuration
2) Data Exchange
3) Data and Meta Data

Well formedness

Validation: XML schema is a blue print for XML documentation

Namespace: allows usage of elements from differnet schemas in a single xml document. We use the unique 
namespace to identify elements

<customerName>Bharath</customerName>

<customerName> is MetaData, Bharath is data. This is equivalent to customer.name="Bharath"  
```

5 XSD (XML schema definition): 
```
it is a contractor between provider and consumer.
example: 
1) web.xsd for web.xml the JEE web application descriptor
2) project.xsd for eclipse IDE project

XSD Types:
In-Build Types
```

6 NAMESPACE
```
1) Uniquely Qualify Elements
ex: <amazon:order></amazon:order>

2) Organize types across schemas (like packages in Java)

Instead of using the entire namespace url to refer to a xml element, prefix can be used.
```

7 XML schema example
```
Patient Billing <==> Patient Clinical

Patient Data:
name, age, DOB, Email, gender, phone

```
