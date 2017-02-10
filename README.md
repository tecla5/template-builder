# Template builder

This project contains the HTML templates used to generate PDFs that we send to our customers.

## Structure

- `/bin` contains binaries
- `/builder` contains template builders
- `/content` contains `.json` and `.yaml` files which describe how to generate the template and what content (text) goes where.
- `/generator` contains a script to generate a template (for a specific 
- `/html` contains static `.html` files that can be used to test the PDF generation and act as blueprints for the templates
- `/pdfs` contains the target/sample pdfs that the pdf generation should match
- `/style` contains the styles in `.stylus` or plain `.css`
template library) given a content file and a builder
- `/templates` contains the actual templates to be used in a Template service

## Supported templating engines

See this [list of engines](https://colorlib.com/wp/top-templating-engines-for-javascript/)

We would like to support *EJS* and *doT* for now.

## Usage

Create a content file for the template to be created. This file will describe the basic layout (sections, text, fields etc) and the order of these.

`account.json` or `account.yaml`

Select an existing builder or design a new one (in JavaScript).

Run the generator with the builder `-b` and content file `-c` to generate one or more template files in specific template engine formats `-f`.

`$ ./bin/template generate child-account -b account-questionaire -c child-account -f dot`

```html
<div>Hi {{=it.name}}!</div>
<div>{{=it.age || ''}}</div>
```

Generates template `child-account.dot` in `/templates`

Note: See [mock-api converter](https://gitlab.intranet.ginmon.com/ginmon/mock-api/blob/master/convert/execute.js) for example on how to write a Node.js executable. You could also use [commander](https://www.npmjs.com/package/commander)

Run the template with a data file and a css file to generate a static html file.

`$ ./bin/template run child-account.dot -s basic`

Generates `child-account.html` with basic styling

Validate that the html can be used to generate a satisfactory pdf.

`$ ./bin/pdf child-account`

The pdf binary should use our pdf service or [wkhtmltopdf](https://github.com/wkhtmltopdf/wkhtmltopdf) installed locally (f.ex via Docker)



