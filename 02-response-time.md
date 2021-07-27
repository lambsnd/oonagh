# Response Time Measurement with Qualtrics

Once the participant starts the survey, they will be asked to enter an ID (e.g., name, username, or email address). This information will be used to record response times for that participant.

This tutorial explains how to record response times per question in Qualtrics, when using the Matrix Table (or Multiple-Choice) question format. The javascripts shared here records [*timestamps*](https://en.wikipedia.org/wiki/Timestamp) (date and time) each time the participant makes an answer choice.

## Set up Embedded Data

To tell Qualtrics that you want to record timestamps, under the "Survey" tab, select **_Survey flow_** on the left panel (it may show four icons; survey flow is the second) and follow these steps: 

1. Click to :heavy_plus_sign: *Add a new Element Here*.
2. Select *Embedded Data*
3. Type a descriptive variable name, for example, `responseTimeMeasurement`.
4. Save changes and go back to menu the **_Builder_** menu (first icon on left panel).

## Set up a Username Variable

For this tutorial, we will call the **Username** variable the one that identifies your participant. 

1. After you have added the username question, click on it to select it. 
2. Under the **_Builder_** menu, scroll down to the section :arrow_down_small: *Question behavior*, and select the option *Javascript*. 
3. Add the following script for the data variable `responseTimeMeasurement`, replacing `999` with the [correct QID](https://www.qualtrics.com/support/integrations/api-integration/finding-qualtrics-ids/#LocatingQualtricsIDs), and :white_check_mark: save. More instructions on how to find QIDs are given below.

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

> #### Here is how to find the QID (also available [here](https://www.qualtrics.com/support/integrations/api-integration/finding-qualtrics-ids/#LocatingQualtricsIDs)):
>
> 1. On the top right corner, click your account picture
> 2. Select *Account Settings*
> 3. You should see four panels appear; click on *Qualtrics IDs*.
> 4. This section shows a list of all your available IDs for Surveys, User, Libraries, and more. Under Surveys, select the survey the question belongs to. **Make sure to select the correct Survey**-- since the QIDs are *unique to each survey*.
> 5. A list of questions and their IDs will pop up; select the question used to collect the username.


## Set up Response Time Data

After editting your username question, you are ready to set up data collection directly in your survey question. Note that the method described here is only for Matrix Table or Multiple-Choice type of questions. 

1. Select the survey question for which you want to collect RT data (click on it).
2. Under the **_Builder_** menu, scroll down to select *Javascript* under the menu :arrow_down_small: *Question Behavior*.
3. Add the following code for the data variable `responseTimeMeasurement`:

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

4. Save your changes.
5. Publish the survey.
6. Test out your data collection: the last column of your data should be named "responsetimeMeasurement".

## Disclaimers

In this example, the Qualtrics question type is Matrix table or Multiple-choice. This script may also work for other question types (not tested).

&copy; Javascript code by [Alex Brodersen](https://www.github.com/alexbrodersen) and tutorial by [Dani Rebouças Ju](https://www.github.com/drebouca).
