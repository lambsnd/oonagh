# Response Time Measurement with Qualtrics

Once the participant starts the survey, they will be asked to enter an ID (e.g., name, username, or email address). This information will be used to record response times for that participant.

## Set up username variable

For this tutorial, we will call the **username** variable the one that identifies your participant. After you have added the username question, click on it to select. Under the **Edit question** panel on the left, select, under the menu :arrow_down_small: *Question behavior*, the option :radio_button: *Javascript*. 

Then add the following script for the data variable `responseTimeMeasurement`, replacing `999` with the [correct QID](https://www.qualtrics.com/support/integrations/api-integration/finding-qualtrics-ids/#LocatingQualtricsIDs), and :white_check_mark: save.

- Here is how to find the QID (also available [here](https://www.qualtrics.com/support/integrations/api-integration/finding-qualtrics-ids/#LocatingQualtricsIDs)):

1. On the top right corner, click your account picture
2. Select *Account Settings*
3. You should see four panels appear; click on *Qualtrics IDs*.
4. This section shows a list of all your available IDs for Surveys, User, Libraries, and more. Under Surveys, select the survey the question belongs to. **Make sure to select the correct Survey**-- since the QIDs are *unique to each survey*.
5. A list of questions and their IDs will pop up; select the one you need for the username ID.

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

Select question, and under the **Edit Question** panel on the left, select under the menu :arrow_down_small: *Question Behavior* the option :radio_button: *Javascript*.

Then add the following code for a data variable called `responseTimeMeasurement`:
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
