# Blup

Blup is a small program which turns a JSON file into a HTML file based on a Jinja template file. The program needs a json source file and a Jinja html template.

## Installation

```bash
$ pip install blup
```

## Usage

You need to prepare two files :
* a JSON file with all the data you'd like put into your template. The root element needs to be an object (not a list).
* a template file following Jinja's rules. You can check them out [on their doc](https://jinja.palletsprojects.com/en/3.1.x/templates/).

Then, once everything is prepared, you need to run :

```bash
$ blup template.html source.json >> output.html
```

You can also run blup as a server (constantly listening for json modifications). For that, use this command :

```bash
$ blup template.html source.json -o output.html --serve
```

## Example

Imagine you'd like to build a small HTML page showing your resume. You start by writing all the informations needed in a json file.

```json
{
  "name": "César Pichon",
  "occupation": "Student in computing sciences",
  "studies": [
    {
      "name": "Bachelor of Social sciences",
      "date": "2018-2021"
    },
    {
      "name": "Bachelor of Computing sciences",
      "date": "2021-2023"
    }
  ]
}
```

Then, you write a Jinja template :

```jinja
<!DOCTYPE html>
<html>
  <head>
    <title>Resume</title>
  </head>
  <body>
    <h1>{{ name }}</h1>
    <h2>{{ occupation }}</h2>
    <p>
      <h3>Studies</h3>
      <ul>
        {% for diploma in studies %}
          <li><b>{{ diploma.name }}</b> - {{ diploma.date }}</li>
        {% endfor %}
      </ul>
    </p>
  </body>
</html>
```

Finally, your run blub and get the following result :

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Resume</title>
  </head>
  <body>
    <h1>César Pichon</h1>
    <h2>Student in computing sciences</h2>
    <p>
      <h3>Studies</h3>
      <ul>
          <li><b>Bachelor of Social sciences</b> - 2018-2021</li>
          <li><b>Bachelor of Computing sciences</b> - 2021-2023</li>
      </ul>
    </p>
  </body>
</html>
```
