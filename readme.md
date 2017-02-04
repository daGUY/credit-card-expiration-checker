# Credit Card Expiration Checker
* By James Scariati
* October 2015

## Description
Prevent users from entering an expired credit card month/year combination, by using the current date to disable options that occur in the past.

**[View Demo](http://scariati.kissr.com/github/cc-exp/)**

## Dependencies
* [jQuery](http://jquery.com)

## Use
Include jQuery and `jquery.ccExpirationChecker.min.js` in your HTML:

```html
<head>
	<script src="lib/jquery.min.js"></script>
	<script src="lib/jquery.ccExpirationChecker.min.js"></script>
</head>
```

Next, add `<select>` boxes to your HTML for the month and year dropdown menus, with `.month` and `.year` classes to denote each one:

```html
<select class="expiration month" autocomplete="cc-exp-month" x-autocompletetype="cc-exp-month">
	<option value="1">January</option>
	<option value="2">February</option>
	<option value="3">March</option>
	<option value="4">April</option>
	<option value="5">May</option>
	<option value="6">June</option>
	<option value="7">July</option>
	<option value="8">August</option>
	<option value="9">September</option>
	<option value="10">October</option>
	<option value="11">November</option>
	<option value="12">December</option>
</select>
<select class="expiration year" autocomplete="cc-exp-year" x-autocompletetype="cc-exp-year">
	<option value="2016">2016</option>
	<option value="2017">2017</option>
	<option value="2018">2018</option>
	<option value="2019">2019</option>
	<option value="2020">2020</option>
	<option value="2021">2021</option>
	<option value="2022">2022</option>
	<option value="2023">2023</option>
	<option value="2024">2024</option>
	<option value="2025">2025</option>
</select>
```

Note: the plugin empties the `<select>` boxes and populates them dynamically, using the current date to determine the range of year options. The hardcoded `<option>` elements simply provide a fallback in case JavaScript is disabled or fails to load.

Finally, call the plugin on the `<select>` boxes:

```javascript
$(".expiration").ccExpirationChecker();
```

## Options
The following options are available:

```javascript
$(".expiration").ccExpirationChecker({
	monthInput: "cardExpirationMonth",
	yearInput: "cardExpirationYear",
	yearRange: 10
});
```

* `monthInput`: the ID to use for the Month dropdown menu
* `yearInput`: the ID to use for the Year dropdown menu
* `yearRange`: the range of years to display in the Year dropdown menu, starting from the current year. Defaults to `10`

## Notes
The functionality is based on the following rules:

* If the user selects a month earlier than the current month, the current year will be disabled
* If the user selects the current year, any month earlier than the current month will be disabled

Given these rules, it's impossible to enter a date that occurs in the past.

For example, if it's currently October 2015:

* Selecting April will disable the option for 2015 (April 2015 occurs in the past)
* Selecting December will enable the option for 2015 (December 2015 occurs in the future)
* Selecting 2015 will disable all months earlier than October (September 2015 and earlier occur in the past)

Note that in the last example, selecting 2015 is only possible if the Month dropdown menu is either left blank or set to October (the current month) or later. Otherwise, the option for 2015 would be disabled like in the first example.