# JS--Promise

JavaScript Promises - Explain like I am Five:

[Article Link](https://blog.greenroots.info/javascript-promises-explain-like-i-am-five)

The Jack and Jill story which has grandparents(as consumers). The grandparents are also busy discussing about the daily routine which is they are not waiting for water but are working and will start cooking once the kids are back with water.

There can be two possibilities: 
1. Jack can come down with the water.
2. Jack fell down (disaster) and did not get the water.

In this short story, there is a promise of getting the water using the activity of fetching it. The promise can get fulfilled(getting the water) by the kids or reject due to the disaster. Also, grandparents were not sitting idle and were planning their day.

The JS promises also work in a similar way. We create them to fetch asynchronously(configuration, data store) which means we do not want to wait for the response but we can continue to work on the response when its available. <br>

<table><thead><tr><th>In Real Life with JS</th><th>In Our Story</th></tr></thead><tbody><tr><td>Promise </td><td>Water fetching by Jack and Jill</td></tr><tr><td>Executor Function </td><td>Fetch the Water </td></tr><tr><td>Activity</td><td>Fetch</td></tr><tr><td>Expected data in response </td><td>Water</td></tr><tr><td>Consumer </td><td>Grandparents </td></tr><tr><td>Resolve/fullfilled</td><td>Successfully get the water </td></tr><tr><td>Reject </td><td>Disaster / not get water</td></tr><tr><td>Task after getting the data </td><td>Cooking</td></tr></tbody></table>
