# Scenarios

```
### 
Maintenance Plans

### 
For a checklist we use a multi-value picklist and ask the user to slide over the activities that they have completed. To make the values reportable, we have a formula field for each pickist value to turn a checkbox on if that value is selected in the multi-value field.

### 
Here's our scenario, we have a call center that will take the customer's call and dispatch a work order/service appointment. When that happens, we have the auto-schedule in play and the system assigns the closest engineer as the service resource. But, the engineer may go back to the facility the next day so they have the ability to create a new service appointment. We do not want the system to go though the logic and possibly find another agent and assign them to the appointment. So, I need an ability to have this situation bypass the auto-scheduling and take into consideration that the engineer opened it themselves and it should assign them as the Service Resource.
>>
managed this through a "Self Dispatch" process which I have designed, on the create appointment page i have added a checkbox self dispatch and this is automatically checked on if the user is an engineer, then in the background I have process builder on create of the SA which checks this checkbox and then runs a flow, the flow then looks up the service resource for the user and creates the service resource document which is associated to the engineer and this is all you need for the appointment to show as assigned to the engineer and it will appear in the app.
You can use the same concept in your quick action.

### 
@Lance Riviere
 (Customer) our issue is due to picture upload in the flow. We will try the fix as suggested & let you know if it works. Thanks.

### 
integrating Salesforce FSL and Communities to enable consumers to book their own service appointments
>> using the book appointment snap in. Works fine in communities  

### 
I am having some issues trying to test my logic with the mobile app. All of the appointments that will be set for our company will be in EST, however I am in PST so while I am trying to test my logic, this is being taken into account when it offers the time slots, leaving a 36+ hour travel time. Is there a way to fake/force my current geocoding location and not what my mobile device detects. I have an iPad and there are no free solutions to do this that I can find so my hope is there is some object in Salesforce that this information is stored on and I can disable the location services on the iPad and update that object manually.
>>
Chad Barbour (Customer)
@Jason Lari (Deck Helmet) Setting the mobile app aside for a moment, the lat/long of the Service Territory Member is the first place the scheduling logic looks for travel calcs. If that's not populated, it uses the lat/long on the Service Territory. This will allow to you set your location used for scheduling to someplace closer to your test customer. (If neither of those are populated, then there's no travel time calculated for the first appointment of the day.)

If you're scheduling using the global actions, the time slots and candidates are presented using the timezone of the service territory associated with the appointment. As with any date/time value in Salesforce, this is stored in GMT (but the timezone adjustment has been taken into consideration). The platform displays date/time values on the page layouts based on the user's timezone. So it's likely you'll see an 8 AM EST appointment show as 6 AM PST if you're looking at the record detail. The global actions would have shown 8 AM in this example.

As for the mobile app, I believe the times are displayed using the device's timezone and turn-by-turn directions will be based on your current location.

I typically test things by setting the ST address to some point relevant to my use case and not worrying about my mobile app. 

The exception to the rule is the Emergency Wizard. This global action uses the last known location on the Service Resource for immediate scheduling.

### 
When it comes to the available time slots that we need to have populate, this will be different from work type to work type. Using operating hours this can be achieved, however when I create a work order with the territory, and the specific operating hours I want it to use, no matter what I cannot get those time slots using the book appointment option, it always defaults to the default operating hours that are set on the settings. However it works as expected with the apex class I built to pull time slots. Why does it not work with the book appointment buttons regardless of what hours are selected on the work order or service territory and how can we make the book appointment button use the operating hours that are set on the work order/service appointment or service territory?

>>
Chad Barbour (Customer)
@Jason Lari (Deck Helmet) The time slot definition for the Book Appointment action is first defined by the operating hours populated on the related Work Order's Entitlement (assuming the WO is the parent of the SA). If that's blank, then it reverts to the default operating hours defined in the global action settings. If the goal is to use the global actions, I recommend leveraging Entitlements to provide the operating hours.


### Customize the Dispatcher Console with Field Sets
https://help.salesforce.com/articleView?id=pfs_fieldsets.htm


```
