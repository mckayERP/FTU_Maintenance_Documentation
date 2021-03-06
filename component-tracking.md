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

**Attributes** can be thought of as specifications.  There are two types: **Product Attributes** and **Instance Attributes**.  Instance Attributes have values that are specific to an instance of a product - things like a serial number, lot code, guarantee date or any other value that uniquely identifies an individual product. The Product Attributes define specifications that do not change from instance to instance. For example, the Product Attributes could include the "details" of the product shown on a website.

For component tracking, its important that the base product of the component have an **Attribute Set** defined.  Instance Attribute defined, ideally a serial number.  Without the instance, the component is no different then the product and tracking through a life-cycle is not possible.  This may be the case for consummable items like applied paint or nuts and bolts and tracking these items may not be important. However, there is often a need to replace such consumables after a single use.  In these cases, the product should have at least one Product Attribute defined.

For the product, we will use a generic Cessna 150L model.  There are many attributes that could be added to this product as specifications but the key ones we will use are the Manufacturer Name or Make and the Model.  If desired, additional attributes could be added for spec data such as fuel type, empty weight, etc...

We will also create an instance attribute which will only be valid when a component - an instance of the product - is defined.  The instance attributes will be the aircraft registration.  When the attribute set is defined, we will include a serial number.

Start by defining the attribute for the Aircraft Make.  Open the Attribute Window and create a record for the AC Make.  Make it mandatory and set the Attribute Value Type to list as shown below.

![](/assets/Attribute%28make-list%29.png)

Next, open the Attribute Value tab and create two records for the relevant aircraft in operation: Cessna and Beechcraft.

![](/assets/AttributeValues%28make-list%29.png)

For the Aircraft Model attribute, create a new Attribute list as follows:

![](/assets/Attribute%28model-list%29.png)

Set the AC Model values to the models of interest.

![](/assets/AttributeValues%28model-list%29.png)

Now create the instance attribute for the AC registration.  Since the product is generic, the registration will be an instance attribute.  Make the Attribute Value Type a String and also make the attribute mandatory and an instance attribute.

![](/assets/Attribute%28reg%29.png)

#### 3. Create an Attribute Set

With the attributes defined, we can create an Attribute Set which will include these attributes and define a serial number as another instance attribute. Select the Serial No. and make it mandatory.

![](/assets/AttributeSet%28AC%29.png)

Under the Attribute Use tab, select the three attributes created above.

![](/assets/AttributeUse%28AC%29.png)

#### 4. Define the Component Product

We are now ready to define a product that makes use of the Attribute Set.  Open the Product Window and create an entry for the C-150L product.  Select "Track as Component" and set the Attribute Set to "Aircraft" as defined above.  In the Attribute Set Instance \(ASI\) field, click the helper button to open a dialog where the values of the Attributes can be completed.  Fill this in as shown below.

![](/assets/ProductASI%28new C-150L%29.png)

After saving the attribute set instance, the product record should appear as follows:

![](/assets/Product%28AC%29.png)

At this point we have a product and a product Attribute Set Instance.  Note that the ASI field does not contain a registration or a serial number.  These attributes of the ASI will be filled in when the product is referenced in a document or the Component Tracking window.

##### Defining Substitue Products

In some cases, it may be necessary to define multiple products for a component.  This can be helpful if there are several manufacturers of a replacement part, each using a different model and part number for compatible and interchangable parts.  Starter moters are a good example.  There are many suppliers that build or overhaul starter motors that are compatible with a given engine and which are interchangeable.  One make/model of started motor can be substituted for another in the engine assembly.

To define the list of acceptable substitutes, first create product records for the interchangeable parts.  Then, on at least one, but preferably all, of the products, open the Substitute tab of the Product Window and add the other interchangeable products.  If you only do this on one product, that product should be referenced in the main Product BOM.  It will appear as the "master product" on the Component BOM Line.  Having done this, when a sub-component is being created as part of a  component BOM, or replaced in a maintenance action, the new/replacement product will be selected from the master product and its set of substitues.  The figure below shows the Product Installed combobox expanded with a list of substitute products defined for the EQ starter on a O-200-A Continental Motor.

![](/assets/CT_CompBOMLineProdInstalledSubList.png)

#### 5. Define a Component Life Cycle Model

To make it easier to manage a large number of components, a Component Life Cycle Model can be used to define the life cycle.  When individual components are created, the model values are copied to the component, saving time in manual entry and ensuring that the life units and measures are accurate.

The Component Life Cycle Model can vary significantly from product to product.  Certain products have a life measured in time, others in use and some have an unlimited life.  When assessing the Life Used of a component, a source of data is required.  The Life Cycle Model allows the life usage source to be specified as follows:

