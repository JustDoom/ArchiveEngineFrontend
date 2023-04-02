# Archive Engine Frontend

[![Discord Server](https://img.shields.io/discord/979589333524820018?color=7289da&label=DISCORD&style=flat-square&logo=appveyor)](https://discord.gg/k8RcgxpnBS)

This is the repository for the frontend of the Archive Engine website. It is built with NuxtJS.

## TODO

- [x] Add pagination
- [x] Add loading feedback
- [x] Add sorting by different columns (timestamp, url, status code and mimetype)
- [x] Add a statistics page
- [ ] Add error feedback
- [ ] Add the options/filtering/page as a url parameter for easy sharing/modifying
- [ ] Allow changing of the page size

## Usage

### Requirements

- NodeJS
- Yarn

### Installation
Make sure to install the dependencies

```bash
yarn install
```

### Development

Start the development server on http://localhost:3000

```bash
yarn dev
```

### Production

Build the application for production:

```bash
yarn build
```
