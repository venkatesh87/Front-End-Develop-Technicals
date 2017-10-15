## Study-javascript-json

### JS

```javascript
// A JSON object is basically a JavaScript object
var header = document.querySelector('header');
var section = document.querySelector('section');
// we are going to store the URL of the JSON file we want to retrieve in a variable
var requestURL = 'https://mdn.github.io/learning-area/javascript/oojs/json/superheroes.json';
// To create a request, we need to create a new request object instance from the XMLHttpRequest constructor, using the new keyword.
var request = new XMLHttpRequest();
// Now we need to open a new request using the open() method, request.open('HTTP', URL JSON);
request.open('GET', requestURL);
// Here we are setting the responseType to JSON, so the server will know we want a JSON object returned, and sending the request with the send() method
request.responseType = 'json';
request.send();
// The last bit of this section involves waiting for the response to return from the server, then dealing with it
request.onload = function() {
  // we are going to store the response of the Server file we want to retrieve in a variable
  var superHeroes = request.response;
  populateHeader(superHeroes);
  showHeroes(superHeroes);
}
// Now we've retrieved our JSON data, let's make use of it by writing the two functions we referenced above
function populateHeader(jsonObj) {
  var myH2 = document.createElement('h2');
  myH2.textContent = jsonObj['squadName'];
  header.appendChild(myH2);

  var myPara = document.createElement('p');
  myPara.textContent = 'Hometown: ' + jsonObj['homeTown'] + ' // Formed: ' + jsonObj['formed'];
  header.appendChild(myPara);
}

function showHeroes(jsonObj) {
  var heroes = jsonObj['members'];

  for (var i = 0; i < heroes.length; i++) {
    var myArticle = document.createElement('article');
    var myH3 = document.createElement('h3');
    var myPara1 = document.createElement('p');
    var myPara2 = document.createElement('p');
    var myPara3 = document.createElement('p');
    var myList = document.createElement('ul');

    myH3.textContent = heroes[i].name;
    myPara1.textContent = 'Secret identity: ' + heroes[i].secretIdentity;
    myPara2.textContent = 'Age: ' + heroes[i].age;
    myPara3.textContent = 'Superpowers:';

    var superPowers = heroes[i].powers;
    for (var j = 0; j < superPowers.length; j++) {
      var listItem = document.createElement('li');
      listItem.textContent = superPowers[j];
      myList.appendChild(listItem);
    }

    myArticle.appendChild(myH3);
    myArticle.appendChild(myPara1);
    myArticle.appendChild(myPara2);
    myArticle.appendChild(myPara3);
    myArticle.appendChild(myList);

    section.appendChild(myArticle);
  }
}
```

### HTML

```javascript
<div id="wrapper">
  <div id="header">
    <div class="container">
      <div class="row">
        <div class="col-lg-12 col-md-12 col-sm-12 col-xs-12">
          <p>Header</p>
        </div>
      </div>
    </div>
  </div>
  <div id="main-content">
    <div class="container">
      <div class="row mbt">
        <div class="main-content col-xs-12">
          <h3 class="mb20">Danh sách sinh viên ban đầu</h3>
          <header>
          </header>
          <section>
          </section>
        </div>
      </div>
    </div>
  </div>
</div>
```
