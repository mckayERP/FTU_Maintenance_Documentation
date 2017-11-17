# Component Tracking

Component tracking involves recording the life events of a particular component from the time it enters service to the time it is disposed of or scrapped.   Component tracking is important in Aviation Maintenance since the life history of critical components determines their suitability for service and the inspection/overhaul schedule they are subject to follow.

In the FTU software, components are essentially Products that are flagged as being tracked as a component.  Such products, when they are used in any transaction, be it a purchase order, material receipt, maintenance work order or maintenance action/result, will have that history tracked in the technical log for that component.

A product by itself is very generic and only suitable for the most basic components, such as bolts and nuts, which have no serial numbers and which are indistinguishable from all other components of the same make/model or type.  To distinguish products futher, attribute sets are used to define the important specifications of the product and the distinguishing elements, such as a serial number, that will be used to identify a unique component.

Components can be assemblies of other components and these assemblies can be installed in other higher-level assemblies.  The assemblies are defined by Bills Of Material \(BOM\)s.  The highest level component, in the FTU application at least, is an aircraft.  The aircraft is its own component with a serial number and  its own Bill of Materials.

As an example, a Cessna C-150M is a generic product with a make and model.  It has a product BOM that defines the critical products of interest to aviation maintenance that includes the following:

* an airframe;
* an engine;
* a propeller;
* a fire extinguisher;
* avioncs;
* instruments;
* etc...

The engine product will have a similar BOM that will include:

* Carburator
* Cylinders
* Starter Motor
* Alternators
* Magnetos

Each of these products may have an attribute set instance that identifies specifications but there will be no component instance information such as serial numbers.

The components are specific instances of the products.  Using the above example, a specific aircraft, with a call mark and serial number, will have a component BOM that mirrors the product BOM but that includes the components \(product and attribute set instance\) for each product.  The carburator component will have a serial number and specific life data, such as time since last overhaul.

## Identifying Components

It is not necessary to manually create components.  Components are created automatically when the following conditions exist:

1. A Product exists that has the "Track as Component" flag selected.
2. That Product is referenced on any Document such as a Material Receipt, Purchase Order, Maintenance Work Order etc...

To create a component with attributes, the Product will have to have an Attribute Set defined on the Product window.  If the Attribute Set includes specification information, the Product can also have an Attribute Set Instance defined which includes the specification information but that does not have any instance information.  The component will be created when any document references that Product and an Attribute Set Instance that includes a serial number.

The Product window can also be used to define the Component Life Cycle model used to create the component.  The model determines such values as the life measurement units, the source of the life usage increments, the maximum life usage and if there is any extension on the life usage possible.

So in summary, to create a Component:

1. Ensure that the [Airworthiness Directives have been loaded at least once](/Loading Airworthiness Directives from the CAWIS site.).  This will initialize the set of manufacturers and models for the aircraft.
2. Create Attributes for the product, one for each specification that will be added to the product.
3. Define an Attribute Set listing the product attributes \(specifications\) and instance attributes \(serial number, lot or guarantee date\)
4. Define the product and select "Track as Component" in the Product Window.
5. In the Product WIndow, set the Attribute Set Instance as required - defining the product attributes.
6. If the product is an assembly, create a Bill of Materials for the product, identifying other products as sub-components.
7. Create a Component Life Cycle Model record.
8. Create any suitable document and reference the Product and Attribute Set Instance \(with serial number\).
9. In the Component window, verify that the component exits and that a history \(Technical Log\) has been created with an initial entry.
10. Find the parent component and add the created component to the assembly.  \(This describes the manual process of adding a component to an assembly.  The process can also be performed through the maintenance work order activities or results.\)
11. Verify that the sub-component history shows that the sub-component was added to the parent BOM.

These steps are explained in detail below using a simple aircraft model as an example.  The aircraft is a Cessna 150M, call sign C-FJZP.  It contains the following equipment that needs to be tracked:

* Aircraft C-150L C-FJZP SN: 15074708
  * Engine O-200-A SN: 67128-7-A
    * Cylinder 1 Part: AEC65314ST61.1D SN: 23543
    * Cylinder 2 Part: AEC65314ST61.1D SN: 23544
    * Cylinder 3 Part: AEC65314ST61.1D SN: 23545
    * Cylinder 4 Part: AEC65314ST61.1D SN: 23544
    * Alternator Part: De OFF10300FR SN: H060387
    * Carburetor Part: 10-4894-1 SN: 75023314
    * Magneto - left Part: 4301 SN: 03060693
    * Magneto - right Part: 4301 SN: 08091570
    * Starter Part: EQ6986 SN: 12011960S
    * Vacuum Pump Part: CH215CC-9 SN: 66076
  * Hose - Fuel Part: 350-0210
  * Hose - oil Part: AE7010000B0150
  * Engine bolts \(4\)
  * Engine Mounts \(4\)
  * Fire Extinguisher
  * Emergency Locator Transmitter

#### 1. Verify that the Airworthiness Directives have been loaded

Open the Product window and create a new product record.  Select the checkbox "Track as Component".  A box labled CAWIS Manufacturer will appear.  Try to select an entry from the box.  If it is full of aircraft company names, no action needs be taken and you can move on to the next step.  If the selection list of the box is empty, it will need to be filled first.  This is done by running the process "Load Airworthiness Directives".  This process will gather all the airworthiness information from the Transport Canada CAWIS website - a process that can take several hours to complete.  While the process runs, you can complete the other steps but you will need to return to the Product Window and update the product records with the correct CAWIS Manufacturer and Model.

#### 2. Create Attributes

For the product, we will use a generic Cessna 150L model.  There are many attributes that could be added to this product as specifications but the key ones we will use are the Manufacturer Name or Make and the Model.  If desired, additional attributes could be added for spec data such as fuel type, empty weight, etc...

We will also create an instance attribute which will only be valid when a component - an instance of the product - is defined.  The instance attributes will be the aircraft registration.  When the attribute set is defined, we will include a serial number.

![](/assets/Attribute%28make-list%29.png)![](/assets/AttributeValues%28make-list%29.png)![](/assets/Attribute%28model-list%29.png)![](/assets/AttributeValues%28model-list%29.png)![](/assets/Attribute%28reg%29.png)![](/assets/AttributeSet%28AC%29.png)![](/assets/AttributeUse%28AC%29.png)

![](/assets/ProductASI%28new C-150L%29.png)



![](/assets/Product%28AC%29.png)![](/assets/CompLifeCycle%28Aircraft%29.png)

