# Response Time Measurement with Qualtrics

Once the participant starts the survey, they will be asked to enter an ID (e.g., name, username, or email address). This information will be used to record response times for that participant.

## Set up ID variable

Select ID question, and, under the **Edit question** panel on the left, select under the menu :arrow_down_small: *Question behavior* the option :radio_button: *Javascript*. 

Then add the following script, replacing **999** with the correct **QID** (question ID), and :white_check_mark: Save.

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
