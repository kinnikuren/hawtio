### Camel

Click [Camel](#/jmx/attributes?tab=camel) in the top navigation bar to view all the running Camel Contexts in the current JVM. (The selection will not appear on the navigation bar if there is no Camel running).

The Camel plugin allows you to view all the running Camel applications in the current JVM.
You can among others see the following details:

* Lists of all running Camel applications
* Detailed information of each Camel Context such as Camel version number, runtime statics
* Lists of all routes in each Camel applications and their runtime statistics
* Manage the lifecycle of all Camel applications and their routes, so you can restart / stop / pause / resume, etc.
* Graphical representation of the running routes along with real time metrics
* Profile the running routes with real time runtime statics; detailed specified per processor
* Live tracing and debugging of running routes


#### Camel Tree ####

On the left hand side is the Camel Tree which lists all the running Camel applications in the JVM.

![Camel Tree](app/camel/doc/img/camel-tree.png "Camel Tree")

And on the main view area is a table that lists runtime metrics of each Camel application, as shown below:

![Camel Attributes](app/camel/doc/img/context-attributes.png "Camel Attributes")

Clicking on a Camel application in the tree, selects it, and allows you to see more details about that particular Camel application.


#### Camel Application ####

In the Camel tree expand the selected Camel application to access more information such as the running routes.
When clicking on the routes node in the tree, the main page lists a table of all the routes and runtime metrics as shown below:

![Route Attributes](app/camel/doc/img/route-attributes.png "Route Attributes")

In the table you can select route(s) and use the buttons to control their lifecycle, such as stopping and starting routes.


#### Camel Route ####

By selecting a route in the Camel Tree

![Select Route](app/camel/doc/img/route-select.png "Select Route")

... gives access to a full range of *hawt* functionality. For example the diagram tab, shows a real time visual representation of the route, as shown below:

##### Diagram #####

![Route Diagram](app/camel/doc/img/route-diagram.png "Route Diagram")

If you however the mouse over the nodes in the diagram, a tool tip is presented with additional details.

##### Source #####

The Source tab shows a XML representation of the route.
Camel is able to output any route as XML even if the route was originally developed using Java, Groovy, or Scala code.

![Route Source](app/camel/doc/img/route-source.png "Route Source")

You can even edit the source code, for example we could add a predicate for checking if the message is from Paris in France,
such as adding the following to source code, and clicking the Save button.

    <when customId="true" id="isCityParis">
      <xpath>/person/city = 'Paris'</xpath>
      <to uri="file:target/messages/fr" customId="true" id="messagesFR"/>
    </when>

And the route would be updated at runtime, which we can see in the Diagram tab as shown below:

![Route Updated](app/camel/doc/img/route-updated.png "Route Updated")


##### Profile #####

The profile tab shows a real time profile of the selected route.

The top shows the accumulated profile for the route. Each of the following rows is a break down per processor.

In the screen shot below, we can see the route has processed 3 messages, with a mean processing time of 56 ms per message,
and a total of 169 ms. We can also see from the self time of the last 2 rows, that they only use 1 and 12 ms, so the
bottleneck is at '''choice1'' which has a self time of 146 ms. The '''choice1''' is a Content Based Router EIP that
uses an XPath expression which means the majority of processing time is spent evaluating XPath expressions.

![Route Profile](app/camel/doc/img/route-profile.png "Route Profile")

The metrics shown in the table are as follows:

* Count = Total number of messages processed
* Last = Time in ms. processing the last message.
* Delta = Difference in +/- ms. processing the second-last and last message.
* Mean = Time in ms. for the average processing time.
* Min = Time in ms. for the lowest processing time.
* Max = Time in ms. for the highest processing time.
* Total = Accumulated self time in ms. for processing messages.
* Self = Total time in ms. for processing message in this processor only.




If you select a CamelContext, Route or Endpoint you can then view the **Attributes** or **Charts** of the  various underlying MBeans.

You can use the **Diagram** tab to view a graphical representation of the running routes along with real time runtime metrics. If you select a single route instance then the diagram just shows that route only.

If you select a **Route** you can then use the **Trace** tab to perform diagnostic tracing of routes; to see every version of each message as it flows around a route.