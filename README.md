# Beckhoff-Examples
## Modern features in not so modern industry.

This repository contains code with simple features like : 

- Sending a text message 
- Sending an email
- Sorting an array
- Making a REST API call
- Data persistance to a database
- Generated user interface

**BUT** with a PLC. PLC is an idustrial Arduino on steroids.

Unfortunatelly working with PLC is cumbersome. 

PLCs were meant to replace physical wiring of relay logic - so it's more electrical engineering than software engineering.

So obviously it's not really good at software stuff

...unfortunatelly the industry forces you to write enterprise software in a PLC.

Beckhoff's TwinCAT 3 is one of few which offers modern features like object oriented programming, open API and integration in Visual Studio. 
Other platforms are using their own IDE with their own language.

---
# Expensive features simply and almost for free.

Delivering features with PLCs is cumbersome. Sure, it is possible to deliver a complex feature in a PLC, but is it worth the hassle?

Dealing with a hardware configuration, reading through an obscure documentation just to find the specific memory address... Yuck!

WELL NOT ON MY WATCH!

Time is precious, let's not waste it.

I'll show you how to implement some features from Inxton's Advanced package with the Core package.

Let's start with the most powerful one. Funny enough, it's pretty simple to implement it.


## Let's start
I'll focus on the conceptual design. Here's the code :

- TwinCAT function blocks - [Github link](https://github.com/jozefchmelar/Beckhoff-Examples/tree/master/src/PLC/TwinCAT/Plc/POUs)

- C# Twins/counterparts - [Github link](https://github.com/jozefchmelar/Beckhoff-Examples/tree/master/src/PLC/PlcConnector)
## How to call a C# method from the PLC

PLC has the `CSharpMethod` function block which encapsulates a simple logic. It also has a C# twin (a counterpart) generated by Inxton called `CSharpMethod.g.cs`

When the PLC sets the `InvokeRequested` variable, its C# counterpart will notice and do the work on the PC side. It will also notify the PLC that the work started and ended.

So to call a C# method from a PLC I have to initialize the counterpart and set a variable in the PLC.

 
## How to send an email from the PLC

I will use the `CSharpMethod` function block to send an email, because it's so much easier to do so in C# than in CoDeSys.

I created another function block `fbEmail` which contains a subject, content and the recipient of the email.

It also contains a variable `SendEmail` of type `CSharpMethod`. This variable needs to be initialized in its C# counterpart.

Like this
```csharp
SendEmail.Initialize(SendEmailMethod);
```

It says what C# method should be executed when PLC asks for it.