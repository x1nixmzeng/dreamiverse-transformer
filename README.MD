# Dreamiverse Transformer

This project aims to reverse engineer the user-generated content in the PS4 videogame **Dreams** - from [Media Molecule](https://www.mediamolecule.com/).

Why? **Dreams** hits [end-of-life in September 2023](https://www.pushsquare.com/news/2023/04/media-molecule-to-cease-live-service-for-dreams-now-working-on-a-new-project), where it will no longer receive official updates (the servers are not going offline, but it is no longer receiving support).

*The project name is a lazy reference to an internal server codename ("ultra magnus")*

### The Early Promise

In March 2020, it was suggested that **Dreams** would allow "[creators to use their content \[...\] outside of Dreams](https://twitter.com/mediamolecule/status/1238482258186711040)".  The scope of this was vague, and this was limited to a beta application form to allow use of content for "business purposes".

*Archived: https://web.archive.org/web/20200425220034/https://docs.indreams.me/en/help/beta-evaluation*

Further reading: https://atelier.net/insights/media-molecule-dreams-of-commercial-success


## Progress

- [x] Investigate data formats on disc (game package)
- [x] Investigate web api
- [ ] Backup Dreams creations
- [ ] Write a model viewer (or at least document the requirements)

### Summary

|  | Notes |
| -- | -- |
|  Engine |  [BubbleBath](https://www.mediamolecule.com/blog/article/announcing_our_winning_engine_name_for_dreams) (in-house engine) |
| Language | C++ |
| Tech | json, gnf textures, proprietary data formats, web services |
| Techniques | sdf, [constructive geometry](https://en.wikipedia.org/wiki/Constructive_solid_geometry)  |
| Licenses | pffft, FTTPACK, xxHash, lz4 | 


### First Impressions

* There is an existing project that reverses the frontend website / server endpoints and authentication
  https://github.com/jaames/dreams-api
* There is some raw 3d model data for the imps in obj format?
* Some textures use the gnf format typical of other Playstation titles ([gnf texture reader](https://github.com/tge-was-taken/GFD-Studio/blob/master/GFDLibrary/Textures/GNF/GNFTexture.cs)), most textures on the server are standard JPEGs
* Most files are using bespoke data formats. Most files on-disc are compressed with the lz4 algorithm

### Servers

- Internal dev server: http://ultramagnus.medmol.local:31312/
- Public community server: https://indreams.me/
- Public short-url server: https://drms.me/thermometer?source=game (example)
- Production server: https://prod.puprod.indreams.me/
- Static assets are served from the CDN: https://cdn-prod.puprod.indreams.me/
- The analytics server (updated every 10 seconds): https://dreams.api.wwsga.me/ (not the full url)

### Data Formats

- TODO

## Current State

- Some of the data formats are **understood** (texts, imps, unimodels)
- Much of the game is driven by the web server. While some of the api can be understood, the secured transport protocol (https) makes sniffing the data **almost impossible without being to decrypt the certificate**
- Practically, this means that downloading creations made in Dreams is **not possible**
- The correlation between resource ids and hashes is **not understood** (possibly described in a file named `bloblist.dat`, `content.json`, or `metadata.json`)
- How the game fetches creations is **not fully known** - but the CDN hosts both hashed binary content and hashes images (in various sizes)

## Other Futures

 - The community push for exporting their creations (reach out!)
 - A means to decrypt the endpoints (hacked console? console emulator?) is discovered
 - Further work is done to reverse engineer and understand the game binary (`eboot.bin`)
 - **Dreams** is updated to support exporting creations
 - **Dreams** becomes open source

