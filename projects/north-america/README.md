# North America Project

This project is configured to download/prepare/build a complete Pelias installation for North America.

As a fairly large build, this will require significant resources to complete quickly. It can still run on a personal computer with 8GB+ RAM, but will take a while. It will require 300GB or so of disk space.

Running an interpolation build of this size would also take many days

Additionally, it requires a polylines file generated with [Valhalla](https://github.com/valhalla).

# Setup

Please refer to the instructions at https://github.com/pelias/docker in order to install and configure your docker environment.

The minimum configuration required in order to run this project are [installing prerequisites](https://github.com/pelias/docker#prerequisites), [install the pelias command](https://github.com/pelias/docker#installing-the-pelias-command) and [configure the environment](https://github.com/pelias/docker#configure-environment).

This build also requires [obtaining or generating a polylines file from Valhalla](https://github.com/pelias/polylines/wiki/Generating-polylines-from-Valhalla). Once you have the polylines file, you must move it to `polylines/extract.0sv` within your project data directory. You can also download the latest `north-america-valhalla.polylines.0sv.gz`, move and rename from: https://geocode.earth/data/

Please ensure that's all working fine before continuing.

# Run a Build

To run a complete build, execute the following commands:

```bash
pelias compose pull
pelias elastic start
pelias elastic wait
pelias elastic create
pelias download all
pelias prepare placeholder
pelias prepare interpolation
pelias import all
pelias compose up
pelias test run
```
**Note a key difference from the commands used in the planet or demo (portland-metro) builds:** Be careful NOT to use `prepare polylines` (and similarly, `prepare all`), as the North America data is too large for Pelias to generate the polylines on its own. This will result in the `extract.0sv` polylines file you added (see above) being overwritten with an empty file, which will  prevent interpolation from being properly built.

# Make an Example Query

You can now make queries against your new Pelias build:

[http://localhost:4000/v1/search?text=empire state building](http://localhost:4000/v1/search?text=empire%20state%20building)
