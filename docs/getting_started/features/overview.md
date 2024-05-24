# GTFS Schedule Features

As the GTFS Reference format evolves to meet the current needs of transit systems, its functions can become increasingly complex. The **GTFS Features** are intended to provide a clear and definitive explanation of functionalities enabled by the GTFS Reference format. This helps transit agencies, vendors, consumers and researchers understand the capabilities of GTFS and answer the question: **What can I do with GTFS?** 

The following groups of features explain the purpose of each feature as well as the files and fields associated with them, helping users to understand which data is needed to support a specific feature.

## Base
These essential features form the core of a GTFS feed. They are the minimal elements needed to represent a transit service.

<div class="grid cards" markdown>

- :material-subway-variant:{ .lg .middle } __Agency__

    Details about the agencies responsible for the transit service.          
    
    [:octicons-arrow-right-24: Learn more](/getting_started/features/base/#agency)

- :material-subway-variant:{ .lg .middle } __Stops__

    Locations where a transit service picks up and drops off passengers.      

    [:octicons-arrow-right-24: Learn more](/getting_started/features/base/#stops)

- :material-subway-variant:{ .lg .middle }  __Routes__

    Elements of a transit route such as name and the type of service.       

    [:octicons-arrow-right-24: Learn more](/getting_started/features/base/#routes)

- :material-subway-variant:{ .lg .middle } __Service Dates__

    Structure to schedule trips and service exceptions.                      

    [:octicons-arrow-right-24: Learn more](/getting_started/features/base/#service-dates)

- :material-subway-variant:{ .lg .middle } __Trips__

    Association of transit vehicles to a route on given days.              

    [:octicons-arrow-right-24: Learn more](/getting_started/features/base/#trips)

-   :material-subway-variant:{ .lg .middle } __Stop Times__

    Arrival and departure times of the trips for each stop.                

    [:octicons-arrow-right-24: Learn more](/getting_started/features/base/#stop-times)

</div>

## Base add-ons
These features enhance a GTFS dataset, improving rider experience and facilitating collaboration between agencies, vendors, and data re-users. They may involve adding new fields to existing files or creating new files.

<div class="grid cards" markdown>

- :material-subway-variant:{ .lg .middle } __Feed Information__

    Information regarding the feed itself.                                

    [:octicons-arrow-right-24: Learn more](/getting_started/features/base_add-ons/#feed-information)

- :material-subway-variant:{ .lg .middle } __Shapes__

    Geographic path followed by a vehicle along a trip.                   

    [:octicons-arrow-right-24: Learn more](/getting_started/base_add-ons/#shapes)

- :material-subway-variant:{ .lg .middle } __Route Colors__

    Color scheme assigned to specific routes.                            

    [:octicons-arrow-right-24: Learn more](/getting_started/features/base_add-ons/#route-colors)

- :material-subway-variant:{ .lg .middle } __Bike Allowed__

    Capacity of vehicles to accommodate bicycles or not.                  

    [:octicons-arrow-right-24: Learn more](/getting_started/features/base_add-ons/#bike-allowed)

- :material-subway-variant:{ .lg .middle } __Headsigns__

    Signage used by vehicles indicating the trip’s destination.            

    [:octicons-arrow-right-24: Learn more](/getting_started/features/base_add-ons/#headsigns)

- :material-subway-variant:{ .lg .middle } __Location types__

    Locations within transit stations.                                    

    [:octicons-arrow-right-24: Learn more](/getting_started/features/base_add-ons/#location-types)

- :material-subway-variant:{ .lg .middle } __Frequencies__

    Services based on headways or frequencies.                           

    [:octicons-arrow-right-24: Learn more](/getting_started/features/base_add-ons/#frequency_based_services)

- :material-subway-variant:{ .lg .middle } __Transfers__

    Transfers between different transit services.                         

    [:octicons-arrow-right-24: Learn more](/getting_started/features/base_add-ons/#transfers)

-   :material-subway-variant:{ .lg .middle } __Translations__

    Service information in multiple languages.                            

    [:octicons-arrow-right-24: Learn more](/getting_started/features/base_add-ons/#translations)

- :material-subway-variant:{ .lg .middle } __Attributions__

    Organizations involved in the creation of the dataset.                

    [:octicons-arrow-right-24: Learn more](/getting_started/features/base_add-ons/#attributions)

</div>


## Accessibility
Accessibility features provide essential information for people with disabilities to access the service.

<div class="grid cards" markdown>

- :material-subway-variant:{ .lg .middle } __Stops Wheelchair Accessibility__

    Indicate whether wheelchair boarding is possible from a location.     

    [:octicons-arrow-right-24: Learn more](/getting_started/features/accessibility/#stops-wheelchair-accessibility)

- :material-subway-variant:{ .lg .middle } __Trips Wheelchair Accessibility__

    Indicate if a vehicle can accommodate riders using wheelchairs.       

    [:octicons-arrow-right-24: Learn more](/getting_started/features/accessibility/#trips-wheelchair-accessibility)

- :material-subway-variant:{ .lg .middle } __Text-to-speech__

    Conversion of text for stop names into audio.                         

    [:octicons-arrow-right-24: Learn more](/getting_started/features/accessibility/#text-to-speech)

</div>


## Fares
GTFS can model various fare structures, such as zone, distance, or time-of-day based fares. It informs riders of trip prices and payment methods.

<div class="grid cards" markdown>

-   :material-subway-variant:{ .lg .middle } __Fare Products__

    List the types of tickets or fares available to users.                   

    [:octicons-arrow-right-24: Learn more](/getting_started/features/fares/#fare-products)

-   :material-subway-variant:{ .lg .middle } __Fare Media__

    The media that can be used to hold and/or validate a fare product.        

    [:octicons-arrow-right-24: Learn more](/getting_started/features/fares/#fare-media)

-   :material-subway-variant:{ .lg .middle } __Route-Based Fares__

    Fares based on the route travelled.                                      

    [:octicons-arrow-right-24: Learn more](/getting_started/features/fares/#route-based-fares)

-   :material-subway-variant:{ .lg .middle } __Time-Based Fares__

    Fares based on time (peak/offpeak) or day (weekday/weekend).             

    [:octicons-arrow-right-24: Learn more](/getting_started/features/fares/#time-based-fares)

-   :material-subway-variant:{ .lg .middle } __Zone-Based Fares__

    Fares based on zone traveled.                                            

    [:octicons-arrow-right-24: Learn more](/getting_started/features/fares/#zone-based-fares)

-   :material-subway-variant:{ .lg .middle } __Fares Transfers__

    Fees or discounts applicable when transferring from one leg to another.  

    [:octicons-arrow-right-24: Learn more](/getting_started/features/fares/#transfer-fares)

-   :material-subway-variant:{ .lg .middle } __Fares V1__

    Legacy feature that models simpler fare information.                     

    [:octicons-arrow-right-24: Learn more](/getting_started/features/fares/#fares-v1)

</div>


##  Pathways

Pathways features allows to model large transit stations, so that riders are guided from entrances to boarding areas. They provide path details, estimated navigation times, and wayfinding systems.

<div class="grid cards" markdown>

-   :material-subway-variant:{ .lg .middle } __Pathways connections__

    Paths connecting relevant points within a station.                       

    [:octicons-arrow-right-24: Learn more](/getting_started/features/pathways/#pathways-basic-information)

-   :material-subway-variant:{ .lg .middle } __Pathway details__

    Additional details for stations' pathways.                               

    [:octicons-arrow-right-24: Learn more](/getting_started/features/pathways/#pathways-details)

-   :material-subway-variant:{ .lg .middle } __Levels__

    Levels within a station.                                                

    [:octicons-arrow-right-24: Learn more](/getting_started/features/pathways/#levels)

-   :material-subway-variant:{ .lg .middle } __In-station traversal time__

    Estimated time to navigate paths within a station.                      

    [:octicons-arrow-right-24: Learn more](/getting_started/features/pathways/#in-station-traversal-time)

-   :material-subway-variant:{ .lg .middle } __Pathways signs__

    In-station signage associated with a pathway.                           

    [:octicons-arrow-right-24: Learn more](/getting_started/features/pathways/#pathways-directions)

</div>

## Flexible services
Flexible services, or demand-responsive services, that do not follow regular schedules or fixed routes.

<div class="grid cards" markdown>

- :material-subway-variant:{ .lg .middle } __Continuous stops__

    When a user can be picked up and/or dropped off between stops.           
    
    [:octicons-arrow-right-24: Learn more](/getting_started/features/flexible_services/#continuous-stops)

- :material-subway-variant:{ .lg .middle } __Booking Rules__

    When users can reserve a trip on a demand-responsive service.            

    [:octicons-arrow-right-24: Learn more](/getting_started/features/flexible_services/#booking-rules)

- :material-subway-variant:{ .lg .middle } __Predefined Routes With Deviation__

    Vehicles that can briefly deviate from a route to pick up or drop off.   

    [:octicons-arrow-right-24: Learn more](/getting_started/features/flexible_services/#predefined-routes-with-deviation)

- :material-subway-variant:{ .lg .middle } __Zone-based Demand Responsive Services__

    Services that allow pick up/drop off at any location within a specific area.

    [:octicons-arrow-right-24: Learn more](/getting_started/features/flexible_services/#zone-based-demand-responsive-services)

- :material-subway-variant:{ .lg .middle } __Fixed-Stops Demand Responsive Services__

    Services that allow pick up/drop off at any location within a group of stops.
   
    [:octicons-arrow-right-24: Learn more](/getting_started/features/flexible_services/#fixed-stops-demand-responsive-services)

</div>