* Aircraft - the component life is tied to an aircraft and the component must be identified on the Aircraft tab of the Fleet Management window.  The life of the component will match the airframe time of the aircraft.  Only the top level component that represents the aircraft should use this Life Usage Source.
* Count of Installations - used for components where the life is measured by the number of times the component is installed and removed.  In some cases, such as self-locking nuts, the item can be used once and should be scrapped once uninstalled.
* Inherit from Parent - here the sub component will measure its life in the same way as its parent component.  In this case, if the parent component life measure is increased by a unit, the sub-componet life will also be increased by a unit.  This is useful, for example, in aircraft parts that measure life in airframe hours.  The top level component would have a life usage source of Aircraft and all sub-components that have the Life Usage Source set to Inherit from Parent would be increased as the Aircraft airframe time was increased.
* Not Tracked - here the component life usage is not measured.  This is relevant where the life is measured by date/age and not usage.
* Use a Query - a specialized choice that allows the user to construct a query that will return the current life usage of a component based on data in the database.  The server can be configured to run the query periodically.

To create a model, open the Component Life Cycle Model window and create a record for Aircraft that have an unlimited life. Apply the model to the Aircraft product group so it will be used by all components from all products of that group.

Set the source of the life measurement to Aircraft and the life units to hours.  This means that the component life and the Aircraft airframe time will be linked.  For subcomponents, the life usage source can be set to Parent Component, in which case the sub-component's life will increase as the parent component's life increases.

![](/assets/CompLifeCycle%28Aircraft%29.png)

### 6. Creating a Component Manually

To create a component, a combination of Product and ASI needs to be defined on a document or in the Component Tracking window.  We will use the later to define the aircraft component.  Open the Component Tracking window and set the product to the generic C-150L product.  Note that the Life Usage Source is filled in as "Aircraft" from the model and the Life Use UOM is set to Hour.

![](/assets/CT_CompTrackingWindow%28C-150LNew%29.png)

The Attribute Set Instance field will be highlighted red, indicating it is mandatory as the Product has an Attribute Set that has instance attributes.  A manual entry of these values is required.  Click on the Attribute Set Instance helper button and the following dialog will appear.  Here, the product attribute values are read only and the instance attribute values can be set.  In this example, the Registration is set to C-FJZP and the Serial Number to the airframe serial number

![](/assets/CT_CompTrackingWindow%28C-150LNewASI%29.png)

After completing the Attribute Set Instance dialog and confirming the values, save the Component record.

In the History tab, there will now be a record that shows the Component was created.

![](/assets/CT_CompTrackingWindow-History%28C_FJZP%29.png)

Note that the Life Used amount in the Component Tracking window and history is zero.  To connect the component with the Aircraft, we need to add the Component link on the Fleet Maintenance window.

#### 7. Connect the Top Level component to an Aircraft

Open the Fleet Maintenance Window and find the record for C-FJZP.  Select the component just created in the "Top Component" field.  Save the record.

![](/assets/CT_FleetMaintenanceAircraft.png)

Return to the Component Tracking window and note that the Life Used has been filled in with the airframe life of the Aircraft.  From now on, as the Aircraft hours increase, the component life will also increase.

To create components for all other aircraft in the Fleet, only steps 6. and 7. need be repeated for each aircraft.

## Configuring Component Bills of Material

A component Bill of Material \(BOM\) is identical to a product BOM except the component BOM contains other components.

Configuring a Component BOM starts with a Product BOM.  The Product BOM is copied to every associated component as an empty BOM tree.  Sub components can be added to the "assembly" manually or through work order processes.

The initial configuration of the component is best performed manually.  The steps involved are:

1. Create Component Life Cycle Models, Attribute Sets and Products for each BOM line item.  There needs to be a product for each "assembly" level of the BOM as well as for the lowest level parts.
2. Construct the Product BOM for each assembly.
3. Create the top-level component for each assembly.
4. Populate the component assemblies with sub-components.

If changes are made to the Product BOM at a later time, a process called "Update Component BOMs" will make the same changes to all the effected components.

Constructing the Product BOM is done using the BOM tab of the Product Window.  The header of the BOM can be filled out as required but the **BOM Use must be set to "Master" **and the "Valid from" date set.  It is possible to create multiple BOM header records but the one used to make component BOMs will be one that has the "BOM Use" = "Master" with  "Valid from/to" date. The "Valid to" date can be blank.

BOM Line items will be applied to the component BOM only if the associated product has "Track As Component" selected.

Since most of the quantities of components are instances, the BOM quantity will be set to one \(1\) for the component lines where the product attribute set has instance attributes.



