Briefly (in at most 300 words) reflect on your design choices for M5: first, sketch an application for reporting incidents that uses your format. Second, explain how this application uses your schema(s) and for which purpose, and justify some of your core design choices. Finally, sketch an application for generating the kind of reports mentioned in M5.

For the toolbar, press ALT+F10 (PC) or ALT+FN+F10 (Mac).



### 1. Show your design choice

**Design Description**

In this context, I chose the format as:

1. Core data model: Tree
2. One conceptual model: Using ER diagram
3. Four schemas: Using XML Schema (With each for the overall form, the event's detail, the person's detail, the event's reporter's detail)
4. Set of conforming ExtReps: XML documents.

An XML document that abides by my format will look like:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Form formType="incidentReport" formID="l29831"
    xmlns="..."
    xmlns:xsi="..." 
    xsi:schemaLocation=".../formSchema.xsd">
    <Events>
        <Event eventID="k82638">
            <EventType Value="accident"/>
            <EventDate Value="2021-01-10"/>
            <EventBuilding Value="kilburn"/>
            <EventTime Value="09:00"/>
            <EventRoomNo Value="208"/>
            <EventApartment Value="Not Answered"/>
        </Event>
    </Events>
    <People>
        <Person eventID="k82638">
            <PersonStatus Value="student"/>
            <PersonName Value="Lujin Li"/>
            <PersonIDnumber Value="k72800ll"/>
            <PersonDescriptionOfevent Value="It was a car accident..."/>
            <PersonDescriptionOfinjury Value="Leg injury...."/>
            <PersonTreatment Value="Treated by first aider"/>
            <PersonAbsence Value="still absent"/>
        </Person>
    </People>
    <Reporters>
        <Reporter eventID="k82638">
            <ReporterStatus Value="student"/>
            <ReporterName Value="Lujin Li"/>
            <ReporterIDnumber Value="k72800ll"/>
            <ReporterDescriptionOfevent Value="It was a car accident..."/>
            <ReporterDescriptionOfinjury Value="Leg injury...."/>
            <ReporterTreatment Value="Treated by first aider"/>
            <ReporterAbsence Value="still absent"/>
        </Reporter>
    </Reporters>
</Form>
```

This application uses the formSchema.xsd as the schema for it. (The formSchema.xsd also includes other three schemas for constraints of Event, People, and Reporter.) The Schema announces that the root element 'Form' contains three elements: Events, People, and Reporters.

For Events, it has to contain one or more 'event' elements, with each event containing three mandatory elements(Accident type, Date, and Building) and three optional elements(Time, Room number, and School Department). The Date is set to be a date type formatted in yyyy-mm-dd, and the Time is constrained to hh: mm.

For People, it has to contain one or more 'person' elements(it indicates people who were involved in an accident, usually the victims), with each person containing seven mandatory elements(status, name, id number, event description, injury description, treatment, absence) and four optional elements.
For Reporters, it has to contain one or more 'reporter' elements (it indicates the people that reported the accident), with each reporter containing three mandatory elements (name, job, telephone number) and two optional elements.

**Core design features**

1. Use sequence to represent one or more elements. In the further description of the 'Event' schema, set each 'Event' with a mandatory attribute 'EventID'. (Make similar constraints in both 'Person' and 'Reporter' schema)

```xml
 <xs:element name="Events">
    <xs:complexType>
      <xs:sequence>
        <xs:element maxOccurs="unbounded" ref="Event"/>
      </xs:sequence>
    </xs:complexType>
  </xs:element>
```

2. Use xs:ID, xs:integer, xs:time, xs:dateTime, etc. to constrain different types of elements' value.
3. We can use javaScript as an auxiliary way to accomplish further constraints. For example, an accident without details about victims is not allowed to submit, a near miss with victims is also not allowed to submit, etc.
4. Since every piece of information is separated by elements, the Health and Safety Officer can easily do searches with xQuery-based web pages.

**Application sketch**

1. Use a web-based interface.
2. Use a web form for users to submit the accident report form. Receive the data at the backend, use the schemas to validate the data. Integrate the data into an XML document only if it is successfully validated. Integrate all forms into one XML document.
3. Build another web-based interface for administrators. Use javaScript to encapsulate functions with xQuery. In this case, it will simplify the XML document's search operations for *Health and Safety Officers*.



### 1. Describe your choice

(what data model, what internal representation you chose(flat file, tables,...), what external representaion you are going to use(JSON, CSV, ....))

### 2. Explain  it

(briefly describe your schemas, and what the document looks like in your format)

### 3. Sketch the application

(How you can use what you've designed)



### Notes

what do we have:

Accident detail:

1. *accident type(accident, damage to property, incident/near miss, fire, ill health)
2. *Date
3. *Building
4. Time
5. Room No
6. School Department



Person detail:

1. *status (staff, student, visitor, concentractor, Other)
2. *name
3. *ID number
4. job
5. manager
6. telephone
7. email
8. school unit
9. *event description
10. *injury description
11. *treatment(no treatment, Treated by first aider, Injury in a hospital)
12. *absence(No absence, still absent, absent returned in 3 days, absent due to work-related injury)



Reporter detail:

1. *name
2. *job
3. email
4. *tel
5. school department





**Context**:

This week, continuing from our discussion in class, we assume we are designing a (small part of an) incident reporting system where members of staff of the University of Manchester; you can consider the [current form](http://documents.manchester.ac.uk/display.aspx?DocID=10017) to help you get a better understanding of this domain.

**Task**:

In particular, we want you to design a **format** for recording H&S incidents that provides suitable means to capture the following pieces of data:

1. incidents: what kind, where, when, description of what happened
2. people involved: the person reporting the incident, plus possibly victims and witnesses, including contact details
3. damage: what kind of damage or injury was caused to whom/what, and what are the consequences or requirements.

Notice that we distinguish between different incidents: for example, accidents (which involve victims) and near misses (which cannot involve victims). In the current format, a reporter could report all sorts of non-sensical information. Your format should support an application that supports the user in providing sensical information: for example, they should not report an accident without details about victims, but should not be able to report a near miss with victims. Also, it would be good if the location would enable us to search for all incidents in Kilburn Building - regardless of the many ways to (mis-)spell this building or its address.

 

You should work on the following documents: 

- a conceptual model of your domain, in form of an ER diagram or similar, reflecting all concepts of this exercise
- some example documents in the format you have designed which capture the data of a few different incidents
- a schema, in a schema language of your choice that fits nicely this reporting application, your data structure formalism, and your example document, and which captures your format (in particular, your example documents should be valid w.r.t. your schema!).

**Note:** 

Before you start, have a look at **SE5**, where we ask you to sketch out your application and explain your design choices. So we would like to see a design that you can justify in SE5.

Aim at a **robust** design.

Aim at a good format: consider the *Health and Safety Officer* who needs to write monthly and annual reports of incidents, and ensure that they occur extremely rarely and potential hazards are considered and their risk minimized. So your format should make it very easy for these officers, who are not trained database experts, to query for relevant information: e.g., 'how many near misses did we have last month/year (compared to previous months/years)?' or 'in which departments did we see recent fires?' or 'were there any fires out of hours in the last year?'. Moreover, it should be relatively easy to build

- a web-based user interface for H&S officer to formulate those queries
- a web-based user interface for people to report incidents in a way that the information they provide is complete, reliable, and interpretable.

Also, feel free to google for reporting forms for other institutions: this is a rather common task/application.

```xquery
```

