# Parsing XML Data

## Fetching and Reading XML Data

XML File

```read.xml```

```
<?xml version="1.0" encoding="utf-8" ?>
<root>
    <houses>
        <house id="2">Lannister</house>
        <house id="4">Stark</house>
        <house id="1">Greyjoy</house>
        <house id="3">Targaryen</house>
        <house id="8">Tyrell</house>
        <house id="9">Arryn</house>
        <house id="5">Martell</house>
        <house id="7">Baratheon</house>
        <house id="6">Frey</house>
        <house id="10">Bolton</house>
        <house id="11">Florent</house>
        <house id="12">Tully</house>
    </houses>
    <swords>
        <sword owner="Joffrey Lannister">Widows Wail</sword>
        <sword owner="Arya Stark">Needle</sword>
        <sword owner="Brienne of Tarth">Oathkeeper</sword>
        <sword owner="Samwell Tarly">Heartsbane</sword>
        <sword owner="Eddard Stark">Ice</sword>
        <sword owner="Jon Snow">Longclaw</sword>
    </swords>
</root>
```

HTML:
```
<body>
  <header>
    <h1>Reading Data from XML files</h1>
  </header>
  <main>
    <ul id="swords"></ul>
    <ul id="houses"></ul>
    <pre id="output"></per>
  </main>
</body>
```

Script:
```
document.addEventListener('DOMContentLoaded', () => {
  let url = "read.xml"
  fetch(url)
  .then(response => response.text())  // text, json, blob methods
  .then(data => {
    console.log(data); // string
    let parser = new DOMParser();
    let xml = parser.parseFromString(data, "application/xml");
    document.getElementById('output').textContent = data;
    console.log(xml);
    buildHouseList(xml);
    buildSwordList(xml);
  })
})
```
> xml variable is the html representation

> In XML or HTML, there is the 3 main types of nodes: element nodes, text nodes, attribute nodes

## Get string inside of the text node

```
<house id="2">Lannister</house>
```


```
function buildHouseList(x){
  let list = document.getElementById('houses');
  let houses = x.getElementsByTagName('house');

  for(let i=0; i < houses.length; i++){
    let li = document.createElement('li');
    let house = houses[i].firstChild.nodeValue; // the String
    li.textContent = house;
    list.appendChild(li);
  }
}
```

## Get the text and the value from the attributes

```
function buildSwordList(x){
  let list = document.getElementById('swords');
  let swords = x.getElementsByTagName('sword');

  for(let i=0; i < swords.length; i++){
    let li = document.createElement('li');
    let swordName = swords[i].firstChild.nodeValue; // the String
    let person = swords[i].getAttribute('owner'); // the Attribute
    li.textContent = `${swordName} - ${person}`;
    list.appendChild(li);
  }
}
```


