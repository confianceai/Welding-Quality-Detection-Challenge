# Welding Quality Detection Challenge Webpage

This Webpage is the official documentation of the Welding Quality Detection Challenge, organized by the [IRT SystemX](https://www.irt-systemx.fr/) and [Confiance AI](https://www.confiance.ai/).

Deployed at https://etaia.github.io/Welding-Quality-Detection-Challenge/

## Running the documentation locally

### Requirements

- [Node.js](https://nodejs.org/en/)

### Installation

Clone this repository on your computer.

Install the dependencies.

```sh
npm install
```

You can now run the development server.

```sh
npm run serve
```

Your documentation is now available at [http://localhost:8080/](http://localhost:8080/).

---

### Spell check

This documentation comes with a spell check pipeline that will check the spelling of your documentation.

To run the spell check manually (before pushing your changes), you can run the following command:

```sh
npm install cspell -g
cspell .
```

To add a word to the dictionary, edit the [`cspell.json`](cspell.json) file.
