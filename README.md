# Guide connection for Apache Marmotta and QGIS
This is just a public guide that shows how to stablish a connection between Apache Marmotta and QGIS. This process can be applied for any triple store that has an SPARQL endpoint enabled.

For this process, we used the plugin SPARQLing unicorn. The description process is shown below.

---
## Plugin installation

1. Download the plugin “SPARQLing Unicorn QGIS Plugin” in ZIP form from this [link](https://plugins.qgis.org/plugins/sparqlunicorn/).
2. Open Qgis and go to the "Add-ons" tab and click on "Manage and install add-ons".
3. Then a window will open containing 5 options. Click on "Install from ZIP".
4. Click on the 3 dots [...] and the file explorer will open.
5. We look for and select the plugin that we previously downloaded.
6. Wait and the plugin will be installed in our QGis.

---
## Setup connection

To establish connection between QGIS and Apache Marmotta we will do the following
1. In QGis, look in the task bar for the “Vector” tab, place the cursor on “SPARQLing Unicorn QGIS Plugin” and click on “Adds GeoJSON layer from a Wikidata”.
2. A new window will open, look for and click on “Configure TripleStores” located on the right side of the window.

![SPARQLing Unicorn](https://user-images.githubusercontent.com/46234487/141689686-770f48e4-36d0-4555-b41d-5ea331a31fef.png)

3. Another window will open and we will verify that the "File" option is selected in the "Choose Triple Store" section.
4. In the field "Triple Store Name" we enter the name with which we will identify our triple store within Qgis. In our case it is Apache Marmotta.
5. In the "Triple Store URL" field we will enter the URL of the SPARQL endpoint where we want to connect. In the case of Apache Marmotta it is the following URL http: // ip6-localhost: 8080 / marmotta / sparql / select
6. We click on the option "Test Connection." If everything has gone well, we will get a dialog box that tells us that the URL entered corresponds to a valid SPARQL endpoint as shown in the following image.

![Connection test](https://user-images.githubusercontent.com/46234487/141689730-4d9ae2f6-f04f-4696-a146-85cbedd825f9.png)

7. Then we will click on the option "Detect Configuration" to load the geospatial metadata of the endpoint. A message will appear that will tell us that it found valid information and that if we want to add said SPARQL endpoint to QGis. We will say yes and wait for it to finish to register the endpoint in QGis.

![Success message](https://user-images.githubusercontent.com/46234487/141689758-c475ffc8-c02e-41f0-bc93-5714598d41be.png)


8. We click on “Apply” and close the window
9. If everything went well, we return to the first window, we click on the "Select endpoint" dropdown and our endpoint will be displayed there with the name that has been saved. In our case it was saved as "Apache Marmotta". After having selected our endpoint, we will be ready to execute our queries in the text box below the options.

![Apache Marmotta in QGIS through SPARQLinn unicorn plugin conn](https://user-images.githubusercontent.com/46234487/141689794-e5941d7f-837d-4ce2-8fce-66a72033ed1a.png)

---
## Example
To know how to execute and load data to QGIS, we'll show you how to do it with an example.

---

Execute the SPARQL query shown below.

![SPARQL Query](https://user-images.githubusercontent.com/46234487/141689998-f35abd71-c8a5-4162-90f0-ac14d8a0bbf5.png)

1. We open QGIS
2. Click on task bar -> Vector -> SPARQL Unicorn Wikidata Plugin -> Adds GeoJSON layer from a Wikidata.
3. In the new window, click on the “Select endpoint” section and select “Apache Marmotta”.
4. We insert the above query in the "Valid Query" text box. It should look something similar to the following image.

![Query in SPARQLing plugin](https://user-images.githubusercontent.com/46234487/141690058-d326335c-5c0a-4d6a-8fc9-b999cb11ad9c.png)

6. Since the query contains 2 variables associated with the geometries,? GeoProv and? GeoPlace, as well as 2 variables with information associated with each variable,? TitleProv and? TitlePlace respectively, the plugin must be adjusted so that it reads properly each each geometry and its name since the plugin requires 2 input parameters: the name of the variable with geometry information and the variable that contains the geometry in WKT format. For each tuple it is necessary to adjust the plugin and execute the query again since each execution implies a new layer to be imported in QGIS (Layer). In this case the tuples are as follows.


| # Execution | Geometry variable | Item variable
| --- | --- | --- |
| 1 |	GeoProv |	titleProv |
| 2 |	geoPlace | titlePlace |

7. Click on "Configure TripleStore"
8. Select the appropriate triple store, which in this case is Apache Marmotta.
9. Modify the main SELECT by using variable aliases.
10. Since the plugin does not allow changing the name of the variables that it will read, “geo” and “item”, we will change the main SELECT variable like this: “? GeoProv” by “(? GeoProv as? Geo)” and “? TitleProv "By" (? TitleProv as? Item) ". In this way we will no longer change the name of our variable in each part that appears in our query. It should look similar to the following image.

![Plugin update](https://user-images.githubusercontent.com/46234487/141690400-62857fbd-12eb-445a-a2e9-4bf83152dfa2.png)


12. Then we click on the "add layer" button. The query will be executed and if everything went well, a new layer will be added to QGIS.
13. Subsequently, you must do the same for the second variable, “? GeoPla” for “(? GeoPlace as? Geo)” and “? TitlePlace” for “(? TitlePlace as? Item)”, and we will have the 2 layers ready added in our QGIS.


 ---
 ## Results
 
 The geometries of the provinces are loaded in a single layer.
 
 ![Provinces' geometries](https://user-images.githubusercontent.com/46234487/141690441-43d5c2fa-99af-44b7-bb36-728c156771b5.png)


The museum geometries from the 2nd SPARQL endpoint are loaded as a second layer in QGIS.

![Museums' geometries](https://user-images.githubusercontent.com/46234487/141690460-c6a0fbb8-97c0-4edb-8c9b-3bd753d1ea27.png)


---
### Thanks for reading our article :)
