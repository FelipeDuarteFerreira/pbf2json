
### Run from pre-built binary

You don't need to have `Go` installed on your system to use the binary file in `./build`:

```bash
$ ./build/pbf2json 
Nothing to do, you must specify tags to match against
```

### Usage

To control which tags are outputted you must pass the `-tags=` flag to `pbf2json` and the PBF filepath:

```bash
$ ./build/pbf2json -tags="amenity" /tmp/wellington_new-zealand.osm.pbf
```
```bash
{"id":170603342,"type":"node","lat":-41.289843000000005,"lon":174.7944402,"tags":{"amenity":"fountain","created_by":"Potlatch 0.5d","name":"Oriental Bay Fountain","source":"knowledge"},"timestamp":"0001-01-01T00:00:00Z"}
{"id":170605346,"type":"node","lat":-41.2861039,"lon":174.7711539,"tags":{"amenity":"fountain","created_by":"Potlatch 0.10c","source":"knowledge"},"timestamp":"0001-01-01T00:00:00Z"}
```

### Advanced Usage

Multiple tags can be specified with commas, records will be returned if they match one `OR` the other:

```bash
$ ./build/pbf2json -tags="building,shop" /tmp/wellington_new-zealand.osm.pbf
```
```bash
{"id":267784221,"type":"node","lat":-41.2975165,"lon":174.7799081,"tags":{"name":"The Warehouse","shop":"department_store"},"timestamp":"0001-01-01T00:00:00Z"}
{"id":279402641,"type":"node","lat":-41.306234100000005,"lon":174.77813590000002,"tags":{"name":"Beaurepaires","shop":"car_repair"},"timestamp":"0001-01-01T00:00:00Z"}
```

Tags can also be grouped with the `+` symbol, records will only be returned if they match one `AND` the other:

```bash
$ ./build/pbf2json -tags="addr:housenumber+addr:street" /tmp/wellington_new-zealand.osm.pbf
```
```bash
{"id":172588254,"type":"node","lat":-41.305838200000004,"lon":174.7634702,"tags":{"addr:city":"Wellington","addr:housenumber":"205","addr:postcode":"6021","addr:street":"Ohiro Road","amenity":"cinema","name":"Penthouse Cinema","source":"knowledge","website":"http://www.penthousecinema.co.nz/"},"timestamp":"0001-01-01T00:00:00Z"}
{"id":267314224,"type":"node","lat":-41.2952482,"lon":174.7749056,"tags":{"addr:city":"Wellington","addr:housenumber":"213","addr:street":"Cuba Street","name":"Comfort Hotel","tourism":"hotel"},"timestamp":"0001-01-01T00:00:00Z"}
```

### Run the go code from source

Make sure `Go` is installed and configured on your system, see: https://gist.github.com/missinglink/4212a81a7d9c125b68d9

```bash
sudo apt-get install mercurial;
go get;
go run osm2pbf.go;
```