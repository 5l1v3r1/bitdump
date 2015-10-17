# bitdump
A tool to extract database data from a blind SQL injection vulnerability. Note that this tool will not *find* the vulnerabilities for you; it is assumed one has already been found. This tool will only exploit a given vulnerability to extract data.

### When *not* to use bitdump
Since bitdump has to extract data 1 bit at a time, it is an extremely slow method of reading data. You should probably first check to see if the data may be obtained by other means.

## Usage

`bitdump.py url success attackfield [otherfield, [otherfield ...]]`

  * `url` is the vulnerable injection endpoint.
  * `success` is a string that is **_only_** present in a response from a successful query (i.e., one that returns at least one row). This string must *not* be present in responses from malformed or unsuccessful (empty-result) queries. bitdump uses this string to determine its 1 bit of data per query.
  * `attackfield` is the name of the vulnerable field. For example, if the url is vulnerable to sql injection in the "username" field, then this should be "username".
  * `otherfield` is any other field that must be present in the request in order for it to be successful. By default, all of these fields' values will be set to "" (an empty string). To assign a different value, use `field:value`.
      
      For example, to assign "root" to parameter "username", use `username:root`
          
#####Flags

Bitdump additionally supports the following optional flags:

  * `-h` will print basic usage information.
      Alias: `--help`

  * `-o [OUTFILE]` will redirect all output to OUTFILE instead of `stdout`. Alias: `--outfile`, `--out`

  * `-d [DELAY]` will pause for DELAY ms before sending each query. Alias: `--delay`
        
  * `-v` is used to indicate the amount of logging output to display while running the script, from `-v` to `-vvv`. If no verbose flag is given, no logging output will be displayed (but the final database structure will still be printed when the script completes). Alias: `--verbose`
