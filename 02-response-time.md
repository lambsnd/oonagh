# Response Time Measurement with Qualtrics

Once the participant starts the survey, they will be asked to enter an ID (e.g., name, username, or email address). This information will be used to record response times for that participant.

The first step in obtaining response time data using Qualtrics is to obtain *timestamps* from which you can derive response times. Timestamps are recordings of date and time data for when a certain action happens. In this case, we will record date and time data for every time a participant makes an answer choice.

To tell Qualtrics that you want to record timestamps, under the Survey panel, select **Survey flow** on the left and follow the steps: 

1. Click to :heavy_plus_sign: *Add a new Element Here*.
2. Select *Embedded Data*
3. Type a descriptive variable name, for example, `responseTimeMeasurement`.
4. Click again on :heavy_plus_sign: *Add a new Element Here* and select *Web Service*

## Set up username variable

For this tutorial, we will call the **username** variable the one that identifies your participant. After you have added the username question, click on it to select. Under the **Edit question** panel on the left, select, under the menu :arrow_down_small: *Question behavior*, the option :radio_button: *Javascript*. 

Then add the following script for the data variable `responseTimeMeasurement`, replacing `999` with the [correct QID](https://www.qualtrics.com/support/integrations/api-integration/finding-qualtrics-ids/#LocatingQualtricsIDs), and :white_check_mark: save.

> #### Here is how to find the QID (also available [here](https://www.qualtrics.com/support/integrations/api-integration/finding-qualtrics-ids/#LocatingQualtricsIDs)):
>
> 1. On the top right corner, click your account picture
> 2. Select *Account Settings*
> 3. You should see four panels appear; click on *Qualtrics IDs*.
> 4. This section shows a list of all your available IDs for Surveys, User, Libraries, and more. Under Surveys, select the survey the question belongs to. **Make sure to select the correct Survey**-- since the QIDs are *unique to each survey*.
> 5. A list of questions and their IDs will pop up; select the question used to collect the username.


```js
Qualtrics.SurveyEngine.addOnload(function()
{
    	Qualtrics.SurveyEngine.setEmbeddedData( 'responseTimeMeasurement', [{}]);
});

Qualtrics.SurveyEngine.addOnReady(function()
{
	var results = new RegExp('[\?&]' + "username" + '=([^&#]*)').exec(window.location.href);
	if (results!=null) {
		jQuery("#QR\\~QID999\\~1").val(results[1]);
	}//
});

Qualtrics.SurveyEngine.addOnUnload(function()
{
	/*Place your JavaScript here to run when the page is unloaded*/
});
```

## Set up response time data

Select the survey question for which you want to collect RT data. Under the **Edit Question** panel on the left, select under the menu :arrow_down_small: *Question Behavior* the option :radio_button: *Javascript*.

Then add the following code for the data variable `responseTimeMeasurement`:

```js
Qualtrics.SurveyEngine.addOnload(function()
{
	/*Place your JavaScript here to run when the page loads*/

});

Qualtrics.SurveyEngine.addOnReady(function()
{
	/*Place your JavaScript here to run when the page is fully displayed*/
    jQuery('input:radio').click(function(d){ 
        var responsetimedata = Qualtrics.SurveyEngine.getEmbeddedData('responseTimeMeasurement');
        var elem = d.currentTarget;
        var val = elem.getAttribute("id");

        var t = new Date();
        var values = [{val: val,
                      t: t}];    
        responsetimedata = responsetimedata.concat(values)
        Qualtrics.SurveyEngine.setEmbeddedData( 'responseTimeMeasurement', responsetimedata)
        console.log(responsetimedata);
    });
});

Qualtrics.SurveyEngine.addOnUnload(function()
{
	/*Place your JavaScript here to run when the page is unloaded*/

});
```


## Disclaimers

In this example, the Qualtrics question type is Matrix table or Multiple choice. This script may also work for other question types (not tested).
